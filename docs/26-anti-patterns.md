# Anti-patterns courants en .NET

Ce guide répertorie les pièges à éviter lors du développement d'applications .NET modernes.

## 1. L'utilisation excessive de `async void`
- **Problème** : `async void` ne permet pas de remonter les exceptions au bloc appelant, ce qui peut faire crasher l'application entière.
- **Solution** : Utiliser `async Task` pour toutes les méthodes asynchrones, sauf pour les gestionnaires d'événements (event handlers).

## 2. Ignorer la gestion des tokens d'annulation (`CancellationToken`)
- **Problème** : Les requêtes HTTP ou requêtes en base de données continuent de tourner même si l'utilisateur annule l'action.
- **Solution** : Propager le `CancellationToken` dans toutes les méthodes asynchrones.
