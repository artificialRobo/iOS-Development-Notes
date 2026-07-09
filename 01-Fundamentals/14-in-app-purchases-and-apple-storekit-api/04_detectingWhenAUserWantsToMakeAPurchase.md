# Notes: Setting Up an In-App Purchase Button in a Table View

## Goal

* Add a **"Get More Quotes"** cell at the bottom of the table.
* When tapped, it starts the **in-app purchase** process.

---

## 1. Add an Extra Table View Cell

* Current number of cells:

  ```swift
  quotesToShow.count
  ```
* Add one extra cell:

  ```swift
  quotesToShow.count + 1
  ```
* Purpose:

  * First `quotesToShow.count` cells display quotes.
  * Last cell becomes the **Buy/Get More Quotes** button.

---

## 2. Configure the Last Cell

Use an `if` statement:

* If:

  ```swift
  indexPath.row < quotesToShow.count
  ```

  → Display a quote.

* Else:

  * Set text:

    ```
    Get More Quotes
    ```
  * Change text color (using a Color Literal).
  * Add:

    ```swift
    disclosureIndicator
    ```

    * Displays a chevron (>) to indicate the cell is tappable.

---

## 3. Detect Cell Selection

Implement the table view delegate method:

```swift
tableView(_:didSelectRowAt:)
```

* Since `UITableViewController` already has this method, use:

  ```swift
  override
  ```

---

## 4. Check if the Buy Cell Was Tapped

Condition:

```swift
if indexPath.row == quotesToShow.count
```

Reason:

* Quotes are indexed from `0`.
* The extra "Get More Quotes" cell is always at index `quotesToShow.count`.

Initially test with:

```swift
print("Buy quotes clicked")
```

---

## 5. Create the Purchase Method

Replace the test print with:

```swift
buyPremiumQuotes()
```

Then create the function:

```swift
func buyPremiumQuotes() {
    // In-app purchase code goes here
}
```

Organize code with:

```swift
#pragma MARK: In-App Purchase Methods
```

---

## 6. Improve User Experience

After selecting the cell, deselect it automatically:

```swift
tableView.deselectRow(at: indexPath, animated: true)
```

This removes the gray highlight after tapping.

---

## Key Concepts Learned

* Add an extra table view cell using `count + 1`.
* Use an `if` statement to distinguish normal cells from the purchase cell.
* Customize the purchase cell:

  * Text: **Get More Quotes**
  * Custom text color
  * `disclosureIndicator`
* Handle taps with:

  ```swift
  tableView(_:didSelectRowAt:)
  ```
* Detect the purchase cell using:

  ```swift
  indexPath.row == quotesToShow.count
  ```
* Call:

  ```swift
  buyPremiumQuotes()
  ```
* Deselect the cell for a smoother UI.

---

### Next Step

Learn to use **StoreKit** to:

* Connect to Apple's App Store.
* Query available in-app purchases.
* Purchase the **Premium Quotes** product.
