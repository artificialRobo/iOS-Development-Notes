# Notes: Using Xcode for Source Control

### Overview

* Xcode 9 significantly improved built-in Git integration.
* Developers can perform most Git tasks directly in Xcode without using the command line.
* Equivalent Git operations (init, commit, branch, merge, push, pull, etc.) are available through Xcode's GUI.

---

## 1. Creating a Git Repository in Xcode

### Steps

1. Create a new Xcode project.
2. Check **"Create Git repository on my Mac"**.
3. This is equivalent to:

```bash
git init
```

### Result

* Xcode automatically creates an **Initial Commit**.
* View commits in the **Source Control Navigator**.

---

## 2. Making Commits

### Example Changes

* Added labels:

  * "Udder"
  * "Fresh Milk, On Demand"
* Added image assets:

  * Milk image
  * Cow image

### Commit Process

1. Go to **Source Control → Commit**.
2. Review file differences.
3. Enter a commit message.
4. Commit changes.

Example commit message:

```text
Add label and images
```

### Key Point

* Xcode visually displays changes before committing, including XML changes in Storyboards.

---

## 3. Restoring Lost Work (Discard Changes)

### Scenario

* Accidentally:

  * Deleted UI elements
  * Modified files incorrectly
  * Deleted storyboard files
  * Added invalid code

### Solution

Use:

```text
Source Control → Discard All Changes
```

### Result

* Reverts the project back to the last commit.
* Restores the last stable version.

### Benefit

Git acts like a checkpoint system, allowing recovery from mistakes.

---

## 4. Working with Branches

### Creating a Branch

From Source Control Navigator:

```text
Right Click Commit → Branch From...
```

Example branch:

```text
milk-design
```

### Important

Creating a branch does not switch to it automatically.

Use:

```text
Checkout
```

to switch branches.

---

## 5. Example: Milk Design Branch

### Changes

* Added an Image View.
* Displayed a milk image.

### Commit

```text
Change view controller interface
```

### Result

* Changes are stored only in the `milk-design` branch.

---

## 6. Example: Cow Design Branch

### Steps

1. Branch again from master.
2. Create:

```text
cow-design
```

3. Add cow image instead.

### Commit

```text
Change interface to incorporate cow image
```

### Best Practice

Use descriptive commit messages.

Bad:

```text
Changes
```

Good:

```text
Change interface to incorporate cow image
```

---

## 7. Merging Branches

### Goal

Choose the milk design as the final version.

### Steps

1. Checkout `milk-design`.
2. Right-click `master`.
3. Select:

```text
Merge 'milk-design' into 'master'
```

### Result

* Master now contains the milk design.
* Xcode automatically returns to the master branch.

---

## 8. Viewing Old Commits

### Purpose

Review previous versions of the project.

### Steps

1. Right-click a commit.
2. Select:

```text
Checkout Commit
```

### Result

* Project temporarily reverts to that historical state.

### Use Cases

* Recover old ideas.
* Review previous implementations.
* Compare older versions of code.

---

## 9. Comparing Versions

### Example

Master branch:

* Added `viewWillAppear()`.

Milk-design branch:

* Removed `didReceiveMemoryWarning()`.

### Tool

Use the:

```text
Version Editor
```

### Benefits

* Compare files side-by-side.
* Compare:

  * Different commits
  * Different branches
  * Historical versions

### Why Useful?

Helps identify:

* Added code
* Removed code
* Differences between branches

---

## 10. Connecting Xcode to GitHub

### Setup

Go to:

```text
Xcode → Preferences → Accounts
```

Add:

```text
GitHub Account
```

### What Happens

* Xcode authenticates with GitHub.
* Retrieves necessary credentials.
* Enables remote repository management.

---

## 11. Creating a GitHub Remote

### Steps

1. Open Source Control Navigator.
2. Right-click repository.
3. Select:

```text
Create Remote on GitHub
```

### Configuration

* Repository name
* Description
* Default remote:

```text
origin
```

### Result

* Local repository is pushed to GitHub.

---

## 12. Pushing Changes

### After New Commits

Option 1:

```text
Commit and Push
```

Option 2:

```text
Source Control → Push
```

### Purpose

Uploads local commits to GitHub.

---

## 13. Pulling Changes

### Scenario

Someone (or you) modifies GitHub directly.

Example:

* Added a README file on GitHub.

Now:

```text
Remote repository > Local repository
```

### Push Fails

Because local code is outdated.

### Solution

```text
Source Control → Pull
```

Pull from:

```text
origin/master
```

### Result

* Downloads remote changes.
* Synchronizes local repository.

---

## 14. Push After Pull

### Workflow

1. Commit local changes.
2. Pull remote updates.
3. Resolve differences if needed.
4. Push latest version.

Example:

```text
Commit:
Add viewDidDisappear

Pull:
origin/master

Push:
origin/master
```

### Result

Both local and remote repositories stay synchronized.

---

# Key Git Concepts Covered

| Concept               | Xcode Feature            |
| --------------------- | ------------------------ |
| Initialize Repository | Create Git Repository    |
| Commit                | Source Control → Commit  |
| View History          | Source Control Navigator |
| Undo Changes          | Discard All Changes      |
| Branch                | Branch From              |
| Switch Branch         | Checkout                 |
| Merge                 | Merge Into               |
| View Old Versions     | Checkout Commit          |
| Compare Versions      | Version Editor           |
| Remote Repository     | GitHub Integration       |
| Upload Changes        | Push                     |
| Download Changes      | Pull                     |

---

## Main Takeaway

Xcode 9 provides a complete graphical interface for Git, allowing developers to:

* Initialize repositories
* Commit changes
* Create branches
* Merge branches
* Compare versions
* Recover old work
* Connect to GitHub
* Push and pull changes

All without needing to use the command line.
