# Notes: Using a Constants File and static keyword in Swift

## Why Strings Are Dangerous

* Strings don't get the same error-checking support from Xcode as methods and variables.
* Typos in method names are caught by the compiler, but typos inside strings are not.
* If a segue identifier string is misspelled (e.g., wrong capitalization), the app can crash at runtime because it can't find the matching segue.

**Example Problem:**

```swift
performSegue(withIdentifier: "RegisterToChat", sender: self)
```

If the actual segue identifier is:

```swift
"registerToChat"
```

the app will crash because the identifiers don't match.

---

## Solution: Create a Constants File

### Step 1: Create a New Swift File

Create:

```swift
Constants.swift
```

### Step 2: Create a Constants Structure

```swift
struct Constants {
    static let registerSegue = "RegisterToChat"
    static let loginSegue = "LoginToChat"
}
```

### Benefits

* Avoids repeatedly typing strings.
* Reduces typo-related bugs.
* Makes code easier to maintain.
* Allows Xcode autocomplete and suggestions.

---

## Using Constants in Code

Instead of:

```swift
performSegue(withIdentifier: "RegisterToChat", sender: self)
```

Use:

```swift
performSegue(withIdentifier: Constants.registerSegue, sender: self)
```

This is safer and easier to maintain.

---

## Static Properties (Type Properties)

### Instance Property

```swift
struct MyStructure {
    let instanceProperty = "ABC"
}
```

To access it:

```swift
let myStructure = MyStructure()
print(myStructure.instanceProperty)
```

Output:

```text
ABC
```

### Type Property (Static Property)

```swift
struct MyStructure {
    static let typeProperty = "123"
}
```

To access it:

```swift
print(MyStructure.typeProperty)
```

Output:

```text
123
```

### Key Difference

| Instance Property             | Type Property              |
| ----------------------------- | -------------------------- |
| Belongs to an object instance | Belongs to the type itself |
| Requires creating an object   | No object creation needed  |
| Accessed via instance         | Accessed via type name     |

---

## Type Methods vs Instance Methods

### Instance Method

```swift
func instanceMethod() {
}
```

Call with:

```swift
let myStructure = MyStructure()
myStructure.instanceMethod()
```

### Type Method

```swift
static func typeMethod() {
}
```

Call with:

```swift
MyStructure.typeMethod()
```

### Important

* Works for both **Structs** and **Classes**.
* Type methods behave similarly to type properties.

---

## Convention: Using `K` Instead of `Constants`

Many developers shorten:

```swift
struct Constants {
}
```

to:

```swift
struct K {
}
```

Example:

```swift
K.registerSegue
K.loginSegue
```

This makes code shorter while still indicating values come from the Constants file.

---

## Adding More Constants

Example:

```swift
struct K {
    static let appName = "Flash Chat"
    static let registerSegue = "RegisterToChat"
    static let loginSegue = "LoginToChat"
}
```

Use throughout the app:

```swift
title = K.appName
```

instead of:

```swift
title = "Flash Chat"
```

---

## Advantages of Constants Files

* Centralized storage for frequently used values.
* Consistent naming across the project.
* Easier maintenance (change once, update everywhere).
* Fewer runtime crashes due to typo errors.
* Better autocomplete support from Xcode.
* Cleaner and more readable code.

---

## Testing After Refactoring

Verify that:

1. Login → Chat screen works.
2. Register → Chat screen works.
3. App title displays correctly.
4. Animations still work.
5. Segue identifiers in `Main.storyboard` exactly match those in `Constants.swift`.

---

## Key Takeaway

**Store important strings (segue identifiers, app names, etc.) in a Constants file using `static let` properties instead of hardcoding strings throughout your app. This makes your code safer, cleaner, and easier to maintain.**
