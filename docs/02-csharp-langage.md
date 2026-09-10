# 🔷 C# — Langage & Fonctionnement

Syntaxe, GC, IL, JIT, AOT, records et pattern matching.

## Syntaxe & Bases

C# est un langage **orienté objet**, **typé statiquement**, développé par Microsoft.

### Types valeur vs référence

| Type valeur (`struct`) | Type référence (`class`) |
|------------------------|--------------------------|
| `int`, `bool`, `double` | `string`, `object`, `User` |
| Stocké sur la **stack** | Stocké sur le **heap** |
| Copie par valeur | Copie par référence |
| Ne peut pas être `null` (sauf `Nullable<T>`) | Peut être `null` |

### Nullables

```csharp
int? age = null;
string? name = null;

var length = name?.Length ?? 0;
name ??= "Default";
```

### Propriétés

```csharp
// Auto-property
public string Name { get; set; }

// Init-only (immuable après construction)
public Guid Id { get; init; }

// Required (C# 11+)
public required string Email { get; set; }

// Computed
public string FullName => $"{FirstName} {LastName}";
```

## Fonctionnement interne

### 🗑️ GC (Garbage Collector)

- Gère automatiquement la mémoire
- **3 générations** : 0, 1, 2 + LOH (Large Object Heap)
- Libère les objets non référencés
- Modes : **Workstation** (client) / **Server** (multi-thread)
- `IDisposable` pour les ressources non managées

```csharp
public class ResourceHolder : IDisposable
{
    private bool _disposed = false;

    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }

    protected virtual void Dispose(bool disposing)
    {
        if (!_disposed)
        {
            if (disposing) { /* libérer ressources managées */ }
            _disposed = true;
        }
    }
}
```

### ⚙️ IL (Intermediate Language)

- Code compilé par le compilateur C#
- **Indépendant de la plateforme**
- Stocké dans les **assemblies** (`.dll`, `.exe`)
- Lu par le **CLR** (Common Language Runtime)

### 🔥 JIT (Just-In-Time)

- Compile l'IL en **code machine** à l'exécution
- Optimisé pour la plateforme cible
- Compilation à la volée (méthode par méthode)
- **Avantage** : optimisation runtime

### 🚀 AOT (Ahead-Of-Time)

- Compilation **native avant exécution**
- Pas de JIT au runtime
- Démarrage plus rapide
- Idéal pour containers, mobile, IoT
- **Native AOT** disponible depuis .NET 7+

| Critère | JIT | AOT |
|---------|:---:|:---:|
| Démarrage | Lent | Rapide |
| Optimisation runtime | ✅ | ❌ |
| Taille binaire | Petite | Grande |
| Compatibilité | Totale | Limitée |

## Records

Types **immuables** avec **égalité structurelle**.

```csharp
// Record classique
public record User(string Name, int Age);

// Utilisation
var user = new User("Alice", 25);
var updated = user with { Age = 26 };

// Égalité structurelle
var u1 = new User("Alice", 25);
var u2 = new User("Alice", 25);
Console.WriteLine(u1 == u2); // True

// Record struct (C# 10+)
public record struct Point(int X, int Y);
```

## Pattern matching

### `is`

```csharp
if (obj is string s)
    Console.WriteLine(s.Length);

if (obj is int i and > 0)
    Console.WriteLine($"Positif: {i}");
```

### `switch` expression

```csharp
var result = status switch
{
    Status.Active => "Actif",
    Status.Inactive => "Inactif",
    _ => "Inconnu"
};
```

### Property patterns

```csharp
if (user is { Name: "Alice", Age: > 18 })
    Console.WriteLine("Alice majeure");
```

### List patterns (C# 11+)

```csharp
int[] numbers = { 1, 2, 3, 4, 5 };
if (numbers is [1, 2, .., 5])
    Console.WriteLine("Match !");
```