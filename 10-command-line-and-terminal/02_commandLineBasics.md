# Notes: Basics of Command Line and Shortcuts

## Terminal Basics (macOS)

### 1. Opening Terminal

* Open **Spotlight Search** with:

  * Click Spotlight icon, or
  * Press **Command + Space**
* Search for **Terminal** and open it.
* Alternatively, open it from the **Applications** folder.

### 2. Terminal Appearance

* Terminal themes can be customized via:

  * **Terminal → Preferences → Profiles**
* Different color schemes can improve readability and reduce eye strain.

---

## Understanding Your Location in Terminal

### Home Directory (`~`)

* The **tilde (`~`)** represents your **home directory**.
* Example path:

  ```
  Macintosh HD
  └── Users
      └── username (~)
  ```
* When Terminal opens, you're usually placed in your home directory.

### Check Contents of Current Directory

```bash
ls
```

* `ls` = **list**
* Displays files and folders in the current directory.

---

## Navigating Directories

### Change Directory (`cd`)

```bash
cd Documents
```

* Moves into the Documents folder.

### Auto-complete with Tab

* Type part of a folder name and press **Tab**:

  ```bash
  cd Doc<Tab>
  ```
* Terminal completes the folder name automatically.
* If multiple matches exist, type more letters before pressing Tab.

---

## Directory Paths

### Move One Folder at a Time

```bash
cd Documents
cd Learn
cd Languages
```

### Move Using a Full Path

```bash
cd Documents/Learn/Languages
```

* Faster than moving one directory at a time.

### Return to Home Directory

```bash
cd ~
```

* Takes you back to your home directory.

---

## Command History

### Previous Commands

* **Up Arrow** → Previous command
* **Down Arrow** → Next command

Useful for reusing commands without retyping them.

---

## Quick Navigation Trick

### Drag-and-Drop Folder

1. Type:

   ```bash
   cd
   ```
2. Drag a folder from Finder into Terminal.
3. Terminal automatically inserts the folder's full path.
4. Press Enter.

Example:

```bash
cd /Users/username/Documents/Learn/Languages
```

---

## Moving Backwards in Directories

### Go Up One Level

```bash
cd ..
```

Example:

```bash
Languages → Learn
Learn → Documents
Documents → Home
```

### Go Up Multiple Levels

```bash
cd ..
cd ..
cd ..
```

---

## Relative vs Absolute Paths

### Moving Forward

If a folder exists inside the current directory:

```bash
cd Music
```

### Moving Backward/Elsewhere

Use the full path:

```bash
cd /Users/username/Music
```

---

## Clearing the Terminal Screen

```bash
clear
```

* Removes previous output from the screen.
* Does **not** change your current directory.

---

## Editing Commands Efficiently

### Option/Alt Click

* Hold **Option (Alt)** and click anywhere in a command line.
* Moves the cursor directly to that position.

Useful when editing long commands.

---

## Useful Keyboard Shortcuts

| Shortcut     | Action                           |
| ------------ | -------------------------------- |
| `Ctrl + A`   | Move cursor to beginning of line |
| `Ctrl + E`   | Move cursor to end of line       |
| `Up Arrow`   | Previous command                 |
| `Down Arrow` | Next command                     |
| `Ctrl + U`   | Clear current command line       |

### Example

```bash
Ctrl + A
```

Moves cursor to:

```bash
|cd Documents/Learn/Languages
```

```bash
Ctrl + E
```

Moves cursor to:

```bash
cd Documents/Learn/Languages|
```

```bash
Ctrl + U
```

Clears the entire command without executing it.

---

## Key Commands Learned

```bash
ls          # List files and folders
cd folder   # Enter a folder
cd ~        # Go to home directory
cd ..       # Go up one directory level
clear       # Clear terminal screen
```

---

## Key Takeaways

* `ls` lists directory contents.
* `cd` changes directories.
* `~` represents your home directory.
* `..` moves up one directory level.
* Use **Tab** for auto-completion.
* Use **Up/Down arrows** to access command history.
* Use keyboard shortcuts (`Ctrl+A`, `Ctrl+E`, `Ctrl+U`) to work faster.
* Dragging folders into Terminal is a quick way to get full paths.
