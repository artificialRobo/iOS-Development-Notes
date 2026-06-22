# Notes: Git Clone (Cloning a Remote Repository)

## What is Git Clone?

* **`git clone`** is a Git command used to copy a remote repository from GitHub (or another remote source) to your local machine.
* Cloning downloads:

  * All project files
  * Complete commit history
  * All versions and changes of the repository

<p align="center" >
    <img src="assets/git clone.png" alt="">
</p>

## Why Use Git Clone Instead of Download ZIP?

* Downloading a ZIP only gives you the current files.
* Cloning with Git:

  * Preserves commit history
  * Keeps Git tracking information
  * Allows you to use Git commands like `git log`, `git pull`, and `git push`

## Example Workflow

1. Find a repository on GitHub.
2. Click **"Clone or download"**.
3. Copy the repository URL.
4. Open Terminal and navigate to the desired directory (e.g., Desktop).
5. Run:

```bash
git clone <repository-url>
```

Example:

```bash
git clone https://github.com/user/swift-2048.git
```

6. Press Enter to download the repository to your local machine.

## After Cloning

* A new folder containing the project appears in your local directory.
* You can:

  * Open the project files.
  * Launch the project in an IDE (e.g., Xcode).
  * Run and test the application.
  * Study the source code and coding style.

## Running Cloned iOS Projects

* To run an iOS app on a real device, you typically need to:

  * Change the **Bundle Identifier**
  * Select your **Development Team**
* These changes are usually unnecessary when running on a simulator.

## Learning from Open-Source Projects

Cloning open-source repositories allows you to:

* Explore real-world codebases.
* Learn coding patterns and best practices.
* Understand project structure and implementation techniques.
* Experiment with existing applications.

## Viewing Commit History

After cloning, navigate into the project folder:

```bash
cd project-name
```

View commit history:

```bash
git log
```

This displays:

* Previous commits
* Commit messages
* Development history of the project

## Key Commands

| Command           | Purpose                                        |
| ----------------- | ---------------------------------------------- |
| `git clone <url>` | Copy a remote repository to your local machine |
| `cd <folder>`     | Move into the cloned project directory         |
| `git log`         | View commit history                            |

## Key Takeaways

* `git clone` downloads a complete repository, including its history.
* It is preferable to downloading ZIP files when working with Git projects.
* Cloned repositories can be run, modified, and studied locally.
* Use `git log` to explore the project's commit history.
* Cloning is commonly used to obtain starter projects, open-source code, and collaborative repositories.

## Next Topics

* Forking repositories
* Creating pull requests
* Merging repositories
