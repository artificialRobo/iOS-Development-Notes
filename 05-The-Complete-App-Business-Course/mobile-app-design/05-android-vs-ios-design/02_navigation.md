# Notes: Navigation Differences Between iOS and Android

## 1. Back Navigation

* **Android:**

  * Uses a **hardware/system Back button**.
  * Back navigation is **time-based**.
  * Returns to the **previous screen visited**, similar to a web browser's Back button.

* **iOS:**

  * Uses a **Back button** in the **top-left corner**.
  * Back navigation is **hierarchy-based**.
  * Returns to the **parent screen** rather than the previously visited screen.

**Key Point:**
When designing an app, navigation should follow each platform's expected behavior.

---

## 2. Navigation Styles

**Android**

* Traditionally uses a **Hamburger Menu (☰)**.
* Tapping it opens a **side navigation drawer** with different screens.
* Called a "hamburger" because the three horizontal lines resemble a hamburger.

**iOS**

* Traditionally uses a **Bottom Tab Bar**.
* Located at the bottom of the screen.
* Recommended maximum of **5 tabs** for easy thumb navigation.

---

## 3. Hamburger Menu vs Tab Bar

* Many designers dislike the **hamburger menu** because:

  * Navigation options are **hidden**.
  * Users may forget features that are "out of sight, out of mind."
* As a result, many Android apps now use:

  * **Top tab navigation** with **swipe gestures**.
  * Users can swipe left or right to switch between screens.
* **Example:** The Android version of the **Twitter** app uses this navigation style.

---

## Key Takeaways

* **Android Back:** Returns to the **previous screen** (time-based).
* **iOS Back:** Returns to the **parent screen** (hierarchy-based).
* **Android Navigation:** Traditionally uses a **hamburger menu**, though swipeable tabs are becoming more common.
* **iOS Navigation:** Primarily uses a **bottom tab bar** (up to 5 tabs).
* Always design navigation according to the conventions of the target platform for a better user experience.
