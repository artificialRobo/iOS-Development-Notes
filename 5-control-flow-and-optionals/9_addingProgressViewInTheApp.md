# Notes: Adding a ProgressView in the Egg Timer App

## Purpose of ProgressView

* Users cannot see debug console output, so a visual indicator is needed.
* A **ProgressView** displays how much time is left until the eggs are done.
* It visualizes the **seconds remaining** as a percentage.

---

## Adding a ProgressView in Storyboard

1. Open **Main.storyboard**.
2. Click the **+** button and search for **Progress View**.
3. Drag the ProgressView into the existing **Timer View** (inside the Vertical Stack).
4. Ensure it is nested under **Timer View**.

---

## Setting Constraints

* Pin the ProgressView:

  * **0 px from the left**
  * **0 px from the right**
* Add **Vertical Center in Container** constraint.
* This centers the ProgressView within the Timer View.

---

## Customizing the ProgressView

1. Change the style from **Default** to **Bar**.
2. Add a **height constraint of 5 px** for better visibility.
3. Customize colors:

   * **Progress Tint** → System Yellow (completed portion)
   * **Track Tint** → System Gray (remaining portion)

Result:

* Yellow = completed progress
* Gray = remaining progress

---

## Understanding the `progress` Property

* The ProgressView uses a value between **0.0 and 1.0**:

  * `0.0` = 0% complete
  * `0.5` = 50% complete
  * `1.0` = 100% complete

---

## Connecting ProgressView to Code

1. Create an **IBOutlet** from the ProgressView to `ViewController`.
2. Make sure the type is **UIProgressView**.
3. Name it:

```swift
@IBOutlet weak var progressBar: UIProgressView!
```

---

## Updating the Progress Bar in Code

When an egg button is pressed:

```swift
progressBar.progress = 1.0
```

* `progress` expects a **Float** value.
* `1.0` represents **100% completion**.

---

## Current Result

* Pressing any egg button immediately fills the progress bar to 100%.

---

## Next Challenge

Instead of jumping directly to 100%, update the ProgressView so that it:

* Reflects the **remaining cooking time**.
* Gradually increases as the timer counts down.
* Provides a real-time visual representation of progress.
