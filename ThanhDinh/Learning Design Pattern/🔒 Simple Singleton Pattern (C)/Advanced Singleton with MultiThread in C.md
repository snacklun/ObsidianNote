# Modern Thread-Safe Singleton using `Lazy<T>`

```C#
public sealed class Singleton
{
    private readonly string data;

    // Lazy<T> ensures thread-safe lazy initialization
    private static readonly Lazy<Singleton> lazyInstance =
        new Lazy<Singleton>(() => new Singleton("default data"));

    // Private constructor prevents external instantiation
    private Singleton(string data)
    {
        this.data = data;
    }

    public static Singleton Instance => lazyInstance.Value;

    public string GetData() => data;
}

```

---

# Explanation (Notion Style)

### 1. `Lazy<T>` handles:

- **Thread-safe lazy initialization** by default.
- Ensures the Singleton is created **only when accessed first time**.
- No need to write explicit `lock` or `volatile`.

---

### 2. Private constructor

- Prevents outside classes from creating new instances.
- Guarantees only one instance ever exists.

---

### 3. Accessing the singleton

```C#
Singleton s = Singleton.Instance;

```

- Access triggers lazy creation if it hasn't happened yet.
- Always returns the **same instance** afterward.

---

### 4. Benefits over double-checked locking:

|Traditional Double-Checked Locking|`Lazy<T>` Approach|
|---|---|
|Requires explicit `volatile` and `lock`|Built-in thread safety, no explicit locks|
|More verbose and error-prone|Simple, concise, and less boilerplate code|
|Risk of subtle threading bugs if misused|Handles threading issues internally|

---

### 5. Optional `LazyThreadSafetyMode`

You can control the thread-safety behavior if needed:

```C#
new Lazy<Singleton>(() => new Singleton("data"), LazyThreadSafetyMode.ExecutionAndPublication);

```

---

# TL;DR

- Use `**Lazy<T>**` for the simplest, cleanest, and safest Singleton pattern in C#.
- No need to manage synchronization manually.
- Code is easier to read, maintain, and less error-prone.