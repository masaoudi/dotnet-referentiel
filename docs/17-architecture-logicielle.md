# 🏗️ Architecture logicielle

Clean Architecture, DDD.

## Organisation de projet .NET

```
MySolution/
├── src/
│   ├── MyApp.Domain/          # Entités, value objects
│   ├── MyApp.Application/     # Use cases, DTOs
│   ├── MyApp.Infrastructure/  # EF Core, repositories
│   └── MyApp.WebApi/          # Controllers, Program.cs
├── tests/
│   ├── MyApp.UnitTests/
│   └── MyApp.IntegrationTests/
└── MySolution.sln
```

## Clean Architecture

### Principe

Les dépendances **pointent vers l'intérieur**.

```
Domain ← Application ← Infrastructure
              ↑
            WebApi
```

### Avantages

- Domaine indépendant
- Testabilité accrue
- Inversion de dépendance

## DDD (Domain-Driven Design)

### Concepts clés

| Concept | Description |
|---------|-------------|
| **Entité** | Identité unique |
| **Value Object** | Immuable, sans identité |
| **Agrégat** | Groupe d'entités cohérentes |
| **Repository** | Accès aux agrégats |
| **Domain Event** | Événement métier |
| **Bounded Context** | Frontière du domaine |
| **Ubiquitous Language** | Langage commun |

### Exemple

```csharp
// Value Object
public record Money(decimal Amount, string Currency);

// Entité
public class Order
{
    public Guid Id { get; private set; }
    public Money Total { get; private set; }
    private readonly List<OrderLine> _lines = new();

    public void AddLine(Product product, int quantity)
    {
        _lines.Add(new OrderLine(product, quantity));
        RecalculateTotal();
    }
}
```