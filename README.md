# 📚 Référentiel de Révision

> Consultant .NET Fullstack & Azure DevOps — Synthèse des compétences, concepts et pratiques.

![.NET](https://img.shields.io/badge/.NET-8-512BD4?logo=dotnet&logoColor=white)
![C#](https://img.shields.io/badge/C%23-13-68217A?logo=csharp&logoColor=white)
![Azure DevOps](https://img.shields.io/badge/Azure%20DevOps-CI%2FCD-0078D7?logo=azuredevops&logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL%20Server-2019-CC2927?logo=microsoftsqlserver&logoColor=white)
![Docker](https://img.shields.io/badge/Containers-Docker%20%2F%20K8s-2496ED?logo=docker&logoColor=white)

## 📋 Table des matières

- [🎯 Points clés couverts](#-points-clés-couverts)
- [1. Parcours & Expériences](#1-parcours--expériences)
- [2. C# — Langage & Fonctionnement](#2-c--langage--fonctionnement)
- [3. Nouveautés C# (v2 à v13)](#3-nouveautés-c-v2-à-v13)
- [4. Collections .NET](#4-collections-net)
- [5. LINQ & Sérialisation](#5-linq--sérialisation)
- [6. Asynchronisme & I/O](#6-asynchronisme--io)
- [7. Principes de développement](#7-principes-de-développement)
- [8. Design Patterns](#8-design-patterns)
- [9. ASP.NET & API](#9-aspnet--api)
- [10. Blazor & UI](#10-blazor--ui)
- [11. SignalR, GraphQL, gRPC](#11-signalr-graphql-grpc)
- [12. Qualité & Tests](#12-qualité--tests)
- [13. Data & Bases de données](#13-data--bases-de-données)
- [14. ORM & Accès aux données](#14-orm--accès-aux-données)
- [15. Logging & Sécurité](#15-logging--sécurité)
- [16. Performance & Profiling](#16-performance--profiling)
- [17. Architecture logicielle](#17-architecture-logicielle)
- [18. DevOps & Cloud Azure](#18-devops--cloud-azure)
- [19. Docker & Kubernetes](#19-docker--kubernetes)
- [20. Outils & IDE](#20-outils--ide)
- [21. Web (HTML, CSS, JS)](#21-web-html-css-js)
- [22. Messaging (RabbitMQ, ZeroMQ)](#22-messaging-rabbitmq-zeromq)
- [23. Méthodologies & Organisation](#23-méthodologies--organisation)
- [24. WinForms & WPF](#24-winforms--wpf)
- [25. Intelligence Artificielle](#25-intelligence-artificielle)
- [26. Anti-patterns à éviter](#26-anti-patterns-à-éviter)
- [27. Code propre qui fait la différence](#27-code-propre-qui-fait-la-différence)

---

## 🎯 Points clés couverts

✅ C#, GC/IL/JIT/AOT, records, pattern matching  
✅ Collections (List, Dictionary, HashSet, Queue, Stack...)  
✅ LINQ, JSON/XML/Protobuf/MessagePack  
✅ Async/await, Task, bonnes pratiques  
✅ SOLID, KISS, DRY, YAGNI  
✅ ASP.NET Core, MVC, Minimal API, DI, Middleware  
✅ Blazor, SignalR, GraphQL, gRPC  
✅ Tests (TDD, unitaires, intégration, E2E)  
✅ SQL Server, MySQL, Lucene, ClickHouse  
✅ ADO.NET, Dapper, EF Core, NHibernate  
✅ Logging (NLog, Serilog), sécurité (OAuth2, JWT)  
✅ Clean Architecture, DDD  
✅ Azure, CI/CD, Docker, Kubernetes  
✅ IA, prompt engineering, bonnes pratiques pro  

---

## 1. Parcours & Expériences

- **ODDO BHF** : développement .NET C#, Web API, WCF, WinForms, SQL Server, NHibernate.
- **MEDIAPOST** : consultant .NET Fullstack & Azure DevOps, API REST, SQL Server, ZeroMQ, CI/CD.

## 2. C# — Langage & Fonctionnement

- Types valeur/référence, nullables, records, propriétés modernes.
- Compréhension runtime : **GC**, **IL**, **JIT**, **AOT**.

## 3. Nouveautés C# (v2 à v13)

- **C# 2.0** : génériques, nullables.
- **C# 3.0** : LINQ, lambda, `var`.
- **C# 5.0** : `async/await`.
- **C# 8.0** : nullable reference types, async streams.
- **C# 9.0+** : records, init, améliorations pattern matching.
- **C# 12/13** : primary constructors, collection expressions, nouveautés runtime/perf.

## 4. Collections .NET

- `List<T>`, `Dictionary<K,V>`, `HashSet<T>`, `Queue<T>`, `Stack<T>`, `LinkedList<T>`.
- Choix selon complexité, accès, ordre, unicité, concurrence.

## 5. LINQ & Sérialisation

- LINQ : `Where`, `Select`, `OrderBy`, `GroupBy`, `Join`, `Any`, `All`, `First`, etc.
- Sérialisation : JSON (web), XML (interop), Protobuf/MessagePack (performance).

## 6. Asynchronisme & I/O

- `async/await`, `Task`, `Task<T>`, `ValueTask`.
- Règles : **async all the way**, éviter `.Result/.Wait()`, utiliser `CancellationToken`.

## 7. Principes de développement

- SOLID
- DRY
- KISS
- YAGNI

## 8. Design Patterns

- Créationnels : Singleton, Factory, Builder.
- Structurels : Adapter, Facade, Decorator, Proxy.
- Comportementaux : Strategy, Observer, Command, Repository, Unit of Work.

## 9. ASP.NET & API

- MVC/Web API vs Minimal API.
- Routing, Middleware pipeline, DI (Transient/Scoped/Singleton).

## 10. Blazor & UI

- Blazor Server, WebAssembly, Web App hybride (.NET 8+).

## 11. SignalR, GraphQL, gRPC

- **SignalR** : temps réel.
- **GraphQL** : requêtes flexibles.
- **gRPC** : hautes performances via Protobuf/HTTP2.

## 12. Qualité & Tests

- TDD : Red → Green → Refactor.
- Tests : unitaires, intégration, E2E.
- Outils : NUnit/xUnit, Moq, AutoFixture, couverture de code.

## 13. Data & Bases de données

- Relationnel : SQL Server, MySQL.
- Non relationnel / analytique : Lucene, ClickHouse.

## 14. ORM & Accès aux données

- ADO.NET (bas niveau)
- Dapper (micro ORM)
- EF Core (ORM complet)
- NHibernate

## 15. Logging & Sécurité

- Logging structuré : Serilog, NLog.
- Sécurité : OAuth2, JWT, Identity Server.

## 16. Performance & Profiling

- Gestion mémoire (stack/heap/LOH).
- Outils : BenchmarkDotNet, dotTrace, dotMemory, App Insights.

## 17. Architecture logicielle

- Clean Architecture.
- DDD (Entities, Value Objects, Agrégats, Domain Events).
- Structure en couches Domain/Application/Infrastructure/WebApi.

## 18. DevOps & Cloud Azure

- Azure Functions, App Insights, Web App, Service Bus, Key Vault.
- CI/CD avec Azure DevOps & GitHub Actions.

## 19. Docker & Kubernetes

- Dockerfile multi-stage.
- Docker Compose.
- Concepts K8s : Pod, Service, Deployment, Ingress.

## 20. Outils & IDE

- Visual Studio, VS Code, .NET CLI, .NET Aspire.
- Gestion de source : Git, GitHub, Azure DevOps, SVN.

## 21. Web (HTML, CSS, JS)

- HTML5 sémantique, CSS3 (Flexbox/Grid), JavaScript moderne, HTTP/HTTPS.

## 22. Messaging (RabbitMQ, ZeroMQ)

- RabbitMQ : broker AMQP.
- ZeroMQ : messaging léger hautes performances.

## 23. Méthodologies & Organisation

- Agile/Scrum : planning, daily, review, rétro.
- Code review, commits atomiques, branches structurées.

## 24. WinForms & WPF

- WinForms (desktop classique).
- WPF (XAML, MVVM).

## 25. Intelligence Artificielle

- Prompt engineering.
- Copilot/ChatGPT/Azure OpenAI pour assistance dev.
- Vérification humaine obligatoire (sécurité, qualité, licences).

## 26. Anti-patterns à éviter

- `catch (Exception) { }`
- `throw ex;`
- `.Result/.Wait()` en async
- `async void` (hors event handlers)
- SQL concaténé (injection)
- secrets dans le repo
- God classes, N+1 queries, duplication, absence de tests

## 27. Code propre qui fait la différence

- Code lisible, testable, maintenable.
- Noms explicites, méthodes courtes, responsabilités claires.
- Documentation utile (README, ADR, XML docs).
- Automatisation qualité (linters, analyzers, CI/CD).

---

## 📌 Licence

Usage personnel / préparation d'entretien.

## 👤 Auteur

Consultant .NET Fullstack & Azure DevOps.
