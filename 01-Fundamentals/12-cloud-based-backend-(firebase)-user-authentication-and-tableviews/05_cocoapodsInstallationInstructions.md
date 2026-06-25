# Notes: CocoaPods Installation Instructions

## What is CocoaPods?

* CocoaPods is a dependency manager for iOS development.
* It helps you install and manage third-party libraries (pods) in Xcode projects.
* The official CocoaPods website provides installation guides, troubleshooting resources, and documentation.

---

## Prerequisites

Before installing CocoaPods, ensure you have:

* A Mac running macOS.
* A stable internet connection.
* Administrator (admin) account access.
* The Terminal application (pre-installed on macOS).

---

## Opening Terminal

1. Click the Spotlight Search icon.
2. Search for **Terminal**.
3. Open the Terminal application.
4. Look for the command prompt (`$` or `%`), where commands are entered.

---

## macOS Catalina Users (Optional Step)

If you see a message about changing from **bash** to **zsh**:

1. Copy the command provided in the Terminal message.
2. Paste it into Terminal.
3. Press **Enter**.
4. Enter your admin password when prompted.
5. The shell will switch to **zsh**.

**Note:** Passwords typed in Terminal are hidden (no characters or asterisks appear).

---

## Step 1: Install CocoaPods

Run the following command:

```bash
sudo gem install cocoapods
```

### What happens?

* Terminal asks for your admin password.
* CocoaPods and its required gems are downloaded and installed.
* Installation time depends on internet speed (a few seconds to several minutes).

### Success Indicator

Wait until:

* The command finishes.
* The prompt (`$` or `%`) reappears.

---

## Step 2: Set Up CocoaPods

Run:

```bash
pod setup --verbose
```

### Purpose

* Downloads the CocoaPods master repository.
* Retrieves information about available pods and their versions.

### Why use `--verbose`?

* Displays progress details.
* Helps confirm the process is still running.

### Important Notes

* This step may take longer than installation.
* Requires a reliable internet connection.
* If it fails, try running the command again.

---

## Step 3: Verify Installation

Check that CocoaPods is installed correctly:

```bash
pod --version
```

### Expected Result

* A version number appears (e.g., `1.8.4`, `1.9.x`, or newer).

### If You See a Version Number

CocoaPods is successfully installed and ready to use.

### If You See an Error

* Repeat the installation steps.
* Check the CocoaPods troubleshooting guide for common fixes.

---

## Key Commands Summary

| Purpose               | Command                      |
| --------------------- | ---------------------------- |
| Install CocoaPods     | `sudo gem install cocoapods` |
| Set up CocoaPods      | `pod setup --verbose`        |
| Verify installation   | `pod --version`              |
| Clear Terminal screen | `clear`                      |

---

## Important Tips

* Use an **admin account** when installing CocoaPods.
* Terminal passwords are entered **blindly** (nothing appears on screen).
* Wait for the prompt to return before entering another command.
* Installation and setup may take several minutes depending on internet speed.
* Most installation issues can be solved by retrying the commands or consulting the troubleshooting guide.

### Outcome

After completing these steps and successfully running `pod --version`, CocoaPods is installed and ready for use in iOS development projects.
