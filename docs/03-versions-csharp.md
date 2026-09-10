# 🆕 Nouveautés C# — Version par version (v2 → v13)

Évolution complète du langage C# depuis la version 2.0 (2005) jusqu'à la version 13 (2024).

## C# 2.0 (2005)

**Framework** : .NET Framework 2.0 · **IDE** : Visual Studio 2005

- **Génériques** : `List<T>`, `Dictionary<K,V>`
- **Types nullables** : `int?`, `Nullable<T>`
- **Méthodes anonymes** : `delegate { }`
- **Itérateurs** : `yield return`
- **Classes partielles** : `partial class`
- **Méthodes partielles**

```csharp
List<int> numbers = new List<int>();
int? age = null;

public IEnumerable<int> GetNumbers()
{
    yield return 1;
    yield return 2;
}
```

## C# 3.0 (2007)

**Framework** : .NET Framework 3.5 · **IDE** : Visual Studio 2008

- **LINQ**
- **Expressions lambda** : `x => x * 2`
- **Méthodes d'extension**
- **Types anonymes** : `new { Name = "x" }`
- **Typage implicite** : `var`
- **Initialiseurs d'objets**
- **Propriétés auto-implémentées**
- **Arbres d'expression**

```csharp
var adults = users.Where(u => u.Age >= 18).ToList();
var person = new { Name = "Alice", Age = 25 };
```

## C# 4.0 (2010)

**Framework** : .NET Framework 4.0 · **IDE** : Visual Studio 2010

- **dynamic** : liaison tardive
- **Paramètres nommés** : `Method(name: "Alice")`
- **Paramètres optionnels** : `Method(int x = 0)`
- **Covariance/contravariance**

```csharp
dynamic obj = GetDynamicObject();
public void CreateUser(string name, int age = 18) { }
```

## C# 5.0 (2012)

**Framework** : .NET Framework 4.5 · **IDE** : Visual Studio 2012

- **async / await**
- **Attributs d'appelant** : `[CallerMemberName]`
- **Correction foreach** : closure des variables

```csharp
public async Task<User> GetUserAsync(int id)
{
    var response = await _httpClient.GetAsync($"/api/users/{id}");
    return await response.Content.ReadFromJsonAsync<User>();
}
```

## C# 6.0 (2015)

**Framework** : .NET Framework 4.6 · **IDE** : Visual Studio 2015 (Roslyn)

- **Null-conditional** : `?.`
- **String interpolation** : `$"Hello {name}"`
- **Auto-property initializers**
- **Expression-bodied members**
- **nameof** : `nameof(User.Name)`
- **Using static**
- **Exception filters** : `catch (Ex) when (...)`
- **await dans catch/finally**

```csharp
var length = user?.Name?.Length ?? 0;
var message = $"Hello {user.Name}";
public string FullName => $"{FirstName} {LastName}";
throw new ArgumentNullException(nameof(user));
```

## C# 7.0 (2017)

**Framework** : .NET Framework 4.7 · **IDE** : Visual Studio 2017

- **Tuples** : `(int, string)`
- **Out variables** : `out var x`
- **Pattern matching** : `is`, `switch`
- **Local functions**
- **Ref returns & locals**
- **Discards** : `_`
- **Binary literals** : `0b1010`
- **Digit separators** : `1_000_000`

```csharp
(int Id, string Name) GetUser() => (1, "Alice");
var (id, name) = GetUser();

if (int.TryParse("123", out var number))
    Console.WriteLine(number);

var million = 1_000_000;
```

## C# 7.1 → 7.3 (2017-2018)

**Frameworks** : .NET Core 2.x · **IDE** : VS 2017 v15.3 → v15.7

### C# 7.1
- **async Main** : `static async Task Main()`
- **Default literal** : `default`

### C# 7.2
- **in parameters** (readonly ref)
- **readonly structs**
- **private protected**
- **Span<T>**

### C# 7.3
- **Contraintes génériques** : `enum`, `delegate`, `unmanaged`
- **Réassignation ref**
- **Initialisation stackalloc**
- **== et != pour les tuples**

```csharp
static async Task Main(string[] args) { await RunAsync(); }

public readonly struct Point
{
    public int X { get; }
    public int Y { get; }
    public Point(int x, int y) => (X, Y) = (x, y);
}
```

## C# 8.0 (2019)

**Framework** : .NET Core 3.0 · **IDE** : Visual Studio 2019

- **Nullable reference types** : `string?`
- **Async streams** : `IAsyncEnumerable<T>`
- **Ranges & indices** : `..`, `^`
- **Using declarations** : `using var x = ...`
- **Switch expressions**
- **Property patterns**
- **Static local functions**
- **Default interface methods**

