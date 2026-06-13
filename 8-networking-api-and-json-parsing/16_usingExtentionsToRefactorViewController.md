# Notes: Using Extensions, MARK Comments, and Code Snippets to Refactor ViewController

## 1. Refactoring with Extensions

* `WeatherViewController` originally adopted two protocols:

  * `UITextFieldDelegate`
  * `WeatherManagerDelegate`
* To improve code organization, protocol-related code is moved into separate extensions.

### UITextFieldDelegate Extension

```swift
extension WeatherViewController: UITextFieldDelegate {
    // Text field methods
}
```

* Move all text field-related methods (including `searchPressed`) into this extension.
* Remove `UITextFieldDelegate` from the main class declaration.

### WeatherManagerDelegate Extension

```swift
extension WeatherViewController: WeatherManagerDelegate {
    // Weather manager methods
}
```

* Move:

  * `didUpdateWeather`
  * `didFailWithError`
* Remove `WeatherManagerDelegate` from the main class declaration.

### Benefits of Extensions

* Separates responsibilities into logical sections.
* Makes the main view controller cleaner and easier to read.
* Xcode displays extensions and their methods separately in the file structure.

---

## 2. Using MARK Comments

* `MARK` comments create visible sections in Xcode's file navigator.

#### Syntax

```swift
// MARK: - UITextFieldDelegate
```

#### Example

```swift
// MARK: - UITextFieldDelegate
extension WeatherViewController: UITextFieldDelegate {
    ...
}
```

```swift
// MARK: - WeatherManagerDelegate
extension WeatherViewController: WeatherManagerDelegate {
    ...
}
```

### Benefits of MARK

* Divides large files into clear sections.
* Improves navigation within the file.
* Sections appear in Xcode's jump bar and file structure.

---

## 3. Creating Custom Code Snippets

Code snippets allow frequently used code to be inserted quickly.

### Steps to Create a Snippet

1. Select the code.
2. Right-click.
3. Choose **Create Code Snippet**.
4. Add:

   * Title (e.g., *Mark Comment*)
   * Summary
   * Completion shortcut (e.g., `mark`)

---

## 4. Adding Placeholders in Code Snippets

Placeholders let you quickly customize inserted code.

#### Placeholder Syntax

```swift
<#Section Heading#>
```

#### Example Snippet

```swift
// MARK: - <#Section Heading#>
```

When inserted, Xcode highlights the placeholder so you can replace it easily.

---

## 5. Using the Custom Snippet

* Type the completion shortcut:

  ```
  mark
  ```
* Press **Enter**.
* Xcode inserts:

  ```swift
  // MARK: - <#Section Heading#>
  ```
* Replace the placeholder with a section name such as:

  * `UITextFieldDelegate`
  * `WeatherManagerDelegate`

---

## Final File Structure

```swift
class WeatherViewController: UIViewController {
    // Properties and core functionality
}

// MARK: - UITextFieldDelegate
extension WeatherViewController: UITextFieldDelegate {
    // Text field methods
}

// MARK: - WeatherManagerDelegate
extension WeatherViewController: WeatherManagerDelegate {
    // Weather manager methods
}
```

## Key Takeaways

* Use **extensions** to separate protocol-specific functionality.
* Use **MARK comments** to create organized sections in large files.
* Create **custom code snippets** to speed up repetitive coding tasks.
* Use **placeholders (`<#...#>`)** in snippets for easy customization.
* A well-organized file is easier to read, maintain, and navigate.
