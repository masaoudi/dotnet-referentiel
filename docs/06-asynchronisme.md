# ⚡ Asynchronisme & I/O

async/await, Task, bonnes pratiques.

## async / await

Mécanisme pour exécuter des opérations longues sans bloquer le thread principal.

```csharp
public async Task<User> GetUserAsync(int id)
{
    var response = await _httpClient.GetAsync($"/api/users/{id}");
    response.EnsureSuccessStatusCode();
    var json = await response.Content.ReadAsStringAsync();
    return JsonSerializer.Deserialize<User>(json);
}
```

## Types de retour

| Type | Usage |
|------|-------|
| `Task` | Méthode async sans retour |
| `Task<T>` | Méthode async avec retour |
| `ValueTask<T>` | Optimisation (fréquent, sans allocation) |
| `IAsyncEnumerable<T>` | Stream asynchrone |

## Exécution parallèle

```csharp
// Séquentiel
foreach (var id in ids)
    await GetUserAsync(id);

// Parallèle
var tasks = ids.Select(id => GetUserAsync(id));
var users = await Task.WhenAll(tasks);
```

## Bonnes pratiques

### ✅ À FAIRE

- **async all the way** : ne pas bloquer avec `.Result` ou `.Wait()`
- Utiliser `CancellationToken` pour les opérations longues
- `ConfigureAwait(false)` dans les bibliothèques
- Nommer les méthodes async avec suffixe `Async`

### ❌ À NE PAS FAIRE

- `.Result` ou `.Wait()` : risque de **deadlock**
- `async void` : impossible à attendre
- Oublier `await` : l'opération s'exécute en tâche de fond
- Mélanger sync et async sans raison

## CancellationToken

```csharp
public async Task<IEnumerable<User>> GetAllAsync(CancellationToken ct = default)
{
    return await _context.Users.ToListAsync(ct);
}

// Utilisation
using var cts = new CancellationTokenSource(TimeSpan.FromSeconds(30));
var users = await GetAllAsync(cts.Token);
```