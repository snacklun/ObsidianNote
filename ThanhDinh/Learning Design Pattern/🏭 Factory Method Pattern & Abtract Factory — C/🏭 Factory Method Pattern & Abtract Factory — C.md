---

## 🧠 Overview

> The Factory Method Pattern defines an interface for creating an object,
> 
> but lets **subclasses decide** which class to instantiate.

You use it when:

- You want to delegate object creation to subclasses.
- You want to follow **Open/Closed Principle** — add new product types without touching existing code.
- You want to remove `if/else` logic from client code.

---

# ⚙️ 🧩 Simple Factory Method Example

---

### 🎯 Problem

We want to create **different types of enemies**,

but avoid big `if/else` statements in the game logic.

---

## 👾 Step 1 — Product Interface

```C#
public interface IEnemy
{
    void Attack();
}

```

---

## 👹 Step 2 — Concrete Products

```C#
public class Orc : IEnemy
{
    public void Attack() => Console.WriteLine("Orc slashes with axe!");
}

public class Goblin : IEnemy
{
    public void Attack() => Console.WriteLine("Goblin throws a rock!");
}

```

---

## 🏭 Step 3 — Creator (Factory Base Class)

```C#
public abstract class EnemySpawner
{
    // Factory Method
    public abstract IEnemy CreateEnemy();

    public void SpawnEnemy()
    {
        var enemy = CreateEnemy();
        Console.WriteLine("Spawning enemy...");
        enemy.Attack();
    }
}

```

> The CreateEnemy() is the factory method — subclasses decide which concrete enemy to produce.

---

## 🧙 Step 4 — Concrete Factories

```C#
public class OrcSpawner : EnemySpawner
{
    public override IEnemy CreateEnemy() => new Orc();
}

public class GoblinSpawner : EnemySpawner
{
    public override IEnemy CreateEnemy() => new Goblin();
}

```

---

## 🧑‍💻 Step 5 — Client Code

```C#
public class Program
{
    public static void Main()
    {
        EnemySpawner orcSpawner = new OrcSpawner();
        EnemySpawner goblinSpawner = new GoblinSpawner();

        orcSpawner.SpawnEnemy();
        goblinSpawner.SpawnEnemy();
    }
}

```

---

## 🧾 Output

```Plain
Spawning enemy...
Orc slashes with axe!
Spawning enemy...
Goblin throws a rock!

```

---

## 💡 Key Points

|Concept|Description|
|---|---|
|**Factory Method**|Abstract method for object creation|
|**Subclass responsibility**|Each subclass decides which object to create|
|**Extensible**|Add new types by subclassing — no `if/else`|
|**Open/Closed Principle**|Add new creators without modifying existing code|

---

## 🧩 Overview

> The Factory Pattern family helps you create objects without exposing the creation logic to the client.

There are two main levels of complexity:

|Type|Description|
|---|---|
|**Simple Factory / Factory Method**|Creates objects from one family (single type)|
|**Abstract Factory**|Creates related objects (families of types) consistently🧩 Example — Simple Weapon Factor|

[[🧱 Complex Factory — Abstract Factory Pattern]]