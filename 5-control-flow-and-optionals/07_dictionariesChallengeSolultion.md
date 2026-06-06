## Notes: Optionals and Dictionaries in Swift App

### 1. Converting an Optional to a Non-Optional

* `sender.currentTitle` returns an **optional String** (`String?`).
* To force Swift to treat it as a non-optional, use an exclamation mark (`!`):

  ```swift
  sender.currentTitle!
  ```
* This is called **force unwrapping**.
* By using `!`, the programmer is telling Swift:

  > "I know this value will never be nil."

### 2. Errors vs Warnings

* **Errors** prevent the app from running.
* **Warnings** do not stop the app from running.

### 3. Why Does the Dictionary Return an Optional?

* Even after unwrapping `sender.currentTitle`, accessing a dictionary value still returns an optional.
* Example:

  ```swift
  let result = eggTimes["Soft"]
  ```
* `result` is of type:

  ```swift
  Int?
  ```

  (Optional Integer)

### 4. Reason Dictionaries Return Optionals

* Dictionary keys are often strings.
* Swift cannot guarantee that a key exists.
* Example:

  ```swift
  eggTimes["Soft"]   // Returns 5
  eggTimes["soft"]   // Returns nil
  ```
* Because a key might be misspelled or missing, Swift returns an optional value.

### 5. Checking the Type

* Option-clicking on a variable in Xcode shows its type.
* Example:

  ```swift
  let result = eggTimes["Soft"]
  ```

  Type:

  ```swift
  Int?
  ```

### 6. Force Unwrapping Dictionary Results

* If you're certain the key exists, you can force unwrap:

  ```swift
  let result = eggTimes["Soft"]!
  ```
* This converts the optional integer into a regular integer.

### 7. When Is Force Unwrapping Safe?

* Safe when you are absolutely sure the key exists.
* Example:

  * Button titles are `"Soft"`, `"Medium"`, and `"Hard"`.
  * These exactly match the keys in the dictionary.
  * Therefore:

    ```swift
    eggTimes[hardness]!
    ```

    is unlikely to fail.

## Key Takeaways

* `!` = force unwrap an optional value.
* `sender.currentTitle` is optional because a button may not have a title.
* Dictionary lookups return optionals because the requested key may not exist.
* Use force unwrapping only when you are certain the value is not `nil`.
* A successfully unwrapped dictionary value becomes a normal value (e.g., `Int` instead of `Int?`).
