## 🧠 Overview

> The Prototype Pattern allows you to create new objects by cloning existing ones instead of instantiating new objects from scratch.

It’s especially useful when:

- Object creation is expensive or complex.
- You want to **duplicate an object with all its nested state**.
- You need **polymorphic copies** (subclasses clone correctly).
- Your objects form a **graph** (with cycles or shared references).

---

## ⚙️ Core Idea

- Each object can **clone itself** through a `Clone()` method.
- A **dictionary** tracks cloned instances, ensuring each original object corresponds to exactly **one clone**.
- This avoids infinite recursion in circular references and preserves shared references.

---

## 🧩 Class Structure

### 1️⃣ Prototype Interface

```C#
public interface IPrototype<T>
{
    T Clone(Dictionary<object, object> clones = null);
}

```

> Defines a generic Clone() method that takes an optional dictionary for tracking.

---

### 2️⃣ Base Abstract Class — Skill

```C#
public abstract class Skill : IPrototype<Skill>
{
    public string Name { get; set; }
    public int Level { get; set; }

    public abstract Skill Clone(Dictionary<object, object> clones = null);
    public override string ToString() => $"{Name} (Level {Level})";
}

```

> Base for polymorphic cloning — allows FireballSkill and HealingSkill to define their own cloning logic.

---

### 3️⃣ Concrete Skills

```C#
public class FireballSkill : Skill
{
    public int FireDamage { get; set; }

    public override Skill Clone(Dictionary<object, object> clones = null)
    {
        if (clones == null) clones = new();
        if (clones.ContainsKey(this)) return (Skill)clones[this];

        var clone = new FireballSkill
        {
            Name = this.Name,
            Level = this.Level,
            FireDamage = this.FireDamage
        };

        clones[this] = clone;
        return clone;
    }
}

```

```C#
public class HealingSkill : Skill
{
    public int HealAmount { get; set; }

    public override Skill Clone(Dictionary<object, object> clones = null)
    {
        if (clones == null) clones = new();
        if (clones.ContainsKey(this)) return (Skill)clones[this];

        var clone = new HealingSkill
        {
            Name = this.Name,
            Level = this.Level,
            HealAmount = this.HealAmount
        };

        clones[this] = clone;
        return clone;
    }
}

```

> Each subclass clones its unique fields and registers itself in the clones dictionary.

---

### 4️⃣ Item Class (Shallow Copy Example)

```C#
public class Item : IPrototype<Item>
{
    public string Name { get; set; }
    public int Quantity { get; set; }

    public virtual Item Clone(Dictionary<object, object> clones = null)
    {
        if (clones == null) clones = new();
        if (clones.ContainsKey(this)) return (Item)clones[this];

        var clone = (Item)MemberwiseClone(); // shallow copy
        clones[this] = clone;
        return clone;
    }

    public override string ToString() => $"{Name} x{Quantity}";
}

```

> Simple objects can safely use MemberwiseClone() for shallow copying.

---

### 5️⃣ Pet (Circular Reference Example)

```C#
public class Pet : IPrototype<Pet>
{
    public string Name { get; set; }
    public Character Owner { get; set; }

    public Pet Clone(Dictionary<object, object> clones = null)
    {
        if (clones == null) clones = new();
        if (clones.ContainsKey(this)) return (Pet)clones[this];

        var clone = new Pet { Name = this.Name };
        clones[this] = clone;

        // Don't deep clone owner; will fix later
        clone.Owner = this.Owner;

        return clone;
    }

    public override string ToString() => $"Pet: {Name}, Owner: {Owner?.Name}";
}

```

> Uses the shared dictionary to avoid infinite recursion between Pet ↔ Owner.

---

### 6️⃣ Character (Full Graph Clone)

```C#
public class Character : IPrototype<Character>
{
    public string Name { get; set; }
    public List<Skill> Skills { get; set; } = new();
    public List<Item> Inventory { get; set; } = new();
    public Pet Pet { get; set; }

    public Character Clone(Dictionary<object, object> clones = null)
    {
        if (clones == null) clones = new();
        if (clones.ContainsKey(this)) return (Character)clones[this];

        var clone = new Character { Name = this.Name + " Clone" };
        clones[this] = clone;

        // Deep clone skills
        clone.Skills = new List<Skill>();
        foreach (var skill in Skills)
            clone.Skills.Add(skill.Clone(clones));

        // Shallow clone inventory
        clone.Inventory = new List<Item>();
        foreach (var item in Inventory)
            clone.Inventory.Add(item.Clone(clones));

        // Clone pet
        if (Pet != null)
        {
            clone.Pet = Pet.Clone(clones);
            clone.Pet.Owner = clone; // fix circular reference
        }

        return clone;
    }

    public void Show()
    {
        Console.WriteLine($"Character: {Name}");
        Console.WriteLine("Skills:");
        foreach (var skill in Skills) Console.WriteLine($" - {skill}");
        Console.WriteLine("Inventory:");
        foreach (var item in Inventory) Console.WriteLine($" - {item}");
        if (Pet != null)
            Console.WriteLine($"Pet: {Pet.Name} (Owner: {Pet.Owner.Name})");
        Console.WriteLine();
    }
}

```

