# Swift Deep Dive: Dictionaries

## What is a Dictionary in Swift?

* A **Dictionary** is a collection data type in Swift, similar to an array.
* It stores data as **key-value pairs**.
* The **key** is used to look up an item.
* The **value** is the information associated with that key.

**Example:**

```swift
var dictionary = [
    "brewery": "A place where beer is made"
]
```

---

### Multiple Key-Value Pairs

* A dictionary can contain many entries.
* Key-value pairs are separated by commas.

**Example:**

```swift
var dictionary = [
    "brewery": "A place where beer is made",
    "bakery": "A place where bread is made"
]
```

---

### Data Types in Dictionaries

* Keys and values do not have to be the same type.
* You can explicitly define the dictionary's data types.

**Example (String key, Int value):**

```swift
var phoneBook: [String: Int] = [
    "John": 771234567,
    "Sarah": 771234568
]
```

**Syntax:**

```swift
[KeyType: ValueType]
```

---

## Dictionary vs Array

| Array                       | Dictionary               |
| --------------------------- | ------------------------ |
| Stores values only          | Stores key-value pairs   |
| Access items using an index | Access items using a key |
| Example: `array[0]`         | Example: `dict["John"]`  |

---

## Retrieving Values

**Array:**

```swift
array[0]
```

* Uses a numeric index.
* Returns the item at that position.

**Dictionary:**

```swift
dict["John"]
```

* Uses a key instead of an index.
* Returns the value associated with that key.

**Example:**

```swift
var phoneBook: [String: Int] = [
    "John": 771234567
]

phoneBook["John"]
```

**Output:**

```swift
771234567
```

---

## Key Takeaways

* Dictionaries are collections that store **key-value pairs**.
* Created using square brackets `[]`.
* Keys are unique identifiers used to retrieve values.
* Keys and values can have different data types.
* Arrays use **indexes** to access data; dictionaries use **keys**.
* Dictionary type syntax:

  ```swift
  [KeyType: ValueType]
  ```
