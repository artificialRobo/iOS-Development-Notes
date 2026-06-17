# Notes: UITableView and Message Model

## What is UITableView?

* `UITableView` is one of the most commonly used UI components in iOS.
* It displays data in a scrollable list of rows (cells).
* Commonly used in apps like Mail, Messages, Settings, etc.

---

## Creating a UITableView

1. Open the Object Library.
2. Search for **Table View**.
3. Drag and drop it onto a View Controller.
4. Resize it as needed (full screen or partial screen).

### Table View Controller vs View Controller

* **Table View Controller**

  * Specialized controller dedicated to displaying a table view.
  * Less flexible.

* **View Controller + Table View**

  * More flexible.
  * Can place table views anywhere on the screen.
  * Preferred approach in this lesson.

---

## Prototype Cells

* A table view contains **prototype cells**.
* Prototype cells are reused to display multiple rows efficiently.
* All cells share the same layout but display different data.

### Cell Customization Options

* Disclosure indicators
* Selection styles
* Title + subtitle layouts
* Custom cell designs

### Important: Reuse Identifier

* Every prototype cell should have a unique identifier.
* Example:

```swift
ReusableCell
```

* Used in code to dequeue and reuse cells.

---

## Creating a Message Model

Create a Swift file named:

```swift
Message.swift
```

Create a structure:

```swift
struct Message {
    let sender: String
    let body: String
}
```

### Properties

| Property | Type   | Purpose         |
| -------- | ------ | --------------- |
| sender   | String | Email of sender |
| body     | String | Message content |

---

## Creating a Messages Array

Inside `ChatViewController`:

```swift
var messages: [Message] = [
    Message(sender: "1@2.com", body: "Hey!!"),
    Message(sender: "a@b.com", body: "Hello!"),
    Message(sender: "1@2.com", body: "What's up?")
]
```

This acts as the data source for the table view.

---

## Connecting the Table View

Create an IBOutlet:

```swift
@IBOutlet weak var tableView: UITableView!
```

Connect it from the storyboard to the controller.

---

## UITableViewDataSource

UITableView uses the **Data Source** pattern to obtain data.

### Step 1: Adopt the Protocol

```swift
extension ChatViewController: UITableViewDataSource {
}
```

### Step 2: Set Data Source

Inside `viewDidLoad()`:

```swift
tableView.dataSource = self
```

---

## Required Data Source Methods

### 1. Number of Rows

Determines how many cells appear.

```swift
func tableView(_ tableView: UITableView,
               numberOfRowsInSection section: Int) -> Int {
    return messages.count
}
```

### Why Use `messages.count`?

* Dynamic.
* Updates automatically when messages are added.
* Avoids hardcoding values.

---

### 2. Cell for Row

Provides a cell for each row.

```swift
func tableView(_ tableView: UITableView,
               cellForRowAt indexPath: IndexPath)
               -> UITableViewCell {

    let cell = tableView.dequeueReusableCell(
        withIdentifier: K.cellIdentifier,
        for: indexPath)

    return cell
}
```

### Reusable Cells

* Prevents creating new cells repeatedly.
* Improves performance and memory usage.

---

## Displaying Data in Cells

### Static Text Example

```swift
cell.textLabel?.text = "This is a cell"
```

Result:

```
This is a cell
This is a cell
This is a cell
```

---

### Display Row Numbers

```swift
cell.textLabel?.text = "\(indexPath.row)"
```

Output:

```
0
1
2
```

### Understanding `indexPath.row`

* Represents the current row number.
* Used to access data corresponding to that row.

---

## Displaying Message Data

Use the row number to retrieve a message:

```swift
messages[indexPath.row]
```

Get the message body:

```swift
cell.textLabel?.text = messages[indexPath.row].body
```

Output:

```
Hey!!
Hello!
What's up?
```

---

## Table View Separators

Separator lines can be configured in the storyboard.

### Options

* Default → visible separators
* None → no separators

For a chat app:

* Separators are unnecessary.
* Usually disabled because messages will later appear in chat bubbles.

---

## UITableViewDelegate

The delegate handles **user interactions** with the table view.

### Step 1: Adopt Protocol

```swift
extension ChatViewController: UITableViewDelegate {
}
```

### Step 2: Set Delegate

```swift
tableView.delegate = self
```

---

## Example: Detect Cell Selection

```swift
func tableView(_ tableView: UITableView,
               didSelectRowAt indexPath: IndexPath) {

    print(indexPath.row)
}
```

### Behavior

* Tapping row 0 prints `0`
* Tapping row 1 prints `1`
* Tapping row 2 prints `2`

Useful for:

* To-do lists
* Navigation
* Updating selected items

---

## Why Delegate Was Removed

For a chat app:

* Messages should not be selectable.
* No action is needed when users tap messages.

Therefore:

* Delegate code was removed.
* Cell selection was disabled.

### Disable Cell Selection

In the prototype cell:

```text
Selection = None
```

Result:

* Tapping messages does nothing.
* Matches normal chat app behavior.

---

## Data Source vs Delegate

| Data Source                  | Delegate             |
| ---------------------------- | -------------------- |
| Supplies data                | Handles interactions |
| Number of rows               | Row selection        |
| Cell content                 | User actions         |
| Required for displaying data | Optional             |

---

## Key Takeaways

* `UITableView` displays scrollable lists of data.
* Prototype cells are reused for efficiency.
* Every reusable cell needs a **Reuse Identifier**.
* Create a model (`Message`) to structure data.
* Use a messages array as the table's data source.
* Implement `UITableViewDataSource`:

  * `numberOfRowsInSection`
  * `cellForRowAt`
* Use `indexPath.row` to access data for a specific row.
* `UITableViewDelegate` handles user interaction.
* Chat apps typically disable cell selection.
* Reusable cells improve performance and memory efficiency.

### Next Step

Create **custom table view cells** and **chat/message bubbles** instead of using the default table view cell appearance.
