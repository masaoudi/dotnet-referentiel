# ✨ Comment écrire un code propre qui vous différencie

Bonnes pratiques qui font la différence en entretien.

## Les principes fondamentaux

### 📖 Clarté avant intelligence

Le code doit être **facile à lire et comprendre**, pas clever ou obscur.

> **Pourquoi ?** Le code est lu 10 fois plus qu'il n'est écrit.

### 🎯 Cohérence

Suivez les **conventions existantes**. Utilisez des analyseurs (StyleCop, .NET Analyzers).

### 📛 Nommage significatif

Les noms doivent **révéler l'intention**. `userRepository` > `repo`. `CalculateTotalPrice()` > `Calc()`.

### 🔧 Une seule responsabilité

Chaque classe, méthode, module doit avoir **une seule raison de changer**.

### 🔄 DRY sans sur-abstraction

**Règle de trois** : dupliquez une fois, refactorisez à la troisième occurrence.

### 🧪 Tests d'abord ou en parallèle

Écrivez les tests **avant ou en même temps** que l'implémentation.

### 💬 Commentaires : le « pourquoi », pas le « quoi »

Le code dit **comment**. Les commentaires expliquent **pourquoi**.

### 📦 Immutabilité par défaut

Préférez les objets **immuables** (`record`, `init`, `readonly`).

## Pratiques concrètes

### Formatage

- Indentation : **4 espaces**
- Longueur de ligne : **120 caractères max**
- **File-scoped namespaces** (C# 10+)
- **Nullable activé** globalement

### var vs Type explicite

```csharp
// ✅ var quand le type est évident
var user = new User();
var users = new List<User>();

// ✅ Type explicite quand c'est plus clair
IReadOnlyList<User> users = GetUsers();
decimal total = CalculateTotal();
```

### Records et propriétés

```csharp
public record UserDto(Guid Id, string Email, string Name);

var updated = user with { Name = "New Name" };
```

## Ce qui vous différencie vraiment

### 🏆 1. Votre code parle avant vous

Un **GitHub bien tenu** vaut plus qu'un CV.

### 🏆 2. Vous écrivez des tests, pas des excuses

Un senior **écrit des tests sans qu'on le lui demande**.

### 🏆 3. Vous documentez vos décisions

**ADR**, READMEs utiles, commentaires XML.

### 🏆 4. Vous faites des code reviews constructives

Commenter le **code, pas la personne**.

### 🏆 5. Vous pensez « maintenance » avant « livraison »

« Est-ce que je comprendrai ce code dans 6 mois ? »

### 🏆 6. Vous utilisez les outils à votre disposition

Analyseurs, formatage automatique, CI/CD.

## Checklist du code propre

- [ ] Méthodes courtes (< 20 lignes)
- [ ] Noms significatifs
- [ ] Pas de duplication
- [ ] Guards clauses
- [ ] Immutabilité
- [ ] Async correct
- [ ] Gestion d'erreurs
- [ ] Tests
- [ ] Documentation
- [ ] Outils configurés
- [ ] Pas de secrets dans Git
- [ ] Code review

> 💡 « Écrivez du code comme si la personne qui va le maintenir est un psychopathe violent qui sait où vous habitez. » — *Martin Golding*

**Soyez gentil avec votre futur vous-même.**