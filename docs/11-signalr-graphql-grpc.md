# 🚀 SignalR, GraphQL, gRPC

Communication temps réel et APIs avancées.

## SignalR

Communication **temps réel** entre serveur et clients.

### Avantages

- WebSockets, SSE, Long Polling (fallback automatique)
- Hubs pour broadcast
- Idéal : chat, notifications, dashboards

### Exemple

```csharp
// Hub
public class ChatHub : Hub
{
    public async Task SendMessage(string user, string message)
    {
        await Clients.All.SendAsync("ReceiveMessage", user, message);
    }
}

// Client
var connection = new HubConnectionBuilder()
    .WithUrl("/chatHub")
    .Build();

connection.On<string, string>("ReceiveMessage", (user, message) =>
{
    Console.WriteLine($"{user}: {message}");
});

await connection.StartAsync();
await connection.InvokeAsync("SendMessage", "Alice", "Bonjour !");
```

## GraphQL

Requêtes **flexibles** avec un seul endpoint.

### Avantages

- Pas de over/under-fetching
- Schéma fortement typé
- Un seul endpoint

### Exemple (HotChocolate)

```csharp
public class Query
{
    public User GetUser(int id, [Service] IUserService service)
        => service.GetUser(id);

    public IEnumerable<User> GetUsers([Service] IUserService service)
        => service.GetAllUsers();
}

builder.Services
    .AddGraphQLServer()
    .AddQueryType<Query>();
```

## gRPC

Communication **binaire** (Protobuf), très performante.

### Avantages

- Très rapide
- Streaming bidirectionnel
- Idéal microservices
- HTTP/2 obligatoire

### Exemple

```protobuf
// user.proto
service UserService {
    rpc GetUser (UserRequest) returns (UserResponse);
}

message UserRequest {
    int32 id = 1;
}

message UserResponse {
    string name = 1;
    string email = 2;
}
```

## Comparaison

| Critère | REST | GraphQL | gRPC |
|---------|:----:|:-------:|:----:|
| Format | JSON | JSON | Protobuf |
| Performance | Moyenne | Moyenne | Élevée |
| Flexibilité | Faible | Élevée | Moyenne |
| Streaming | ❌ | ⚠️ | ✅ |
| Idéal | APIs publiques | Frontend complexe | Microservices |