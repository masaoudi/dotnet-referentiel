# 🔄 ORM & Accès aux données

ADO.NET, Dapper, EF Core, NHibernate, Fluent Migrator.

## Comparaison

| Critère | ADO.NET | Dapper | EF Core | NHibernate |
|---------|:-------:|:------:|:-------:|:----------:|
| Niveau | Bas | Micro ORM | ORM complet | ORM complet |
| Performance | ⚡⚡⚡ | ⚡⚡⚡ | ⚡⚡ | ⚡⚡ |
| Verbeux | ✅ | ⚡ | ❌ | ❌ |
| LINQ | ❌ | ❌ | ✅ | ⚠️ |
| Migrations | ❌ | ❌ | ✅ | ⚠️ |

## ADO.NET

```csharp
using var connection = new SqlConnection(connectionString);
using var command = new SqlCommand("SELECT * FROM Users WHERE Id = @Id", connection);
command.Parameters.AddWithValue("@Id", 1);

await connection.OpenAsync();
using var reader = await command.ExecuteReaderAsync();
while (await reader.ReadAsync())
{
    var name = reader.GetString(reader.GetOrdinal("Name"));
}
```

## Dapper

```csharp
using var connection = new SqlConnection(connectionString);
var users = await connection.QueryAsync<User>(
    "SELECT * FROM Users WHERE Age > @Age",
    new { Age = 18 });
```

## Entity Framework Core

```csharp
public class AppDbContext : DbContext
{
    public DbSet<User> Users { get; set; }
}

// Requête
var adults = await _context.Users
    .Where(u => u.Age >= 18)
    .OrderBy(u => u.Name)
    .ToListAsync();

// Insertion
_context.Users.Add(new User { Name = "Alice" });
await _context.SaveChangesAsync();
```

## Fluent Migrator

```csharp
public class AddUsersTable : Migration
{
    public override void Up()
    {
        Create.Table("Users")
            .WithColumn("Id").AsInt32().PrimaryKey().Identity()
            .WithColumn("Name").AsString(100).NotNullable()
            .WithColumn("Email").AsString(255).NotNullable();
    }

    public override void Down()
    {
        Delete.Table("Users");
    }
}
```