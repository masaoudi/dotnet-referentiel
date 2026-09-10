# 🐳 Docker & Kubernetes

Conteneurisation et orchestration.

## Docker

### Concepts

| Concept | Description |
|---------|-------------|
| **Image** | Modèle immuable |
| **Container** | Instance d'image |
| **Dockerfile** | Recette de construction |
| **Docker Compose** | Orchestration multi-containers |
| **Registry** | Dépôt d'images |

### Dockerfile .NET

```dockerfile
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY *.csproj .
RUN dotnet restore
COPY . .
RUN dotnet publish -c Release -o /app

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app .
EXPOSE 80
ENTRYPOINT ["dotnet", "MyApp.dll"]
```

### Docker Compose

```yaml
version: '3.8'
services:
  api:
    build: .
    ports:
      - "5000:80"
    depends_on:
      - db
  db:
    image: mcr.microsoft.com/mssql/server:2019-latest
    environment:
      SA_PASSWORD: "YourPassword123!"
      ACCEPT_EULA: "Y"
```

## Kubernetes

### Concepts

| Concept | Description |
|---------|-------------|
| **Pod** | Plus petite unité déployable |
| **Service** | Exposition réseau |
| **Deployment** | Gestion des replicas |
| **Ingress** | Routage HTTP |
| **ConfigMap / Secret** | Configuration |
| **Namespace** | Isolation logique |

### Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: myregistry/my-app:latest
        ports:
        - containerPort: 80
```