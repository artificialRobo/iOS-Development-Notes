# Notes: Forking and Pull Requests

## 1. Review of Git Areas

Git workflow involves four main areas:

1. **Working Directory** – where you edit files.
2. **Staging Area** – where changes are prepared for commit.
3. **Local Repository** – stores commits on your computer.
4. **Remote Repository** – repository hosted online (e.g., GitHub).

---

## 2. Collaborating with Remote Repositories

When working with others, GitHub enables collaboration through:

* **Forking**
* **Pull Requests (PRs)**

This is the standard workflow for contributing to open-source projects.

---

## 3. What is Forking?

**Forking** = Creating a copy of someone else's GitHub repository under your own GitHub account.

### Important:

* Different from **git clone**.
* **git clone** copies a repository to your local machine.
* **Fork** copies a repository on GitHub itself.

### Why Fork?

Repository owners don't want random internet users modifying their code directly.

After forking:

* You own the copied repository.
* You have full read/write permissions on your fork.
* The original repository remains unchanged.

---

## 4. Open Source Contribution Workflow

### Step 1: Fork the Repository

Create a personal copy of the original GitHub repository.

### Step 2: Clone Your Fork

Download your fork to your local machine.

### Step 3: Make Changes

Examples:

* Fix bugs
* Add features
* Improve documentation
* Refactor code

### Step 4: Commit and Push

Save changes locally and push them to your forked repository.

### Step 5: Create a Pull Request

Request that the original repository owner review and merge your changes.

---

## 5. What is a Pull Request?

A **Pull Request (PR)** is a request asking the repository owner to review and merge your changes.

Think of it as:

> "Here are my suggested improvements. If you like them, please merge them."

### Why is it called a Pull Request?

Because the repository owner chooses to **pull** your changes into their repository.

You cannot directly **push** changes to a repository you don't own.

---

## 6. Pull Request Review Process

When a PR is submitted:

The repository owner can:

* Review code changes
* View commit history
* Leave comments/feedback
* Request modifications
* Approve the changes
* Reject the changes

If approved:

* The PR is **merged**
* A new merge commit is created
* Changes become part of the main repository

---

## 7. Example Workflow

### Original Repository

Owned by Angela.

### Contributor (Gilfoyle)

1. Forks Angela's repository.
2. Makes edits to a chapter.
3. Commits changes.
4. Pushes changes to his fork.
5. Creates a Pull Request.

### Repository Owner (Angela)

1. Receives the PR.
2. Reviews changes.
3. Leaves feedback.
4. Approves the PR.
5. Merges it into the master/main branch.

Result:

* Gilfoyle's changes appear in Angela's repository.
* GitHub shows the merge history and source branch.

---

## 8. Trusted Team vs Open Source Contributors

### Team Repository

Members usually have:

* Read access
* Write access

They can:

* Clone
* Commit
* Push directly

### Open Source Repository

Public contributors usually have:

* Read access only

They must:

* Fork
* Make changes
* Submit Pull Requests

---

## 9. Benefits of Open Source Collaboration

### Learn Team Development

Gain experience working like professional software teams.

### Improve Existing Projects

Contribute:

* Bug fixes
* Features
* Documentation
* Refactoring

### Build a Portfolio

Public contributions showcase your skills.

### Connect with Developers

GitHub acts like a social network for programmers.

---

## 10. Example: Open Source Projects

Popular open-source projects often have:

* Thousands of forks
* Hundreds of contributors
* Many pull requests

Contributions can range from:

### Simple

* Updating README files
* Fixing typos

### Advanced

* Adding features
* Fixing bugs
* Improving performance

Maintainers review contributions before merging.

---

## 11. Key Terms

| Term         | Meaning                                          |
| ------------ | ------------------------------------------------ |
| Fork         | Personal GitHub copy of another repository       |
| Clone        | Download repository to local machine             |
| Commit       | Save a snapshot of changes                       |
| Push         | Upload commits to a remote repository            |
| Pull Request | Request to merge changes into another repository |
| Merge        | Combine changes into the target branch           |
| Read Access  | Can view repository                              |
| Write Access | Can directly modify repository                   |

---

## Summary

**Open-source workflow:**

**Fork → Clone → Modify → Commit → Push → Pull Request → Review → Merge**

This is the standard GitHub collaboration model used by most open-source projects.
