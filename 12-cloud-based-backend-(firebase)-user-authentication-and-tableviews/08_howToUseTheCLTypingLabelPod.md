# Notes: Using CLTypingLabel Pod in your Xcode Project

## 1. Using the CLTypingLabel Pod

After successfully adding the **CLTypingLabel** CocoaPod and building the project, the next step is to use it in the app.

### Finding Usage Instructions

* Check the library documentation:

  * GitHub README
  * CocoaPods page
* Look for the **Usage** section.

---

## 2. Changing a UILabel to CLTypingLabel

### In Interface Builder

1. Open `Main.storyboard`.
2. Select the label you want to animate.
3. Open the **Identity Inspector**.
4. Change the class from:

   ```swift
   UILabel
   ```

   to:

   ```swift
   CLTypingLabel
   ```

Because the pod has been installed correctly, Xcode will recognize the new class.

---

## 3. Updating the IBOutlet

### Before

```swift
@IBOutlet weak var titleLabel: UILabel!
```

### After

```swift
@IBOutlet weak var titleLabel: CLTypingLabel!
```

### Import the Module

Since CLTypingLabel comes from a CocoaPod, import it at the top of the file:

```swift
import CLTypingLabel
```

Build the project (`⌘ + B`) to verify that Xcode recognizes the type.

---

## 4. Triggering the Typing Animation

According to the documentation, the animation starts automatically when a new string is assigned to the label's `text` property.

### Example

Inside `viewDidLoad()`:

```swift
override func viewDidLoad() {
    super.viewDidLoad()

    titleLabel.text = "⚡️FlashChat"
}
```

### Result

* The typing animation runs automatically.
* No need to manually create loops or timers.
* Achieves the same effect with a single line of code.

---

## 5. Benefits of Third-Party Libraries

Using a CocoaPod:

* Saves development time.
* Reduces the amount of code you need to write.
* Provides more polished and reusable functionality.
* Lets developers leverage community-built solutions.

---

## 6. Fixing the PIE Warning

### Warning Encountered

A warning related to **PIE (Position-Independent Executable)** may appear.

### Solution

1. Open the **Pods** project.
2. Select the **Pods** target.
3. Go to **Build Settings**.
4. Search for:

   ```
   position
   ```
5. Change:

   ```
   Generate Position-Dependent Code
   ```

   to:

   ```
   Yes
   ```

### Outcome

* Rebuild the project.
* The warning should disappear.

### General Troubleshooting Tip

* Copy warning messages into Google or Stack Overflow.
* Often another developer has already found a solution.

---

## 7. CocoaPods Workflow Learned

By this point, the tutorial has covered:

1. Creating a `Podfile`
2. Generating an `.xcworkspace`
3. Installing a CocoaPod
4. Using the pod in a project
5. Removing a pod

---

## 8. Removing a CocoaPod

### Step 1: Remove Pod Usage from Code

Restore the label type:

```swift
@IBOutlet weak var titleLabel: UILabel!
```

Remove:

```swift
import CLTypingLabel
```

### Step 2: Update Storyboard

* Open `Main.storyboard`.
* Change the label class from:

  ```
  CLTypingLabel
  ```

  back to:

  ```
  UILabel
  ```

---

### Step 3: Remove the Pod from the Podfile

Delete:

```ruby
pod 'CLTypingLabel'
```

Save the file.

---

### Step 4: Reinstall Pods

1. Close Xcode.
2. Open Terminal.
3. Run:

```bash
pod install
```

CocoaPods updates dependencies and removes CLTypingLabel from the project.

---

### Step 5: Verify Removal

Inside the workspace:

* Open the **Pods** folder.
* Confirm that **CLTypingLabel** is no longer present.

---

## Key Takeaways

* Change a label's class to `CLTypingLabel` to enable typing animations.
* Import the library using:

  ```swift
  import CLTypingLabel
  ```
* Assigning text automatically triggers the animation:

  ```swift
  titleLabel.text = "⚡️FlashChat"
  ```
* Third-party libraries can significantly reduce development effort.
* CocoaPods supports easy installation and removal of dependencies.
* Use Google or Stack Overflow to investigate build warnings and errors.
* Keep the `Podfile` even after removing a pod because it can be used to add future dependencies (e.g., Firebase).
