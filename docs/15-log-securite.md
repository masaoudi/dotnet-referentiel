# 🔐 Log & Sécurité

NLog, Serilog, OAuth2, JWT, IdentityServer.

## Logging

### Serilog

```csharp
Log.Logger = new LoggerConfiguration()
    .WriteTo.Console()
    .WriteTo.File("logs/app.log", rollingInterval: RollingInterval.Day)
    .CreateLogger();

Log.Information("User {UserId} logged in", userId);
```

### NLog

```xml
<nlog>
  <targets>
    <target name="file" xsi:type="File" fileName="logs/app.log" />
  </targets>
  <rules>
    <logger name="*" minlevel="Info" writeTo="file" />
  </rules>
</nlog>
```

## Sécurité

### OAuth2

Protocole d'**autorisation**.

**Flux courants** :
- **Authorization Code** (web apps)
- **Client Credentials** (machine-to-machine)
- **Implicit** (déprécié)

### JWT (JSON Web Token)

Token signé : `header.payload.signature`

```csharp
// Génération
var token = new JwtSecurityToken(
    issuer: "myapp",
    audience: "myusers",
    claims: new[] { new Claim(ClaimTypes.Name, "Alice") },
    expires: DateTime.UtcNow.AddHours(1),
    signingCredentials: credentials);

// Validation
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddJwtBearer(options =>
    {
        options.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateIssuer = true,
            ValidateAudience = true,
            ValidateLifetime = true
        };
    });
```

### IdentityServer / Duende

- Centralise l'authentification
- SSO (Single Sign-On)
- Gestion des utilisateurs

## Bonnes pratiques

- **HTTPS partout**
- **Hasher les mots de passe** (bcrypt, Argon2)
- **Stockage des secrets** : Key Vault, variables d'environnement
- **Principe du moindre privilège**
- **Valider toutes les entrées**