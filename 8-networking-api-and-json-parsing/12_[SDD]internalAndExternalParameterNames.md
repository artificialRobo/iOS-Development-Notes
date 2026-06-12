## Swift Deep Dive Notes: Parameter Names 

### Why Parameter Names Matter in Swift

* Swift emphasizes **clear and readable code** through well-named parameters.
* Unlike **Objective-C**, which often used very long method names to describe functionality, Swift relies on parameter names to make code self-explanatory.

---

### Internal vs External Parameter Names

Swift functions can have **two different names** for a parameter:

1. **External Parameter Name**

   * Used when calling the function.
   * Makes function calls more readable.

2. **Internal Parameter Name**

   * Used inside the function body.
   * Refers to the parameter value during implementation.

<p align="center">
    <img src="assets/internalAndExternalParameter.png" width="auto" style="border-radius: 1%">
</p>

**Example Concept:**

```swift
func greet(personName name: String) {
    print(name)
}
```

Calling the function:

```swift
greet(personName: "John Doe")
```

* `personName` → External name (used when calling).
* `name` → Internal name (used inside the function).

---

### Omitting External Parameter Names

* If you don't want callers to use an external parameter name, replace it with an underscore (`_`).

**Example Concept:**

```swift
func greet(_ name: String) {
    print(name)
}
```

Calling the function:

```swift
greet("John Doe")
```

* No external parameter name is required.
* The internal name (`name`) is still available inside the function.

---

### Key Takeaways

* Swift supports **separate internal and external parameter names**.
* External names improve readability at the call site.
* Internal names are used within the function implementation.
* Using `_` removes the external parameter name, allowing values to be passed directly.
* This feature is central to Swift's goal of creating clear and expressive APIs.
