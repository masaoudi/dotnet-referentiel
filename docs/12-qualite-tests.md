# ✅ Qualité & Tests

TDD, unitaire, intégration, E2E, NUnit, Moq, AutoFixture.

## TDD (Test-Driven Development)

### Cycle Red-Green-Refactor

1. **Red** : écrire un test qui échoue
2. **Green** : écrire le code minimal pour passer
3. **Refactor** : améliorer le code

## Types de tests

| Type | Portée | Outils |
|------|--------|--------|
| **Unitaire** | Une méthode/classe | NUnit, xUnit, MSTest |
| **Intégration** | Plusieurs composants | WebApplicationFactory, Testcontainers |
| **E2E** | Parcours complet | Playwright, Selenium |

## Outils

### NUnit

```csharp
[TestFixture]
public class UserServiceTests
{
    [Test]
    public void Add_TwoNumbers_ReturnsSum()
    {
        var result = 1 + 2;
        Assert.That(result, Is.EqualTo(3));
    }
}
```

### Moq

```csharp
var mockRepo = new Mock<IUserRepository>();
mockRepo.Setup(r => r.GetByIdAsync(1))
        .ReturnsAsync(new User { Id = 1, Name = "Alice" });

var service = new UserService(mockRepo.Object);
```

### AutoFixture

```csharp
var fixture = new Fixture();
var user = fixture.Create<User>();
```

## Pattern AAA

```csharp
[Test]
public async Task GetUserAsync_ExistingId_ReturnsUser()
{
    // Arrange
    var mockRepo = new Mock<IUserRepository>();
    mockRepo.Setup(r => r.GetByIdAsync(1))
            .ReturnsAsync(new User { Id = 1, Name = "Alice" });
    var service = new UserService(mockRepo.Object);

    // Act
    var result = await service.GetUserAsync(1);

    // Assert
    Assert.That(result, Is.Not.Null);
    Assert.That(result.Name, Is.EqualTo("Alice"));
}
```

## Code Coverage

- **Objectif** : 70-80%
- **Outils** : Coverlet, dotCover
- **Attention** : 100% de couverture ≠ 0 bug