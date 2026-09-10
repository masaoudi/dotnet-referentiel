# 🖥️ Blazor & UI

Server, WASM, Web App.

## Modes de rendu

| Mode | Exécution | Avantages | Inconvénients |
|------|-----------|-----------|---------------|
| **Blazor Server** | Côté serveur | Démarrage rapide | Connexion permanente |
| **Blazor WASM** | Navigateur | Offline, rapide après chargement | Téléchargement lourd |
| **Blazor Web App** (.NET 8+) | Hybride | Flexibilité | Plus complexe |

## Composant de base

```razor
@page "/counter"
@rendermode InteractiveServer

<h1>Compteur</h1>
<p>Valeur : @count</p>
<button class="btn btn-primary" @onclick="Increment">+</button>

@code {
    private int count = 0;
    private void Increment() => count++;
}
```

## Cycle de vie

| Méthode | Description |
|---------|-------------|
| `OnInitialized` | Après initialisation |
| `OnInitializedAsync` | Version async |
| `OnParametersSet` | Après réception des paramètres |
| `OnAfterRender` | Après rendu |
| `Dispose` | Nettoyage |

## Data binding

```razor
<input @bind="name" />
<p>Bonjour @name</p>

<input @bind="age" @bind:event="oninput" />

@code {
    private string name = "";
    private int age = 0;
}
```

## Composants

```razor
<!-- UserCard.razor -->
<div class="card">
    <h3>@User.Name</h3>
    <p>@User.Email</p>
</div>

@code {
    [Parameter] public User User { get; set; } = default!;
}

<!-- Utilisation -->
<UserCard User="@currentUser" />
```