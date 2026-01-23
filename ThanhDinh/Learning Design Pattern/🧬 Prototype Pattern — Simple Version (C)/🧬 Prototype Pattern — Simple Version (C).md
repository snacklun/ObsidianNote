---

## 🧠 Overview

> The Prototype Pattern allows you to create a copy of an existing object instead of instantiating it from scratch.

Used when:

- You need many similar objects.
- Object creation is expensive.
- You want to avoid using `new` repeatedly.

---

## ⚙️ Structure

```Plain
IPrototype<T>  →  Interface defining Clone()
ConcretePrototype → Implements Clone() to return a copy
Client → Uses Clone() instead of new

```

---

## 🧩 Example — Simple Enemy Prototype

```C#
public interface IPrototype<T>
{
    T Clone();
}

public class Enemy : IPrototype<Enemy>
{
    public string Name { get; set; }
    public int Health { get; set; }
    public int Damage { get; set; }

    public Enemy Clone()
    {
        // Simple field-by-field copy
        return new Enemy
        {
            Name = this.Name,
            Health = this.Health,
            Damage = this.Damage
        };
    }

    public override string ToString()
        => $"{Name} (HP: {Health}, DMG: {Damage})";
}

```

---

### 🧑‍💻 Client Code

```C#
public class Program
{
    public static void Main()
    {
        // Create original object
        var goblin = new Enemy
        {
            Name = "Goblin",
            Health = 100,
            Damage = 15
        };

        // Clone the prototype
        var goblinClone = goblin.Clone();
        goblinClone.Name = "Goblin Warrior";
        goblinClone.Damage = 25;

        Console.WriteLine("Original: " + goblin);
        Console.WriteLine("Clone: " + goblinClone);
    }
}

```

---

### 🧾 Output

```Plain
Original: Goblin (HP: 100, DMG: 15)
Clone: Goblin Warrior (HP: 100, DMG: 25)

```

---

## 💡 Key Points

|Concept|Description|
|---|---|
|**Clone()**|Creates a new object with the same values|
|**No dictionary**|Because there are no nested or circular references|
|**Fast creation**|Useful for making variations of a base object|
|**Shallow copy**|Works for simple fields like strings, numbers, etc.|

---

## 🧱 When to Use This Simple Version

✅ Objects are small and simple

✅ No nested reference types that need deep copying

✅ You want to avoid expensive construction logic

---

## 🔍 When You’ll Need the “Advanced” Version

If you later add:

- Complex nested objects (e.g. Pet, Weapon)
- Shared references
- Circular links

then you’ll upgrade this simple version into the **advanced prototype** with a `Dictionary<object, object>` to track clones.

---

### 🧠 TL;DR

> Use the simple prototype when your object is flat (just values).
> 
> Use the advanced prototype when your object is _deep_ (nested or linked).

[[🧬 Advanced Prototype Pattern — C Deep Dive]]