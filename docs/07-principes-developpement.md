# 🧭 Principes de développement

SOLID + YAGNI, KISS, DRY.

## SOLID

### S — Single Responsibility Principle

Une classe = **une seule responsabilité** = une seule raison de changer.

```csharp
// ❌ Mauvais : fait tout
public class UserService
{
    public void SaveUser() { }
    public void SendEmail() { }
    public void GenerateReport() { }
}

// ✅ Bon : une responsabilité par classe
public class UserRepository { public void Save() { } }
public class EmailService { public void Send() { } }
public class ReportGenerator { public void Generate() { } }
```

### O — Open/Closed Principle

Ouvert à l'**extension**, fermé à la **modification**.

```csharp
public abstract class Shape
{
    public abstract double Area();
}

public class Circle : Shape
{
    public double Radius { get; set; }
    public override double Area() => Math.PI * Radius * Radius;
}
```

### L — Liskov Substitution Principle

Une sous-classe doit pouvoir **remplacer** sa classe parente sans surprise.

### I — Interface Segregation Principle

Préférer plusieurs **interfaces spécifiques** à une interface générale.

### D — Dependency Inversion Principle

Dépendre des **abstractions**, pas des implémentations.

```csharp
// ❌ Mauvais
public class UserService
{
    private readonly SqlUserRepository _repo = new();
}

// ✅ Bon
public class UserService
{
    private readonly IUserRepository _repo;
    public UserService(IUserRepository repo) => _repo = repo;
}
```

## YAGNI

**You Aren't Gonna Need It**

Ne pas anticiper des besoins hypothétiques. Implémenter quand c'est nécessaire.

## KISS

**Keep It Simple, Stupid**

La simplicité avant tout. Éviter la sur-ingénierie.

## DRY

**Don't Repeat Yourself**

Éviter la duplication de code. Factoriser les logiques communes.

> ⚠️ **Attention** : DRY ne veut pas dire sur-abstrayez. La règle de trois s'applique : dupliquez une fois, refactorisez à la troisième occurrence.