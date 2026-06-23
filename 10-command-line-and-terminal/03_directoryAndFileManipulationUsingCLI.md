# Notes: Directory and File Manipulation using Command Line

## Accessing Directories using Command Line

### 1. Creating Directories

* Use the `mkdir` command to create a new directory (folder).
* Syntax:

  ```bash
  mkdir DirectoryName
  ```
* Example:

  ```bash
  mkdir Angela
  ```

  Creates a folder named **Angela**.

### 2. Navigating Directories

* Use `cd` to move into a directory.
* Example:

  ```bash
  cd Angela
  ```
* Use `ls` to list contents of the current directory.
* An empty folder will show no files when using `ls`.

---

## Creating Files

### Graphical Method

* Open an application (e.g., TextEdit).
* Create a file.
* Save it in the desired folder.
* More steps are involved compared to the command line.

### Command Line Method

* Use `touch` to create a new file.
* Syntax:

  ```bash
  touch filename.txt
  ```
* Example:

  ```bash
  touch Text2.txt
  ```

---

## Opening Files

### Default Application

```bash
open Text2.txt
```

* Opens the file using the system's default application.

### Specific Application

Use the `-a` flag:

```bash
open -a Atom Text2.txt
```

* Opens the file in the Atom editor.

---

## Deleting Files

### Remove a Single File

* Use `rm` (remove).
* Example:

  ```bash
  rm Text.rtf
  ```

### Remove Multiple Files Using Wildcards

* `*` matches all files in the current directory.
* Example:

  ```bash
  rm *
  ```
* Deletes all files in the current directory.

⚠️ **Be careful:** This action cannot be easily undone.

---

## Safety Warning

* Command line operations provide more power and control than graphical interfaces.
* Always verify your current location before running destructive commands.
* Check your location with:

  ```bash
  ls
  ```

  or

  ```bash
  pwd
  ```

---

## Deleting Directories

### Why `rm` Alone Doesn't Work

```bash
rm Angela
```

* Produces an error because **Angela is a directory**.

### Remove a Directory Recursively

Use the `-r` flag:

```bash
rm -r Angela
```

* Deletes the directory and all files/subdirectories inside it.

⚠️ **Recursive deletion is destructive.**

---

## Dangerous Commands

### Force Deletion

```bash
rm -rf DirectoryName
```

* `-r` = recursive (delete directories and contents)
* `-f` = force (no confirmation prompts)

### Extremely Dangerous Example

```bash
sudo rm -rf --no-preserve-root /
```

* `sudo` = execute as administrator.
* `--no-preserve-root` removes protection on the root directory.
* Can wipe an entire system and make recovery impossible.

⚠️ Never run commands you don't fully understand.

---

## Key Commands Summary

| Command                | Purpose                               |
| ---------------------- | ------------------------------------- |
| `mkdir folder`         | Create a directory                    |
| `cd folder`            | Move into a directory                 |
| `ls`                   | List directory contents               |
| `touch file.txt`       | Create a file                         |
| `open file.txt`        | Open with default app                 |
| `open -a App file.txt` | Open with specific app                |
| `rm file.txt`          | Delete a file                         |
| `rm *`                 | Delete all files in current directory |
| `rm -r folder`         | Delete a directory and contents       |
| `rm -rf folder`        | Force delete directory recursively    |

---

## Additional Resources Mentioned

* **Learn Enough Command Line to Be Dangerous** – recommended free tutorial for learning more advanced command-line concepts such as grep, curl, and other developer tools.

---

## Bonus: Hidden Terminal Game

* macOS includes a text adventure game through Emacs:

  ```bash
  emacs -batch -l dunnet
  ```
* Launches a classic text-based adventure game inside Terminal.
* Commands like:

  ```text
  take shovel
  dig
  ```

  can be used to interact with the game.
