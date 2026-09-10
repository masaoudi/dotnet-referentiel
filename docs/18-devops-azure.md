# ☁️ DevOps & Cloud Azure

CI/CD, Azure Services.

## Azure Services

| Service | Description | Cas d'usage |
|---------|-------------|-------------|
| **Azure Functions** | Serverless | Traitements événementiels |
| **Application Insights** | Monitoring | Traces, métriques |
| **WebApp** | Hébergement web | API, sites |
| **Service Bus** | Messaging | Files, topics |
| **Key Vault** | Gestion de secrets | Clés, certificats |

## CI/CD

### Azure DevOps

```yaml
trigger:
  - main

pool:
  vmImage: 'ubuntu-latest'

steps:
  - task: UseDotNet@2
    inputs:
      version: '8.x'
  - script: dotnet build --configuration Release
    displayName: 'Build'
  - script: dotnet test --no-build
    displayName: 'Tests'
  - task: AzureWebApp@1
    inputs:
      azureSubscription: 'MySubscription'
      appName: 'MyApp'
```

### GitHub Actions

```yaml
name: CI/CD

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '8.x'
      - run: dotnet build --configuration Release
      - run: dotnet test --no-build
```