```csharp
#nullable enable
public string? FindName(int id) => id > 0 ? "Alice" : null;

var array = new[] { 1, 2, 3, 4, 5 };
var slice = array[1..4];
var last = array[^1];

var result = status switch
{
    Status.Active => "Actif",
    Status.Inactive => "Inactif",
    _ => "Inconnu"
};
```

## C# 9.0 (2020)

**Framework** : .NET 5 · **IDE** : Visual Studio 2019 v16.8

- **Records** : `record User(string Name)`
- **Init-only properties** : `init`
- **Top-level statements**
- **Pattern matching** amélioré
- **Target-typed new** : `Person p = new();`
- **With-expressions**
- **Native ints** : `nint`, `nuint`
- **Function pointers**

```csharp
public record User(string Name, int Age);

var user = new User("Alice", 25);
var updated = user with { Age = 26 };

List<int> numbers = new();
```

## C# 10 (2021)

**Framework** : .NET 6 · **IDE** : Visual Studio 2022

- **Global using directives** : `global using System;`
- **File-scoped namespaces** : `namespace X;`
- **Record structs**
- **With expressions sur structs**
- **Constant interpolated strings**
- **Lambda natural types**
- **Extended property patterns**

```csharp
// GlobalUsings.cs
global using System;
global using System.Linq;

// File-scoped namespace
namespace MyApp.Services;

public record struct Point(int X, int Y);
```

## C# 11 (2022)

**Framework** : .NET 7 · **IDE** : Visual Studio 2022 v17.4

- **Raw string literals** : `"""..."""`
- **Required members** : `required`
- **Generic math** : `INumber<T>`
- **List patterns** : `[1, 2, ..]`
- **UTF-8 string literals** : `u8`
- **File-local types**
- **Static abstract members**

```csharp
var json = """
    {
        "name": "Alice"
    }
    """;

public class User
{
    public required string Name { get; set; }
    public required string Email { get; set; }
}

int[] numbers = { 1, 2, 3, 4, 5 };
if (numbers is [1, 2, .., 5])
    Console.WriteLine("Match !");
```

## C# 12 (2023)

**Framework** : .NET 8 · **IDE** : Visual Studio 2022 v17.8

- **Primary constructors** (classes et structs)
- **Collection expressions** : `[1, 2, 3]`
- **Inline arrays**
- **Optional lambda parameters**
- **ref readonly parameters**
- **Alias any type** : `using Point = (int, int);`

```csharp
public class UserService(IUserRepository repository, ILogger logger)
{
    public async Task<User> GetAsync(int id)
    {
        logger.LogInformation("Getting user {Id}", id);
        return await repository.GetByIdAsync(id);
    }
}

List<int> numbers = [1, 2, 3, 4, 5];

using Point = (int X, int Y);
Point p = (10, 20);
```

## C# 13 (2024)

**Framework** : .NET 9 · **IDE** : Visual Studio 2022 v17.12

- **Params collections** : au-delà des arrays
- **New lock type** : `System.Threading.Lock`
- **Partial properties**
- **Implicit index access** : `^`
- **ref struct en async/iterator**
- **Overload resolution priority**

```csharp
public void Process(params ReadOnlySpan<int> numbers) { }

private readonly Lock _lock = new();
lock (_lock)
{
    // Section critique
}
```

## 📊 Tableau récapitulatif

| Version | Année | .NET | Fonctionnalité phare |
|:-------:|:-----:|:----:|---------------------|
| **C# 2.0** | 2005 | .NET Framework 2.0 | Génériques, nullables |
| **C# 3.0** | 2007 | .NET Framework 3.5 | LINQ, lambda, var |
| **C# 4.0** | 2010 | .NET Framework 4.0 | dynamic, paramètres nommés |
| **C# 5.0** | 2012 | .NET Framework 4.5 | async/await |
| **C# 6.0** | 2015 | .NET Framework 4.6 | Null-conditional, string interpolation |
| **C# 7.0** | 2017 | .NET Framework 4.7 | Tuples, pattern matching |
| **C# 7.1-7.3** | 2017-2018 | .NET Core 2.x | async Main, readonly structs |
| **C# 8.0** | 2019 | .NET Core 3.0 | Nullable reference types |
| **C# 9.0** | 2020 | .NET 5 | Records |
| **C# 10** | 2021 | .NET 6 | File-scoped namespaces |
| **C# 11** | 2022 | .NET 7 | Required members |
| **C# 12** | 2023 | .NET 8 | Primary constructors |
| **C# 13** | 2024 | .NET 9 | Params collections |

## 💡 À retenir pour l'entretien

Les versions à citer absolument :
- **C# 2.0** (génériques)
- **C# 3.0** (LINQ)
- **C# 5.0** (async/await)
- **C# 6** (interpolation)
- **C# 8** (nullable reference types)
- **C# 9** (records)
- **C# 12** (primary constructors)