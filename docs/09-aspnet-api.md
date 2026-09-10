# 🌐 ASP.NET & API

MVC vs Minimal API, Routing, Middleware, DI.

## MVC vs Minimal API

| Critère | MVC / Web API | Minimal API |
|---------|:-------------:|:-----------:|
| Structure | Contrôleurs | Lambdas |
| Verbeux | Plus | Moins |
| Idéal pour | Grosses apps | Microservices |
| Filtres | ✅ | ✅ |
| Conventions | ✅ | ❌ |

### Contrôleur MVC

```csharp
[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    private readonly IUserService _service;
    public UsersController(IUserService service) => _service = service;

    [HttpGet("{id}")]
    public async Task<IActionResult> Get(int id)
    {
        var user = await _service.GetUserAsync(id);
        return user == null ? NotFound() : Ok(user);
    }
}
```

### Minimal API

```csharp
var builder = WebApplication.CreateBuilder(args);
builder.Services.AddScoped<IUserService, UserService>();
var app = builder.Build();

app.MapGet("/users/{id}", async (int id, IUserService service) =>
    await service.GetUserAsync(id));

app.Run();
```

## Routing

```csharp
[Route("api/[controller]")]
[HttpGet("{id:int}")]
[HttpPost]
[HttpPut("{id}")]
[HttpDelete("{id}")]
```

## Middleware

Pipeline de traitement HTTP. Chaque middleware peut :
- Traiter la requête
- Passer au suivant (`next()`)
- Court-circuiter

```csharp
app.UseAuthentication();
app.UseAuthorization();
app.UseMiddleware<RequestLoggingMiddleware>();
app.MapControllers();
```

## Injection de dépendances

### Cycles de vie

| Cycle | Description |
|-------|-------------|
| **Transient** | Nouvelle instance à chaque demande |
| **Scoped** | Une instance par requête HTTP |
| **Singleton** | Une instance pour toute l'app |

```csharp
builder.Services.AddTransient<IEmailService, EmailService>();
builder.Services.AddScoped<IUserRepository, UserRepository>();
builder.Services.AddSingleton<IConfiguration>(config);
```