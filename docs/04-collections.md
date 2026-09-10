# 📦 Collections .NET

List, Dictionary, HashSet, Queue, Stack, LinkedList + différences.

## Collections génériques

| Collection | Description | Accès | Cas d'usage |
|------------|-------------|:-----:|-------------|
| `List<T>` | Tableau dynamique | Index O(1) | Collection ordonnée |
| `Dictionary<K,V>` | Table clé-valeur | Clé O(1) | Recherche rapide |
| `HashSet<T>` | Ensemble sans doublons | O(1) | Opérations ensemblistes |
| `Queue<T>` | File FIFO | Enqueue/Dequeue O(1) | Traitement ordonné |
| `Stack<T>` | Pile LIFO | Push/Pop O(1) | Annulation, parcours |
| `LinkedList<T>` | Liste doublement chaînée | O(n) index, O(1) insertion | Insertions fréquentes |
| `SortedList<K,V>` | Dictionnaire trié | O(log n) | Données triées |
| `SortedSet<T>` | Ensemble trié | O(log n) | Ensemble ordonné |
| `ConcurrentDictionary<K,V>` | Dictionnaire thread-safe | O(1) | Multi-thread |

## Différences clés

### List vs LinkedList

| Critère | `List<T>` | `LinkedList<T>` |
|---------|:---------:|:---------------:|
| Accès indexé | ✅ O(1) | ❌ O(n) |
| Insertion milieu | ❌ O(n) | ✅ O(1) |
| Mémoire | Compacte | Fragmentée |
| Cas d'usage | Accès fréquent | Insertions fréquentes |

### Dictionary vs HashSet

| Critère | `Dictionary<K,V>` | `HashSet<T>` |
|---------|:-----------------:|:------------:|
| Stocke | Clé → Valeur | Valeurs uniques |
| Lookup | Par clé | Par valeur |
| Cas d'usage | Mapping | Test d'appartenance |

### Queue vs Stack

| Critère | `Queue<T>` | `Stack<T>` |
|---------|:----------:|:----------:|
| Ordre | FIFO | LIFO |
| Ajout | `Enqueue` | `Push` |
| Retrait | `Dequeue` | `Pop` |
| Analogie | File d'attente | Pile d'assiettes |

### Array vs List

| Critère | `T[]` | `List<T>` |
|---------|:-----:|:---------:|
| Taille | Fixe | Dynamique |
| Performance | ⚡ Meilleure | Légèrement moins |
| Flexibilité | ❌ | ✅ |
| Cas d'usage | Taille connue | Taille variable |

## Exemples

```csharp
// List
var list = new List<int> { 1, 2, 3 };
list.Add(4);

// Dictionary
var dict = new Dictionary<string, int> { ["a"] = 1, ["b"] = 2 };
if (dict.TryGetValue("a", out var value))
    Console.WriteLine(value);

// HashSet
var set = new HashSet<int> { 1, 2, 3 };
set.Add(4);

// Queue
var queue = new Queue<string>();
queue.Enqueue("premier");
var first = queue.Dequeue();

// Stack
var stack = new Stack<string>();
stack.Push("dernier");
var last = stack.Pop();

// LinkedList
var linked = new LinkedList<int>();
linked.AddFirst(1);
linked.AddLast(2);

// LINQ sur collections
var evens = list.Where(x => x % 2 == 0).ToList();
var sorted = dict.OrderBy(kv => kv.Value).ToList();
```