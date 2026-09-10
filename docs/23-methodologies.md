# 📋 Méthodologies & Organisation

Agile, Scrum, Git.

## Agile / Scrum

### Rituels

| Rituel | Description | Durée |
|--------|-------------|-------|
| **Sprint Planning** | Planification du sprint | 2-4h |
| **Daily Meeting** | Synchronisation | 15 min |
| **Brainstorming** | Réflexion collective | Variable |
| **Sprint Review** | Démonstration | 1-2h |
| **Retrospective** | Amélioration continue | 1-2h |

### Rôles

- **Product Owner** : priorités, backlog
- **Scrum Master** : facilitation, obstacles
- **Équipe de développement** : réalisation

## Git — Bonnes pratiques

### Branches

```
main         ← Production
develop      ← Intégration
feature/*    ← Nouvelles fonctionnalités
hotfix/*     ← Corrections urgentes
release/*    ← Préparation release
```

### Workflow

```bash
# Créer une branche
git checkout -b feature/ma-fonctionnalite

# Travailler
git add .
git commit -m "feat: ajout fonctionnalité"

# Mettre à jour
git checkout develop
git pull
git checkout feature/ma-fonctionnalite
git rebase develop

# Merger
git checkout develop
git merge feature/ma-fonctionnalite
git push
```

### Messages de commit

| Préfixe | Usage |
|---------|-------|
| `feat:` | Nouvelle fonctionnalité |
| `fix:` | Correction |
| `docs:` | Documentation |
| `style:` | Formatage |
| `refactor:` | Réorganisation |
| `test:` | Tests |
| `chore:` | Maintenance |

## Code Review

### Bonnes pratiques

- **Commenter le code, pas la personne**
- Proposer des améliorations, pas des critiques
- Vérifier : logique, tests, performance, sécurité
- Automatiser le style (lint)