# 🛠️ Outils & IDE

Visual Studio, VS Code, .NET CLI, .NET Aspire.

## IDE

| Outil | Type | Usage |
|-------|------|-------|
| **Visual Studio** | IDE complet | Développement .NET |
| **VS Code** | Éditeur léger | Web, scripts, multi-langage |

## .NET CLI

```bash
# Créer un projet
dotnet new console -n MyApp
dotnet new webapi -n MyApi
dotnet new classlib -n MyLib

# Build
dotnet build --configuration Release

# Test
dotnet test

# Publish
dotnet publish -c Release -o ./publish

# EF Core
dotnet ef migrations add InitialCreate
dotnet ef database update
```

## .NET Aspire

Orchestration cloud-native pour microservices.

```csharp
var builder = DistributedApplication.CreateBuilder(args);

var cache = builder.AddRedis("cache");
var db = builder.AddSqlServer("db")
    .AddDatabase("mydb");

builder.AddProject<Projects.MyApi>("api")
    .WithReference(cache)
    .WithReference(db);

builder.Build().Run();
```

## Gestion de code source

| Outil | Type | Description |
|-------|------|-------------|
| **Git** | Distribué | Système de contrôle de version |
| **GitHub** | Plateforme | Hébergement Git + CI/CD |
| **Azure DevOps** | Plateforme | Repos, pipelines, boards |
| **SVN** | Centralisé | Ancien système |

### Commandes Git essentielles

```bash
git clone <url>
git checkout -b feature/ma-branche
git add .
git commit -m "feat: ajout section"
git push origin feature/ma-branche
git pull --rebase
```