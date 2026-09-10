# 🚫 À ne pas faire dans votre code

> Les anti-patterns et erreurs courantes à éviter absolument pour un développeur professionnel.

[← Retour au README](../README.md) · [Section précédente](25-ia.md) · [Section suivante](27-code-propre.md)

---

## 📋 Table des matières

- [26.1 Code & Structure](#261-code--structure)
- [26.2 Gestion des erreurs](#262-gestion-des-erreurs)
- [26.3 Async/Await](#263-asyncawait)
- [26.4 Sécurité](#264-sécurité)
- [26.5 Performance](#265-performance)
- [26.6 Tests](#266-tests)
- [🚨 Les 10 erreurs les plus graves](#-les-10-erreurs-les-plus-graves)

---

## 26.1 Code & Structure

### ✔️ À FAIRE

- **Méthodes courtes** : idéalement moins de 20 lignes
- **Responsabilité unique** : une classe = une tâche
- **Noms significatifs** : auto-documentés
- **Éviter le nesting profond** : max 3 niveaux
- **Guards clauses** en début de méthode
- **Commenter le « pourquoi »**, pas le « quoi »

### ✘ À NE PAS FAIRE

- **Méthodes de 500 lignes** avec 10 niveaux d'indentation
- **Classes fourre-tout** (God Class) qui font tout
- **Noms obscurs** : `x`, `temp`, `data`, `manager`
- **Duplication de code** (violation DRY)
- **Commentaires inutiles** qui répètent le code
- **Code mort** commenté qui reste dans le repo
- **Magic numbers** sans constantes nommées

### ❌ MAUVAIS

```csharp
public void ProcessOrder(Order o)
{
    if (o != null)
    {
        if (o.Items != null)
        {
            if (o.Items.Count > 0)
            {
                if (o.Status == 2) // Que signifie 2 ?
                {
                    // 50 lignes de traitement...
                    foreach (var item in o.Items)
                    {
                        if (item.Price > 0)
                        {
                            // 30 lignes...
                        }
                    }
                }
            }
        }
    }
}
```

### ✅ BON

```csharp
private const int OrderStatusPaid = 2;

public void ProcessOrder(Order order)
{
    ArgumentNullException.ThrowIfNull(order);
    
    if (!order.HasItems) return;
    if (order.Status != OrderStatusPaid) return;
    
    ProcessOrderItems(order.Items);
}

private void ProcessOrderItems(IEnumerable<OrderItem> items)
{
    foreach (var item in items.Where(i => i.IsValid))
    {
        ProcessItem(item);
    }
}
```

---

## 26.2 Gestion des erreurs

### ✔️ À FAIRE

- **Attraper des exceptions spécifiques**, pas `Exception`
- **Logger les exceptions** avec contexte
- **Utiliser des exceptions custom** pour le domaine
- **Valider les entrées** en amont
- **Utiliser `ArgumentNullException.ThrowIfNull`**
- **Libérer les ressources** avec `using`

### ✘ À NE PAS FAIRE

- **`catch (Exception) { }`** : avale les erreurs silencieusement
- **`throw ex;`** : perd la stack trace (utiliser `throw;`)
- **Utiliser les exceptions pour le contrôle de flux**
- **Exceptions vides** sans logging
- **Ressources non libérées** (fuites mémoire)
- **Mot de passe en clair** dans le code

### ❌ MAUVAIS

```csharp
try 
{ 
    var result = ProcessData();
}
catch (Exception) { } // Avale silencieusement !

try 
{ 
    DoSomething();
}
catch (Exception ex) 
{ 
    throw ex; // Perd la stack trace !
}
```

### ✅ BON

```csharp
try 
{ 
    var result = await ProcessDataAsync();
}
catch (SqlException ex) when (ex.Number == -2)
{
    _logger.LogWarning(ex, "Timeout lors du traitement");
    throw new DataProcessingException("Le traitement a expiré", ex);
}

try 
{ 
    DoSomething();
}
catch (Exception ex) 
{ 
    _logger.LogError(ex, "Erreur lors de DoSomething");
    throw; // Préserve la stack trace
}
```

---

## 26.3 Async/Await

### ✔️ À FAIRE

- **async all the way** : ne pas bloquer avec `.Result` ou `.Wait()`
- **Utiliser `CancellationToken`** pour les opérations longues
- **`ConfigureAwait(false)`** dans les bibliothèques
- **Retourner `Task` ou `ValueTask`**
- **Nommer les méthodes async avec suffixe `Async`**

### ✘ À NE PAS FAIRE

- **`.Result` ou `.Wait()`** : risque de deadlock
- **`async void`** : impossible à attendre
- **Oublier `await`** : l'opération s'exécute en tâche de fond
- **Mélanger sync et async** sans raison
- **Créer des threads manuellement** au lieu d'utiliser Task

### ❌ MAUVAIS

```csharp
public void ProcessData()
{
    var result = GetDataAsync().Result; // Deadlock possible !
}

public async void FireAndForget() // Impossible à attendre
{
    await DoSomethingAsync();
}
```

### ✅ BON

```csharp
public async Task ProcessDataAsync(CancellationToken ct = default)
{
    var result = await GetDataAsync(ct);
    // traitement...
}
```

---

## 26.4 Sécurité

### ✔️ À FAIRE

- **Requêtes paramétrées** pour éviter l'injection SQL
- **Valider toutes les entrées utilisateur**
- **Stocker les secrets dans Key Vault**
- **Hasher les mots de passe** (bcrypt, Argon2)
- **Utiliser HTTPS partout**
- **Principe du moindre privilège**

### ✘ À NE PAS FAIRE

- **Concaténer des chaînes SQL** : injection SQL
- **Stocker des secrets dans appsettings.json** ou Git
- **Faire confiance aux entrées client**
- **Utiliser MD5/SHA1** pour les mots de passe
- **Exposer des stack traces** en production
- **Désactiver la validation SSL**

### ❌ MAUVAIS

```csharp
// Injection SQL !
var query = "SELECT * FROM Users WHERE Name = '" + userName + "'";
```

### ✅ BON

```csharp
// Requête paramétrée
var query = "SELECT * FROM Users WHERE Name = @Name";
using var cmd = new SqlCommand(query, connection);
cmd.Parameters.AddWithValue("@Name", userName);
```

---

## 26.5 Performance

### ✔️ À FAIRE

- **Utiliser `StringBuilder`** pour les concaténations en boucle
- **Paginer les requêtes** (Skip/Take)
- **Utiliser `AsNoTracking()`** pour les lectures EF
- **Mettre en cache** les données fréquemment accédées
- **Utiliser `Span<T>`** pour éviter les allocations

### ✘ À NE PAS FAIRE

- **Concaténer des strings en boucle** : allocations massives
- **Requêtes N+1** : un appel par élément
- **Charger toutes les données** en mémoire sans filtre
- **Appeler `.ToList()` trop tôt** dans une requête LINQ
- **Ignorer le `CancellationToken`**

### ❌ MAUVAIS

```csharp
// Concaténation en boucle
string result = "";
for (int i = 0; i < 10000; i++)
{
    result += i.ToString(); // 10 000 allocations !
}

// Requête N+1
var orders = await _context.Orders.ToListAsync();
foreach (var order in orders)
{
    var customer = await _context.Customers.FindAsync(order.CustomerId);
}
```

### ✅ BON

```csharp
// StringBuilder
var sb = new StringBuilder();
for (int i = 0; i < 10000; i++)
{
    sb.Append(i);
}
var result = sb.ToString();

// Include / projection
var orders = await _context.Orders
    .Include(o => o.Customer)
    .ToListAsync();
```

---

## 26.6 Tests

### ✔️ À FAIRE

- **Un test = un comportement**
- **Pattern AAA** (Arrange, Act, Assert)
- **Noms de tests descriptifs**
- **Tester les cas limites** (null, vide, max)
- **Mocker les dépendances externes**
- **Tests indépendants et isolés**

### ✘ À NE PAS FAIRE

- **Tester l'implémentation** plutôt que le comportement
- **Tests dépendants** de l'ordre d'exécution
- **Mocker tout**, même les objets simples
- **Ignorer les cas d'erreur**
- **Tests lents** à cause d'appels réels (DB, HTTP)
- **Assertions multiples** dans un seul test

### ❌ MAUVAIS

```csharp
[Test]
public void Test1()
{
    var service = new UserService(new SqlRepository()); // DB réelle !
    var result = service.GetUser(1);
    Assert.IsNotNull(result);
    Assert.AreEqual("Alice", result.Name);
    Assert.AreEqual(25, result.Age);
}
```

### ✅ BON

```csharp
[Test]
public async Task GetUserAsync_ExistingId_ReturnsUserWithCorrectName()
{
    // Arrange
    var mockRepo = new Mock<IUserRepository>();
    mockRepo.Setup(r => r.GetByIdAsync(1))
            .ReturnsAsync(new User { Id = 1, Name = "Alice" });
    var service = new UserService(mockRepo.Object);

    // Act
    var result = await service.GetUserAsync(1);

    // Assert
    Assert.That(result.Name, Is.EqualTo("Alice"));
}
```

---

## 🚨 Les 10 erreurs les plus graves

> [!CAUTION]
> Ces erreurs sont considérées comme **rédhibitoires** en entretien technique.

1. **`catch (Exception) { }`** — avale les erreurs silencieusement
2. **`throw ex;`** — perd la stack trace (utiliser `throw;`)
3. **`.Result` / `.Wait()`** — deadlocks en async
4. **`async void`** — impossible à attendre, exceptions perdues
5. **Injection SQL** — concaténation de chaînes SQL
6. **Secrets dans Git** — mots de passe, clés API
7. **God Class** — classes qui font tout
8. **Requêtes N+1** — performances désastreuses
9. **Code dupliqué** — violation DRY
10. **Pas de tests** — dette technique garantie

---

[← Retour au README](../README.md) · [Section précédente](25-ia.md) · [Section suivante](27-code-propre.md)