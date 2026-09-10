# 📨 Messaging

RabbitMQ, ZeroMQ.

## RabbitMQ

**Broker de messages AMQP**.

### Concepts

| Concept | Description |
|---------|-------------|
| **Producer** | Envoie des messages |
| **Consumer** | Reçoit des messages |
| **Queue** | File d'attente |
| **Exchange** | Routeur de messages |

### Patterns

- **Pub/Sub** : diffusion à plusieurs consumers
- **Routing** : routage par clé
- **Topics** : routage par pattern

### Exemple .NET

```csharp
var factory = new ConnectionFactory { HostName = "localhost" };
using var connection = factory.CreateConnection();
using var channel = connection.CreateModel();

channel.QueueDeclare("hello", false, false, false, null);
var body = Encoding.UTF8.GetBytes("Hello World!");
channel.BasicPublish("", "hello", null, body);
```

## ZeroMQ (ZMQ)

**Bibliothèque de messaging léger** sans broker central.

### Avantages

- Pas de broker
- Très performant
- Patterns variés

### Patterns

| Pattern | Usage |
|---------|-------|
| **Request/Reply** | Client-serveur |
| **Pub/Sub** | Diffusion |
| **Push/Pull** | Pipeline |

### Exemple

```csharp
using var publisher = new PublisherSocket();
publisher.Bind("tcp://*:5555");

using var subscriber = new SubscriberSocket();
subscriber.Connect("tcp://localhost:5555");
subscriber.Subscribe("topic");
```

## Comparaison

| Critère | RabbitMQ | ZeroMQ |
|---------|:--------:|:------:|
| Broker | ✅ | ❌ |
| Performance | Moyenne | Élevée |
| Fiabilité | Élevée | Moyenne |
| Cas d'usage | Découplage | Temps réel |