> The Character.Clone() method demonstrates deep cloning of a nested object graph with shared and cyclic references.

---

### 7️⃣ Client Example

```C#
public class Program
{
    public static void Main()
    {
        var hero = new Character
        {
            Name = "Hero",
            Skills = new List<Skill>
            {
                new FireballSkill { Name = "Fireball", Level = 3, FireDamage = 100 },
                new HealingSkill { Name = "Heal", Level = 2, HealAmount = 50 }
            },
            Inventory = new List<Item>
            {
                new Item { Name = "Health Potion", Quantity = 5 },
                new Item { Name = "Mana Potion", Quantity = 3 }
            }
        };

        var pet = new Pet { Name = "Fluffy", Owner = hero };
        hero.Pet = pet;

        Console.WriteLine("Original:");
        hero.Show();

        var heroClone = hero.Clone();

        heroClone.Name = "Hero Clone";
        heroClone.Skills[0].Level = 5;
        heroClone.Inventory[0].Quantity = 10;
        heroClone.Pet.Name = "Fluffy Clone";

        Console.WriteLine("Clone after modification:");
        heroClone.Show();

        Console.WriteLine("Original after clone modified:");
        hero.Show();
    }
}

```

---

## 🧾 Example Output

```Plain
Original:
Character: Hero
Skills:
 - Fireball (Level 3)
 - Heal (Level 2)
Inventory:
 - Health Potion x5
 - Mana Potion x3
Pet: Fluffy (Owner: Hero)

Clone after modification:
Character: Hero Clone
Skills:
 - Fireball (Level 5)
 - Heal (Level 2)
Inventory:
 - Health Potion x10
 - Mana Potion x3
Pet: Fluffy Clone (Owner: Hero Clone)

Original after clone modified:
Character: Hero
Skills:
 - Fireball (Level 3)
 - Heal (Level 2)
Inventory:
 - Health Potion x10
 - Mana Potion x3
Pet: Fluffy (Owner: Hero)

```

---

## 🧱 Key Mechanisms

### 🧭 Dictionary `<object, object>`

|Role|Description|
|---|---|
|**Key**|Original object reference|
|**Value**|Its corresponding clone|
|**Purpose**|Prevents cloning the same instance twice and handles circular references|

---

### ⚖️ 1:1 Mapping

Each original object maps to **exactly one** clone.

This ensures:

- No duplicate clones.
- Shared references preserved.
- Circular references safely handled.

---

### 🔁 Cloning Flow (Simplified)

```Plain
Character.Clone()
 ├── adds self to dictionary
 ├── clones each Skill (deep)
 ├── clones each Item (shallow)
 └── clones Pet (deep)
      └── Pet.Owner = Character Clone (fix link)

```

---

## 🧩 Deep vs Shallow Cloning

|Type|What it copies|Example|
|---|---|---|
|**Shallow**|References only|`Item.Clone()` (shared potions)|
|**Deep**|Entire object graph|`Skill.Clone()`, `Character.Clone()`|

---

## 🧠 Memory & Performance Considerations

- Dictionary grows with number of unique objects cloned.
- Garbage-collected after cloning completes.
- Use iterative (non-recursive) cloning for very large object graphs.
- Always call `clones[this] = clone;` **before** cloning nested objects to prevent infinite recursion.

---

## 🔒 Best Practices

✅ Always register the clone early

✅ Pass the same dictionary to all nested clones

✅ Use shallow copies for shared/immutable objects

✅ Manually fix circular references

✅ Avoid recursion too deep (may cause stack overflow)

---

## 🧩 Summary

|Concept|Description|
|---|---|
|**Goal**|Create deep, consistent object copies|
|**Technique**|Recursive cloning with reference tracking|
|**Core Tool**|`Dictionary<object, object>` for 1:1 original→clone mapping|
|**Handles**|Circular refs, shared refs, polymorphism|
|**Pattern**|Prototype|

---

## 🧠 In short

> Prototype Pattern = Copying by behavior, not by construction.

You don’t “build” new objects —

you _duplicate_ existing ones, respecting structure and relationships.