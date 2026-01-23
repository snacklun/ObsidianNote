---

## 🧠 Concept

> The Abstract Factory Pattern provides an interface for creating families of related objects without specifying their concrete classes.

---

### 🎯 Goal

- Group object creation into _families_ (e.g., electric vs gasoline cars)
- Ensure that products created together are **compatible**

---

## 🧩 Example — Car Factory System

---

### 🚗 Product Interfaces

```C#
public interface IEngine
{
    void Start();
}

public interface ITire
{
    void Inflate();
}

```

---

### ⚡ Electric Family (Concrete Products)

```C#
public class ElectricEngine : IEngine
{
    public void Start() => Console.WriteLine("Starting electric engine...");
}

public class ElectricTire : ITire
{
    public void Inflate() => Console.WriteLine("Inflating electric tires...");
}

```

---

### ⛽ Gasoline Family (Concrete Products)

```C#
public class GasolineEngine : IEngine
{
    public void Start() => Console.WriteLine("Starting gasoline engine...");
}

public class GasolineTire : ITire
{
    public void Inflate() => Console.WriteLine("Inflating gasoline tires...");
}

```

---

### 🏭 Abstract Factory Interface

```C#
public interface ICarFactory
{
    IEngine CreateEngine();
    ITire CreateTire();
}

```

---

### ⚡ Electric Factory

```C#
public class ElectricCarFactory : ICarFactory
{
    public IEngine CreateEngine() => new ElectricEngine();
    public ITire CreateTire() => new ElectricTire();
}

```

---

### ⛽ Gasoline Factory

```C#
public class GasolineCarFactory : ICarFactory
{
    public IEngine CreateEngine() => new GasolineEngine();
    public ITire CreateTire() => new GasolineTire();
}

```

---

### 👨‍🔧 Client Code

```C#
public class CarAssembler
{
    private readonly IEngine _engine;
    private readonly ITire _tire;

    public CarAssembler(ICarFactory factory)
    {
        _engine = factory.CreateEngine();
        _tire = factory.CreateTire();
    }

    public void Build()
    {
        _engine.Start();
        _tire.Inflate();
    }
}

public class Program
{
    public static void Main()
    {
        ICarFactory factory = new ElectricCarFactory();
        var car = new CarAssembler(factory);
        car.Build();

        factory = new GasolineCarFactory();
        var car2 = new CarAssembler(factory);
        car2.Build();
    }
}

```

---

### 🧾 Output

```Plain
Starting electric engine...
Inflating electric tires...
Starting gasoline engine...
Inflating gasoline tires...

```

---

## 💡 Key Points

|Concept|Description|
|---|---|
|**Abstract Factory**|Groups related products (engines, tires)|
|**Families of products**|Electric family vs Gasoline family|
|**Extensible**|Add new families easily (e.g., HybridCarFactory)|
|**Scalable**|Ensures compatibility among products|
|**Downside**|More classes and complexity|

---

## 🧩 Comparison

|Aspect|Simple Factory|Abstract Factory|
|---|---|---|
|**Purpose**|Create one object|Create related family of objects|
|**Complexity**|Low|High|
|**Number of Products**|1|Multiple related|
|**Extensibility**|Modify switch|Add new factory class|
|**Use Case**|Small apps, few types|Large systems, consistent families|

---

## ⚙️ Real-World Analogy

|Type|Analogy|
|---|---|
|**Simple Factory**|Ordering a pizza — you ask for one type (Margherita or Pepperoni).|
|**Abstract Factory**|Building a car — you need matching engine + tires + body type.|

---

## 🧠 TL;DR

> 🧩 Simple Factory: One object creator (lightweight, easy).🏭 Abstract Factory: Creates multiple related objects, enforces family consistency.