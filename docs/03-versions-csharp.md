# 🆕 Nouveautés C# — Version par version (v2 → v13)

> Évolution complète du langage C# depuis la version 2.0 (2005) jusqu'à la version 13 (2024).

[← Retour au README](../README.md) · [Section précédente](02-csharp.md) · [Section suivante](04-collections.md)

---

## 📋 Table des matières

- [C# 2.0 (2005)](#c-20-2005)
- [C# 3.0 (2007)](#c-30-2007)
- [C# 4.0 (2010)](#c-40-2010)
- [C# 5.0 (2012)](#c-50-2012)
- [C# 6.0 (2015)](#c-60-2015)
- [C# 7.0 (2017)](#c-70-2017)
- [C# 7.1 → 7.3 (2017-2018)](#c-71--73-2017-2018)
- [C# 8.0 (2019)](#c-80-2019)
- [C# 9.0 (2020)](#c-90-2020)
- [C# 10 (2021)](#c-10-2021)
- [C# 11 (2022)](#c-11-2022)
- [C# 12 (2023)](#c-12-2023)
- [C# 13 (2024)](#c-13-2024)
- [📊 Tableau récapitulatif](#-tableau-récapitulatif)

---

## C# 2.0 (2005)

**Framework** : .NET Framework 2.0 · **IDE** : Visual Studio 2005

| Fonctionnalité | Description |
|----------------|-------------|
| **Génériques** | `List<T>`, `Dictionary<K,V>` — types paramétrés |
| **Types nullables** | `int?`, `Nullable<T>` |
| **Méthodes anonymes** | `delegate { }` |
| **Itérateurs** | `yield return` |
| **Classes partielles** | `partial class` |
| **Getters/setters séparés** | Accès différencié |
| **Méthodes partielles** | Déclaration sans implémentation |

```csharp
// Génériques
List<int> numbers = new List<int>();
Dictionary<string, User> users = new Dictionary<string, User>();

// Nullables
int? age = null;
if (age.HasValue) { /* ... */ }

// Itérateurs
public IEnumerable<int> GetNumbers()
{
    yield return 1;
    yield return 2;
    yield return 3;
}
```

---

## C# 3.0 (2007)

**Framework** : .NET Framework 3.5 · **IDE** : Visual Studio 2008

| Fonctionnalité | Description |
|----------------|-------------|
| **LINQ** | Language Integrated Query |
| **Expressions lambda** | `x => x * 2` |
| **Méthodes d'extension** | Ajouter des méthodes à des types existants |
| **Types anonymes** | `new { Name = "x" }` |
| **Typage implicite** | `var` |
| **Initialiseurs d'objets** | `new User { Name = "Alice" }` |
| **Propriétés auto-implémentées** | `public string Name { get; set; }` |
| **Arbres d'expression** | `Expression<Func<T>>` |

```csharp
// LINQ
var adults = users.Where(u => u.Age >= 18).ToList();

// Lambda
Func<int, int> square = x => x * x;

// Méthode d'extension
public static class StringExtensions
{
    public static bool IsNullOrEmpty(this string s) 
        => string.IsNullOrEmpty(s);
}

// Type anonyme
var person = new { Name = "Alice", Age = 25 };

// var
var list = new List<int>();
```

---

## C# 4.0 (2010)

**Framework** : .NET Framework 4.0 · **IDE** : Visual Studio 2010

| Fonctionnalité | Description |
|----------------|-------------|
| **dynamic** | Liaison tardive à l'exécution |
| **Paramètres nommés** | `Method(name: "Alice")` |
| **Paramètres optionnels** | `Method(int x = 0)` |
| **Covariance/contravariance** | Génériques `in`/`out` |
| **Interopérabilité COM** | Améliorée |

```csharp
// dynamic
dynamic obj = GetDynamicObject();
obj.MethodName();

// Paramètres nommés et optionnels
public void CreateUser(string name, int age = 18) { }
CreateUser(name: "Alice", age: 25);
CreateUser("Bob"); // age = 18 par défaut
```

---

## C# 5.0 (2012)

**Framework** : .NET Framework 4.5 · **IDE** : Visual Studio 2012

| Fonctionnalité | Description |
|----------------|-------------|
| **async / await** | Programmation asynchrone |
| **Attributs d'appelant** | `[CallerMemberName]`, `[CallerFilePath]` |
| **Correction foreach** | Closure des variables de boucle |

```csharp
// async/await
public async Task<User> GetUserAsync(int id)
{
    var response = await _httpClient.GetAsync($"/api/users/{id}");
    return await response.Content.ReadFromJsonAsync<User>();
}

// CallerMemberName
public void Log(string message, [CallerMemberName] string caller = "")
{
    Console.WriteLine($"[{caller}] {message}");
}
```

---

## C# 6.0 (2015)

**Framework** : .NET Framework 4.6 · **IDE** : Visual Studio 2015 (Roslyn)

| Fonctionnalité | Description |
|----------------|-------------|
| **Null-conditional** | `?.` |
| **String interpolation** | `$"Hello {name}"` |
| **Auto-property initializers** | `public string Name { get; set; } = "Default";` |
| **Expression-bodied members** | `public int Age => 25;` |
| **nameof** | `nameof(User.Name)` |
| **Using static** | `using static System.Math;` |
| **Exception filters** | `catch (Ex) when (...)` |
| **await dans catch/finally** | Nettoyage asynchrone |

```csharp
// Null-conditional
var length = user?.Name?.Length ?? 0;

// String interpolation
var message = $"Hello {user.Name}, you are {user.Age} years old";

// Expression-bodied
public string FullName => $"{FirstName} {LastName}";

// nameof
throw new ArgumentNullException(nameof(user));

// Exception filter
try { /* ... */ }
catch (HttpException ex) when (ex.StatusCode == 404) { /* ... */ }
```

---

## C# 7.0 (2017)

**Framework** : .NET Framework 4.7 · **IDE** : Visual Studio 2017

| Fonctionnalité | Description |
|----------------|-------------|
| **Tuples** | `(int, string)` |
| **Out variables** | `out var x` |
| **Pattern matching** | `is`, `switch` |
| **Local functions** | Fonctions imbriquées |
| **Ref returns & locals** | Retour par référence |
| **Discards** | `_` |
| **Binary literals** | `0b1010` |
| **Digit separators** | `1_000_000` |

```csharp
// Tuples
(int Id, string Name) GetUser() => (1, "Alice");
var (id, name) = GetUser();

// Out variables
if (int.TryParse("123", out var number))
    Console.WriteLine(number);

// Pattern matching
switch (obj)
{
    case int i when i > 0:
        Console.WriteLine($"Positive: {i}");
        break;
    case string s:
        Console.WriteLine($"String: {s}");
        break;
}

// Local functions
int Fibonacci(int n)
{
    return n <= 1 ? n : Fibonacci(n - 1) + Fibonacci(n - 2);
}

// Digit separators
var million = 1_000_000;
var binary = 0b1010_1010;
```

---

## C# 7.1 → 7.3 (2017-2018)

**Frameworks** : .NET Core 2.x · **IDE** : VS 2017 v15.3 → v15.7

### C# 7.1
- **async Main** : `static async Task Main()`
- **Default literal** : `default`
- **Inférence des noms de tuples**

### C# 7.2
- **in parameters** (readonly ref)
- **readonly structs**
- **private protected**
- **Span<T>** (interior pointer)

### C# 7.3
- **Contraintes génériques** : `enum`, `delegate`, `unmanaged`
- **Réassignation ref**
- **Initialisation stackalloc**
- **== et != pour les tuples**

```csharp
// C# 7.1 : async Main
static async Task Main(string[] args)
{
    await RunAsync();
}

// C# 7.2 : readonly struct
public readonly struct Point
{
    public int X { get; }
    public int Y { get; }
    public Point(int x, int y) => (X, Y) = (x, y);
}

// C# 7.3 : contraintes
public void Process<T>(T value) where T : unmanaged { }
```

---

## C# 8.0 (2019)

**Framework** : .NET Core 3.0 · **IDE** : Visual Studio 2019

| Fonctionnalité | Description |
|----------------|-------------|
| **Nullable reference types** | `string?` |
| **Async streams** | `IAsyncEnumerable<T>` |
| **Ranges & indices** | `..`, `^` |
| **Using declarations** | `using var x = ...` |
| **Switch expressions** | `=>` |
| **Property patterns** | `{ Name: "Alice" }` |
| **Static local functions** | Optimisation |
| **Default interface methods** | Implémentation par défaut |
| **Readonly members** | `readonly` sur membres de struct |

```csharp
// Nullable reference types
#nullable enable
public string? FindName(int id) => id > 0 ? "Alice" : null;

// Async streams
public async IAsyncEnumerable<int> GetNumbersAsync()
{
    for (int i = 0; i < 10; i++)
    {
        await Task.Delay(100);
        yield return i;
    }
}

// Ranges & indices
var array = new[] { 1, 2, 3, 4, 5 };
var slice = array[1..4];  // [2, 3, 4]
var last = array[^1];     // 5

// Switch expression
var result = status switch
{
    Status.Active => "Actif",
    Status.Inactive => "Inactif",
    _ => "Inconnu"
};

// Property patterns
if (user is { Name: "Alice", Age: > 18 })
    Console.WriteLine("Alice majeure");
```

---

## C# 9.0 (2020)

**Framework** : .NET 5 · **IDE** : Visual Studio 2019 v16.8

| Fonctionnalité | Description |
|----------------|-------------|
| **Records** | Types immuables |
| **Init-only properties** | `init` |
| **Top-level statements** | Program.cs simplifié |
| **Pattern matching** amélioré | Relational, logical |
| **Target-typed new** | `Person p = new();` |
| **With-expressions** | `user with { Name = "Bob" }` |
| **Native ints** | `nint`, `nuint` |
| **Function pointers** | `delegate*` |
| **Lambda discard** | `(_, _) => ...` |

```csharp
// Records
public record User(string Name, int Age);

var user = new User("Alice", 25);
var updated = user with { Age = 26 };

// Init-only
public class Person
{
    public string Name { get; init; }
}

// Top-level statements
// Program.cs
Console.WriteLine("Hello World!");

// Target-typed new
List<int> numbers = new();
Person person = new();

// Pattern matching amélioré
if (age is >= 18 and < 65)
    Console.WriteLine("Adulte actif");
```

---

## C# 10 (2021)

**Framework** : .NET 6 · **IDE** : Visual Studio 2022

| Fonctionnalité | Description |
|----------------|-------------|
| **Global using directives** | `global using System;` |
| **File-scoped namespaces** | `namespace X;` |
| **Record structs** | `record struct Point(int X, int Y)` |
| **With expressions sur structs** | |
| **Constant interpolated strings** | |
| **Lambda natural types** | |
| **Extended property patterns** | |

```csharp
// Global usings
// GlobalUsings.cs
global using System;
global using System.Collections.Generic;
global using System.Linq;

// File-scoped namespace
namespace MyApp.Services;

public class UserService { }

// Record struct
public record struct Point(int X, int Y);
```

---

## C# 11 (2022)

**Framework** : .NET 7 · **IDE** : Visual Studio 2022 v17.4

| Fonctionnalité | Description |
|----------------|-------------|
| **Raw string literals** | `"""..."""` |
| **Required members** | `required` |
| **Generic math** | `INumber<T>` |
| **List patterns** | `[1, 2, ..]` |
| **UTF-8 string literals** | `u8` |
| **File-local types** | `file class` |
| **Static abstract members** | Interfaces |

```csharp
// Raw string literals
var json = """
    {
        "name": "Alice",
        "age": 25
    }
    """;

// Required members
public class User
{
    public required string Name { get; set; }
    public required string Email { get; set; }
}

var user = new User { Name = "Alice", Email = "a@b.com" };

// List patterns
int[] numbers = { 1, 2, 3, 4, 5 };
if (numbers is [1, 2, .., 5])
    Console.WriteLine("Match !");

// Generic math
public T Add<T>(T a, T b) where T : INumber<T> => a + b;
```

---

## C# 12 (2023)

**Framework** : .NET 8 · **IDE** : Visual Studio 2022 v17.8

| Fonctionnalité | Description |
|----------------|-------------|
| **Primary constructors** | Classes et structs |
| **Collection expressions** | `[1, 2, 3]` |
| **Inline arrays** | `[InlineArray]` |
| **Optional lambda parameters** | |
| **ref readonly parameters** | |
| **Alias any type** | `using Point = (int, int);` |

```csharp
// Primary constructors
public class UserService(IUserRepository repository, ILogger logger)
{
    public async Task<User> GetAsync(int id)
    {
        logger.LogInformation("Getting user {Id}", id);
        return await repository.GetByIdAsync(id);
    }
}

// Collection expressions
List<int> numbers = [1, 2, 3, 4, 5];
int[] array = [1, 2, 3];
Span<int> span = [1, 2, 3];

// Alias any type
using Point = (int X, int Y);
Point p = (10, 20);
```

---

## C# 13 (2024)

**Framework** : .NET 9 · **IDE** : Visual Studio 2022 v17.12

| Fonctionnalité | Description |
|----------------|-------------|
| **Params collections** | Au-delà des arrays |
| **New lock type** | `System.Threading.Lock` |
| **Partial properties** | |
| **Implicit index access** | `^` dans initializers |
| **ref struct en async/iterator** | |
| **Overload resolution priority** | |

```csharp
// Params collections
public void Process(params ReadOnlySpan<int> numbers) { }
public void ProcessList(params List<string> items) { }

// New lock
private readonly Lock _lock = new();
lock (_lock)
{
    // Section critique
}

// Implicit index access
var array = new int[5];
array[^1] = 10; // Dernier élément
```

---

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

---

> [!TIP]
> **À retenir pour l'entretien**
> 
> Les versions à citer absolument : **C# 2.0** (génériques), **C# 3.0** (LINQ), **C# 5.0** (async/await), **C# 6** (interpolation), **C# 8** (nullable reference types), **C# 9** (records), **C# 12** (primary constructors).

---

[← Retour au README](../README.md) · [Section précédente](02-csharp.md) · [Section suivante](04-collections.md)