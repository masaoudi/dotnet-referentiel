# 🔗 LINQ & Sérialisation

Syntaxe méthode vs requête, opérateurs et formats de sérialisation.

## LINQ (Language Integrated Query)

Permet d'interroger des collections, bases de données, XML avec une syntaxe unifiée.

### Syntaxe méthode (fluent)

```csharp
var result = users
    .Where(u => u.Age > 18)
    .OrderBy(u => u.Name)
    .Select(u => new { u.Name, u.Email })
    .ToList();
```

### Syntaxe requête (query)

```csharp
var result = from u in users
             where u.Age > 18
             orderby u.Name
             select new { u.Name, u.Email };
```

### Opérateurs courants

| Catégorie | Opérateurs |
|-----------|------------|
| **Filtrage** | `Where`, `OfType`, `Distinct` |
| **Projection** | `Select`, `SelectMany` |
| **Tri** | `OrderBy`, `OrderByDescending`, `ThenBy` |
| **Regroupement** | `GroupBy`, `ToLookup` |
| **Jointure** | `Join`, `GroupJoin` |
| **Agrégation** | `Sum`, `Count`, `Average`, `Min`, `Max` |
| **Quantificateurs** | `Any`, `All`, `Contains` |
| **Éléments** | `First`, `Single`, `Last`, `ElementAt` |
| **Ensembles** | `Union`, `Intersect`, `Except` |

### Deferred execution

```csharp
var query = users.Where(u => u.Age > 18); // Pas encore exécuté
var list = query.ToList(); // Exécuté maintenant
```

## Sérialisation

| Format | Bibliothèque | Avantages | Inconvénients |
|--------|--------------|-----------|---------------|
| **JSON** | System.Text.Json, Newtonsoft | Léger, standard web | Moins compact |
| **XML** | XmlSerializer, XDocument | Standard, XSD | Verbeux |
| **Protobuf** | Google.Protobuf | Compact, rapide | Schéma requis |
| **MessagePack** | MessagePack-CSharp | Binaire compact | Moins lisible |

### JSON

```csharp
// System.Text.Json
var json = JsonSerializer.Serialize(user);
var user = JsonSerializer.Deserialize<User>(json);

// Options
var options = new JsonSerializerOptions
{
    PropertyNamingPolicy = JsonNamingPolicy.CamelCase,
    WriteIndented = true
};
```

### Protobuf

```csharp
[ProtoContract]
public class User
{
    [ProtoMember(1)] public string Name { get; set; }
    [ProtoMember(2)] public int Age { get; set; }
}
```