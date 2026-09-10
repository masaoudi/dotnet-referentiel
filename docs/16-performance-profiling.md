# 📊 Performance & Profiling

GC, Span, profiling.

## Maîtrise de la mémoire

| Zone | Description |
|------|-------------|
| **Stack** | Types valeur, allocation rapide |
| **Heap** | Types référence, géré par GC |
| **LOH** | Large Object Heap (> 85 Ko) |

### Span<T> et Memory<T>

```csharp
// Sans allocation
ReadOnlySpan<char> span = "Hello".AsSpan();
var slice = span[1..4];

// Sur un tableau
Span<int> numbers = stackalloc int[10];
```

### ArrayPool<T>

```csharp
var pool = ArrayPool<byte>.Shared;
var buffer = pool.Rent(1024);
try
{
    // Utiliser buffer
}
finally
{
    pool.Return(buffer);
}
```

## Outils de profiling

| Outil | Usage |
|-------|-------|
| **Visual Studio Diagnostic Tools** | CPU, mémoire |
| **dotMemory** (JetBrains) | Analyse mémoire |
| **dotTrace** | Profiler performance |
| **BenchmarkDotNet** | Micro-benchmarks |
| **Application Insights** | Monitoring production |

### BenchmarkDotNet

```csharp
[MemoryDiagnoser]
public class StringBenchmark
{
    [Benchmark]
    public string Concat() => "a" + "b" + "c";

    [Benchmark]
    public string Builder()
    {
        var sb = new StringBuilder();
        sb.Append("a").Append("b").Append("c");
        return sb.ToString();
    }
}
```