# 🌍 Web (HTML, CSS, JS)

Fondamentaux web.

## HTML5

### Structure sémantique

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Mon site</title>
</head>
<body>
    <header>
        <nav>
            <ul>
                <li><a href="/">Accueil</a></li>
            </ul>
        </nav>
    </header>
    <main>
        <section>
            <h1>Titre</h1>
            <p>Contenu</p>
        </section>
    </main>
    <footer>
        <p>© 2026</p>
    </footer>
</body>
</html>
```

## CSS3

### Flexbox

```css
.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 1rem;
}
```

### Grid

```css
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 1rem;
}
```

### Variables

```css
:root {
    --primary: #512bd4;
    --text: #2b2d42;
}

.button {
    background: var(--primary);
    color: var(--text);
}
```

## JavaScript

### ES6+

```javascript
// let / const
const name = "Alice";
let age = 25;

// Arrow functions
const add = (a, b) => a + b;

// Promises
fetch('/api/users')
    .then(res => res.json())
    .then(data => console.log(data));

// async/await
async function getUsers() {
    const res = await fetch('/api/users');
    return await res.json();
}

// Destructuring
const { name, age } = user;

// Spread
const newArray = [...oldArray, 4, 5];
```

## HTTP

### Méthodes

| Méthode | Usage |
|---------|-------|
| **GET** | Récupérer |
| **POST** | Créer |
| **PUT** | Remplacer |
| **PATCH** | Modifier partiellement |
| **DELETE** | Supprimer |

### Codes de statut

| Code | Signification |
|------|---------------|
| **200** | OK |
| **201** | Created |
| **400** | Bad Request |
| **401** | Unauthorized |
| **403** | Forbidden |
| **404** | Not Found |
| **500** | Internal Server Error |