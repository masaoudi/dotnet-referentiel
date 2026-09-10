# 🎨 Design Patterns (GoF)

Créationnels, structurels, comportementaux.

## Créationnels

| Pattern | But | Exemple |
|---------|-----|---------|
| **Singleton** | Une seule instance | Configuration, logger |
| **Factory Method** | Déléguer la création | Création de documents |
| **Abstract Factory** | Familles d'objets | UI cross-platform |
| **Builder** | Construction étape par étape | Requêtes SQL |
| **Prototype** | Clonage d'objets | Copie de configurations |

### Singleton

```csharp
public sealed class Config
{
    private static readonly Lazy<Config> _instance = new(() => new Config());
    public static Config Instance => _instance.Value;
    private Config() { }
}
```

### Builder

```csharp
var query = new QueryBuilder()
    .Select("Name", "Age")
    .From("Users")
    .Where("Age > 18")
    .Build();
```

## Structurels

| Pattern | But | Exemple |
|---------|-----|---------|
| **Adapter** | Compatibilité d'interfaces | Wrapper API |
| **Decorator** | Ajouter des responsabilités | Streams, middlewares |
| **Facade** | Interface simplifiée | API gateway |
| **Proxy** | Contrôle d'accès | Lazy loading, cache |
| **Composite** | Arborescence | Menus, fichiers |

## Comportementaux

| Pattern | But | Exemple |
|---------|-----|---------|
| **Observer** | Notification de changement | Événements, SignalR |
| **Strategy** | Algorithmes interchangeables | Tri, paiement |
| **Command** | Encapsuler une requête | Undo/Redo, CQRS |
| **Repository** | Accès aux données | EF Core, Dapper |
| **Unit of Work** | Transaction unique | DbContext EF |

### Strategy

```csharp
public interface IPaymentStrategy
{
    void Pay(decimal amount);
}

public class CreditCardPayment : IPaymentStrategy
{
    public void Pay(decimal amount) { /* ... */ }
}

public class PayPalPayment : IPaymentStrategy
{
    public void Pay(decimal amount) { /* ... */ }
}
```

### Repository

```csharp
public interface IUserRepository
{
    Task<User?> GetByIdAsync(int id);
    Task AddAsync(User user);
    Task SaveChangesAsync();
}
```