# Swift Deep Dive Notes: Protocols

## What is a Protocol?

<p align="center">
    <img src="assets/protocols.png" width="auto" style="border-radius: 1%">
</p>

A **protocol** in Swift is like a **certificate or qualification** that defines a set of requirements.

* A protocol specifies **what a type must be able to do**.
* It does **not provide the implementation**.
* Classes, structs, and enums can adopt protocols.
* Any type that adopts a protocol must implement its required methods and properties.

**Syntax:**

```swift
protocol CanFly {
    func fly()
}
```

---

## Why Do We Need Protocols?

Protocols solve problems caused by relying too much on **inheritance**.

### Example Problem

#### Bird Class

```swift
class Bird {
    func layEgg() {
        print("The bird makes a new bird in a shell")
    }

    func fly() {
        print("The bird flaps its wings and lifts off into the sky")
    }
}
```

#### Eagle Inherits from Bird

```swift
class Eagle: Bird {
    func soar() {
        print("The eagle glides using air currents")
    }
}
```

This makes sense because eagles can:

* Fly
* Lay eggs
* Soar

---

### The Penguin Problem

```swift
class Penguin: Bird {
    func swim() {
        print("The penguin paddles through the water")
    }
}
```

Because `Penguin` inherits from `Bird`, it also gets:

```swift
penguin.fly()
```

But penguins **cannot fly**.

**Issue:** Inheritance gives subclasses functionality they may not actually need.

---

## Another Problem: Airplanes

Suppose we create:

```swift
struct Airplane {
}
```

An airplane can fly, but it is **not a bird**.

If a flying museum expects a `Bird`:

```swift
func flyingDemo(flyingObject: Bird)
```

then an airplane cannot be passed in because it isn't a Bird.

### Bad Solution

Force Airplane to inherit from Bird:

```swift
class Airplane: Bird
```

Problems:

* Airplanes don't flap wings.
* Airplanes shouldn't lay eggs.
* The relationship doesn't make sense.

This is a sign that inheritance is being misused.

---

## Protocols to the Rescue

### Define a Flying Capability

```swift
protocol CanFly {
    func fly()
}
```

The protocol only declares the requirement.

Not allowed:

```swift
protocol CanFly {
    func fly() {
        // Error
    }
}
```

Protocols cannot contain method bodies.

---

## Adopting a Protocol

### Eagle

```swift
class Eagle: Bird, CanFly {

    func fly() {
        print("The eagle flaps its wings and lifts off into the sky")
    }
}
```

### Airplane

```swift
struct Airplane: CanFly {

    func fly() {
        print("The airplane uses its engine to lift off")
    }
}
```

### Penguin

```swift
class Penguin: Bird {

    func swim() {
        print("The penguin paddles through the water")
    }
}
```

Penguins do not adopt `CanFly`, so they cannot fly.

---

## Using Protocols as Types

Instead of requiring a Bird:

```swift
func flyingDemo(flyingObject: Bird)
```

Use the protocol:

```swift
func flyingDemo(flyingObject: CanFly)
```

Now the function accepts anything that can fly:

```swift
museum.flyingDemo(flyingObject: myEagle)
museum.flyingDemo(flyingObject: myPlane)
```

But not:

```swift
museum.flyingDemo(flyingObject: myPenguin)
```

because `Penguin` does not conform to `CanFly`.

---

## Benefits of Protocols

## 1. Better Separation of Responsibilities

* Flying behavior is separate from bird behavior.
* Only objects that can fly implement flying.

## 2. More Flexibility

Protocols can be adopted by:

* Classes
* Structs
* Enums

Inheritance only works with classes.

## 3. Avoids Incorrect Relationships

* Airplanes are not birds.
* Penguins are birds but cannot fly.

Protocols model capabilities rather than inheritance hierarchies.

## 4. Safer Code

If something conforms to `CanFly`, Swift guarantees it has a `fly()` method.

---

### Multiple Protocol Adoption

A type can adopt multiple protocols:

```swift
struct Airplane: CanFly, AnotherProtocol {
}
```

Separate protocols with commas.

---

### Protocols + Inheritance

For classes that inherit and adopt protocols:

```swift
class Eagle: Bird, CanFly, AnotherProtocol {
}
```

Order:

1. Superclass first (`Bird`)
2. Protocols after (`CanFly`, `AnotherProtocol`)

---

## Key Takeaways

* Protocols define **requirements**, not implementations.
* They describe **capabilities** (e.g., `CanFly`).
* Protocols help avoid problems caused by excessive inheritance.
* Classes and structs can both adopt protocols.
* Protocols can be used as data types.
* A type that adopts a protocol must implement all required methods.
* Protocols are heavily used in Swift, including delegate patterns such as `UITextFieldDelegate`.

## Analogy

**Inheritance:** *"What is this object?"*

**Protocols:** *"What can this object do?"*

Use inheritance for **is-a relationships** and protocols for **can-do capabilities**.
