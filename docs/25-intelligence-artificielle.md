# 🤖 Intelligence Artificielle

Prompt engineering, outils, bonnes pratiques.

> ⚠️ **Important** : L'IA est un **assistant**, pas un cerveau. Elle aide à trouver des informations, à générer du code boilerplate, à explorer des pistes — mais la réflexion, la validation et la décision restent **humaines**.

## Prompt Engineering

### Principes d'un bon prompt

| Principe | Description |
|----------|-------------|
| **Contexte** | Langage, framework, version, contraintes |
| **Rôle** | « Tu es un expert .NET… » |
| **Format** | Code, tableau, JSON… |
| **Exemples** | Few-shot prompting |
| **Itération** | Affiner selon les résultats |
| **Chain-of-Thought** | Raisonnement étape par étape |

### Exemple de prompt

```
Tu es un expert .NET 8.
Génère un service C# pour gérer les utilisateurs avec :
- Interface IUserService
- Implémentation UserService
- Méthodes : GetByIdAsync, CreateAsync, UpdateAsync, DeleteAsync
- Utilisation de EF Core avec DbContext
- Gestion des erreurs avec Result pattern
- Tests unitaires NUnit + Moq
Format : code C# commenté en français.
```

## Outils IA

| Outil | Usage |
|-------|-------|
| **GitHub Copilot** | Assistant de code dans l'IDE |
| **ChatGPT / Claude** | Conception, documentation |
| **Azure OpenAI** | Intégration dans les applications |
| **Copilot VS** | Intégré à Visual Studio |

## Cas d'usage en développement

| Cas | Description | Gain |
|-----|-------------|------|
| **Génération de code** | Boilerplate, DTOs, tests | Temps |
| **Explication de code** | Comprendre du legacy | Compréhension |
| **Refactoring** | Améliorer la structure | Qualité |
| **Débogage** | Analyser des erreurs | Efficacité |
| **Documentation** | Commentaires XML, README | Maintenance |
| **Tests** | Générer des tests unitaires | Couverture |

## Bonnes pratiques & limites

### ⚠️ Points de vigilance

- **Vérifier** systématiquement le code généré (sécurité, performance, licence)
- **Ne pas exposer** de données confidentielles dans les prompts
- **Comprendre** le code avant de l'intégrer
- **L'IA peut halluciner** : API inexistantes, bibliothèques obsolètes
- **Respecter la propriété intellectuelle** et les licences