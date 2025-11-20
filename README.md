[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/ITZAXhaH)
# 🧩 Activity: Polymorphism with Electronic Devices

## 📘 Introduction
In this activity, you will create a simple **Electronic Device Program** in C#.  
You will practice:

- Using **method overloading** (same method name, different parameters)  
- Using **method overriding** (derived class changes base class behavior)  
- Understanding **runtime polymorphism** through base class references  
- Displaying output clearly in the console  

---

## 🪜 Step 1: Create the Base Class

The base class will represent a general **Electronic Device**.

```csharp
public class ElectronicDevice
{
    public string Brand { get; set; }

    // Method Overloading: same name, different parameter lists
    public virtual void TurnOn()
    {
        Console.WriteLine("Electronic device is now ON.");
    }

    public void TurnOn(string deviceName)
    {
        Console.WriteLine($"{deviceName} is now ON.");
    }

    // Virtual method that can be overridden
    public virtual void ShowDetails()
    {
        Console.WriteLine("Showing generic electronic device details.");
    }
}
```

> 💡 **Tip:**  
> Use the `virtual` keyword to allow derived classes to override a method.

---

## 🪜 Step 2: Create the Derived Class

The derived class **Television** inherits from `ElectronicDevice` and customizes its behavior.

```csharp
public class Television : ElectronicDevice
{
    public int ScreenSize { get; set; }

    // Method Overriding: changes the behavior of the base class method
    public override void TurnOn()
    {
        Console.WriteLine("Television is now ON. Displaying startup screen...");
    }

    // Method Overloading: two versions of AdjustVolume
    public void AdjustVolume(int level)
    {
        Console.WriteLine($"Volume set to {level}.");
    }

    public void AdjustVolume(int level, bool mute)
    {
        if (mute)
            Console.WriteLine("Television is muted.");
        else
            Console.WriteLine($"Volume adjusted to {level}.");
    }

    public override void ShowDetails()
    {
        Console.WriteLine($"Television Details: Brand = {Brand}, Screen Size = {ScreenSize} inches");
    }
}
```

> 💡 **Tip:**  
> Use `override` when you want to replace a virtual method from the base class.

---

## 🪜 Step 3: Use the Classes in `Main()`

Now, let’s use both classes and demonstrate **method overloading** and **method overriding**.

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("=== Electronic Device Demo ===");

        // Base class object
        ElectronicDevice device = new ElectronicDevice();
        device.TurnOn();
        device.TurnOn("Laptop");
        device.ShowDetails();

        Console.WriteLine();

        // Derived class object
        Television tv = new Television { Brand = "Samsung", ScreenSize = 55 };
        tv.TurnOn(); // overridden method
        tv.AdjustVolume(20); // overloaded method 1
        tv.AdjustVolume(10, true); // overloaded method 2
        tv.ShowDetails();

        Console.WriteLine();

        // Polymorphism in action
        ElectronicDevice polyDevice = new Television { Brand = "Sony", ScreenSize = 65 };
        polyDevice.TurnOn();       // calls Television's overridden method
        polyDevice.ShowDetails();  // calls Television's overridden method
    }
}
```

> 🧠 **Tip:**  
> When you declare a base class variable (`ElectronicDevice`) and assign it a derived class object (`Television`),  
> the **overridden methods** of the derived class are called — this is **runtime polymorphism**.

---

## 🧾 Step 4: Sample Output

```
=== Electronic Device Demo ===
Electronic device is now ON.
Laptop is now ON.
Showing generic electronic device details.

Television is now ON. Displaying startup screen...
Volume set to 20.
Television is muted.
Television Details: Brand = Samsung, Screen Size = 55 inches

Television is now ON. Displaying startup screen...
Television Details: Brand = Sony, Screen Size = 65 inches
```

---

## 🧩 Step 5: Key Concepts Recap

| Concept | Example | Description |
|----------|----------|-------------|
| **Method Overloading** | `TurnOn()` and `TurnOn(string)` | Same method name, different parameters |
| **Method Overriding** | `Television.TurnOn()` overrides `ElectronicDevice.TurnOn()` | Derived class changes base class behavior |
| **Polymorphism** | `ElectronicDevice polyDevice = new Television();` | Calls the correct method based on object type at runtime |

---

## 🎯 **Challenge Task**

### Create a new derived class called **SmartTelevision** that inherits from `Television`.

Your `SmartTelevision` class should:

1. Add a new property: `public bool HasInternet { get; set; }`
2. Override the `TurnOn()` method to display:  
   `"Smart TV is now ON. Connecting to Wi-Fi..."`
3. Add a new overloaded method:  
   `ConnectToInternet(string networkName)` → displays: `"Connected to [networkName]"`
4. Override `ShowDetails()` to include internet capability info.
5. In `Main()`, create a `SmartTelevision` object and demonstrate all overridden and overloaded methods.

> 💪 **Bonus:** Use a base class reference like this:
> ```csharp
> ElectronicDevice smart = new SmartTelevision { Brand = "LG", ScreenSize = 65, HasInternet = true };
> smart.TurnOn(); 
> smart.ShowDetails();
> ```

---

✅ **End of Activity**  
You have successfully demonstrated **method overloading**, **method overriding**, **multi-level inheritance**, and **runtime polymorphism** in C#.
