# 🚫 À ne pas faire dans votre code

Les anti-patterns et erreurs courantes à éviter.

## 26.1 Code & Structure

### ✅ À FAIRE

- **Méthodes courtes** : idéalement moins de 20 lignes
- **Responsabilité unique** : une classe = une tâche
- **Noms significatifs** : auto-documentés
- **Guards clauses** en début de méthode
- **Commenter le « pourquoi »**

### ❌ À NE PAS FAIRE

- **Méthodes de 500 lignes**
- **Classes fourre-tout** (God Class)
- **Noms obscurs** : `x`, `temp`, `data`
- **Duplication de code**
- **Magic numbers**

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
                    foreach (var item in o.Items)
                    {
                        if (item.Price > 0) { /* 30 lignes... */ }
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
```

## 26.2 Gestion des erreurs

### ❌ MAUVAIS

```csharp
try { var result = ProcessData(); }
catch (Exception) { } // Avale silencieusement !

try { DoSomething(); }
catch (Exception ex) { throw ex; } // Perd la stack trace !
```

### ✅ BON

```csharp
try { var result = await ProcessDataAsync(); }
catch (SqlException ex) when (ex.Number == -2)
{
    _logger.LogWarning(ex, "Timeout");
    throw new DataProcessingException("Expiré", ex);
}

try { DoSomething(); }
catch (Exception ex)
{
    _logger.LogError(ex, "Erreur");
    throw; // Préserve la stack trace
}
```

## 26.3 Async/Await

### ❌ MAUVAIS

```csharp
public void ProcessData()
{
    var result = GetDataAsync().Result; // Deadlock !
}

public async void FireAndForget() { } // Impossible à attendre
```

### ✅ BON

```csharp
public async Task ProcessDataAsync(CancellationToken ct = default)
{
    var result = await GetDataAsync(ct);
}
```

## 26.4 Sécurité

### ❌ MAUVAIS

```csharp
// Injection SQL !
var query = "SELECT * FROM Users WHERE Name = '" + userName + "'";
```

### ✅ BON

```csharp
var query = "SELECT * FROM Users WHERE Name = @Name";
using var cmd = new SqlCommand(query, connection);
cmd.Parameters.AddWithValue("@Name", userName);
```

## 26.5 Performance

### ❌ MAUVAIS

```csharp
// Concaténation en boucle
string result = "";
for (int i = 0; i < 10000; i++)
    result += i.ToString();

// Requête N+1
var orders = await _context.Orders.ToListAsync();
foreach (var order in orders)
    var customer = await _context.Customers.FindAsync(order.CustomerId);
```

### ✅ BON

```csharp
// StringBuilder
var sb = new StringBuilder();
for (int i = 0; i < 10000; i++)
    sb.Append(i);

// Include
var orders = await _context.Orders.Include(o => o.Customer).ToListAsync();
```

## 26.6 Tests

### ❌ MAUVAIS

```csharp
[Test]
public void Test1()
{
    var service = new UserService(new SqlRepository()); // DB réelle !
    var result = service.GetUser(1);
    Assert.IsNotNull(result);
    Assert.AreEqual("Alice", result.Name);
}
```

### ✅ BON

```csharp
[Test]
public async Task GetUserAsync_ExistingId_ReturnsUserWithCorrectName()
{
    var mockRepo = new Mock<IUserRepository>();
    mockRepo.Setup(r => r.GetByIdAsync(1))
            .ReturnsAsync(new User { Id = 1, Name = "Alice" });
    var service = new UserService(mockRepo.Object);

    var result = await service.GetUserAsync(1);

    Assert.That(result.Name, Is.EqualTo("Alice"));
}
```

## 🚨 Les 10 erreurs les plus graves

> ⚠️ Ces erreurs sont **rédhibitoires** en entretien technique.

1. **`catch (Exception) { }`** — avale les erreurs
2. **`throw ex;`** — perd la stack trace
3. **`.Result` / `.Wait()`** — deadlocks
4. **`async void`** — exceptions perdues
5. **Injection SQL** — concaténation SQL
6. **Secrets dans Git** — mots de passe
7. **God Class** — classes qui font tout
8. **Requêtes N+1** — performances
9. **Code dupliqué** — violation DRY
10. **Pas de tests** — dette technique