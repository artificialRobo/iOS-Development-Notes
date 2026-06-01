## Notes: Handling Egg Hardness Selection in Swift

### 1. Using `if-else` Statements

A simple way to determine the cooking time is by checking the selected button title (`hardness`).

```swift
if hardness == "Soft" {
    print(softTime)
} else if hardness == "Medium" {
    print(mediumTime)
} else {
    print(hardTime)
}
```

* `"Soft"`, `"Medium"`, and `"Hard"` correspond to button titles.
* The final `else` handles the remaining case (`Hard`).

---

### 2. Using a `switch` Statement

A cleaner alternative is to use a `switch`.

```swift
switch hardness {
case "Soft":
    print(softTime)
case "Medium":
    print(mediumTime)
default:
    print(hardTime)
}
```

#### More Explicit Version

```swift
switch hardness {
case "Soft":
    print(softTime)
case "Medium":
    print(mediumTime)
case "Hard":
    print(hardTime)
default:
    print("Error")
}
```

* `default` catches unexpected values.
* Useful if an unknown button somehow triggers the action.

---

### 3. Using a Dictionary (Shorter Solution)

Instead of storing separate constants (`softTime`, `mediumTime`, `hardTime`), use a dictionary.

```swift
let eggTimes = [
    "Soft": 5,
    "Medium": 7,
    "Hard": 12
]
```

#### Dictionary Structure

A dictionary stores:

* **Key** → identifier (e.g., `"Soft"`)
* **Value** → associated data (e.g., `5`)

Example:

| Key    | Value |
| ------ | ----- |
| Soft   | 5     |
| Medium | 7     |
| Hard   | 12    |

---

### 4. Challenge

Replace the `if-else` or `switch` statement by:

1. Getting the selected button title (`hardness`).
2. Looking up the corresponding value in `eggTimes`.
3. Printing the retrieved cooking time.

This requires understanding:

* **Swift Dictionaries**
* **Optionals** (dictionary lookups return optional values)

---

## Key Takeaways

* `if-else` and `switch` can both handle multiple conditions.
* `switch` often provides cleaner code.
* Dictionaries allow related data to be stored in one collection.
* Using a dictionary can reduce repetitive code and make lookups more efficient.
* Accessing dictionary values in Swift involves optionals.
