---

## 🧠 What is Singleton?

- Ensures **only one instance** of a class exists.
- Provides a **global access point** to that instance.

---

## ⚙️ Implementation

```C#
public sealed class Singleton
{
    // Static readonly instance — created once when class is loaded
    private static readonly Singleton _instance = new Singleton();

    // Private constructor prevents external instantiation
    private Singleton() { }

    // Public accessor for the single instance
    public static Singleton Instance => _instance;

    // Example method
    public void DoWork()
    {
        Console.WriteLine("Singleton is working!");
    }
}

```

---

## 🧩 Usage Example

```C#
class Program
{
    static void Main()
    {
        Singleton.Instance.DoWork();
    }
}

```

---

## 💡 Key Points

|Feature|Explanation|
|---|---|
|**Private Constructor**|Prevents external instantiation|
|**Static Instance**|Single, readonly instance|
|**Thread Safety**|Guaranteed by static initialization in .NET|
|**Sealed Class**|Prevents subclassing to maintain singleton|

---

## 🧠 How It Works

- The `_instance` is **created automatically** when the class is first loaded.
- The `Instance` property simply returns that single instance.
- Since static initialization in C# is thread-safe, **no extra locking needed**.

---

## ✅ When to Use

- When you want a **single shared resource** or manager (e.g., logger, config).
- When you want to **avoid multiple costly instances**.

[[Advanced Singleton with MultiThread in C]]