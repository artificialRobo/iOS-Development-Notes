# Notes: Using the URLSession for Networking

## 1. What is Networking?

* **Networking** is the process of an app communicating with a web server to request and receive data.

<p align="center">
    <img src="assets/networkingThroughAppUsingAPIs.png" width="auto" style="border-radius: 1%">
</p>

* Example:

  * App sends a request to the **OpenWeatherMap server**.
  * Request includes query parameters such as city name (`q`) and API key (`appid`).
  * Server processes the request and returns the requested weather data.

---

## 2. Steps for Networking in Swift

### Step 1: Create a URL

* Convert a URL string into a `URL` object.
* Since URL strings can contain errors or typos, `URL(string:)` returns an **optional URL**.
* Use optional binding (`if let`) to safely unwrap it.

```swift
if let url = URL(string: urlString) {
    // use url
}
```

---

### Step 2: Create a URLSession

* `URLSession` is responsible for performing networking tasks.
* Think of it as the browser that handles requests.

```swift
let session = URLSession(configuration: .default)
```

---

### Step 3: Create a Data Task

* Assign a task to the session.
* The task retrieves data from the specified URL.
* A **completion handler** is provided to execute code after the request finishes.

```swift
let task = session.dataTask(with: url, completionHandler: handle)
```

---

### Step 4: Start the Task

* Newly created tasks start in a **suspended state**.
* Call `resume()` to begin the request.

```swift
task.resume()
```

---

## 3. The `performRequest` Method

Purpose:

* Receives a URL string.
* Performs all networking steps.

```swift
func performRequest(with urlString: String) {
    // Create URL
    // Create Session
    // Create Task
    // Start Task
}
```

---

## 4. What is a Completion Handler?

### Why is it needed?

* Network requests can take time (milliseconds to minutes).
* The app cannot pause and wait.
* Instead, it continues running and executes a completion handler when the request finishes.

### Completion Handler Parameters

When the request completes, it provides:

1. `Data?` → Returned data
2. `URLResponse?` → Server response
3. `Error?` → Error information (if something went wrong)

---

## 5. Creating a Handler Function

Example:

```swift
func handle(data: Data?,
            response: URLResponse?,
            error: Error?) {
}
```

* Matches the parameters expected by the completion handler.
* Passed to `dataTask()`.

---

## 6. Error Handling

Check for errors first:

```swift
if error != nil {
    print(error!)
    return
}
```

### Why return?

* Stops execution if the request failed.
* Prevents additional errors from processing invalid data.

---

## 7. Handling Returned Data

Use optional binding:

```swift
if let safeData = data {
}
```

### Convert Data to String

Data isn't easily readable when printed directly.

Convert it using UTF-8 encoding:

```swift
let dataString = String(data: safeData,
                        encoding: .utf8)
```

Then print it:

```swift
print(dataString)
```

---

## 8. HTTP vs HTTPS

### Problem

Using:

```text
http://
```

causes an App Transport Security error.

Error:

> Resource could not be loaded because App Transport Security requires a secure connection.

### Solution

Use:

```text
https://
```

instead.

### Why?

* HTTPS encrypts requests and responses.
* Protects API keys and transmitted data.
* Apple requires secure network connections by default.

---

## 9. Result

After switching to HTTPS:

* The app successfully requests weather data.
* OpenWeatherMap returns JSON data containing:

  * Coordinates
  * Weather description
  * Temperature
  * Other weather information

---

## 10. Key Concepts to Remember

### Networking Workflow

1. Create URL
2. Create URLSession
3. Create Data Task
4. Call `resume()`

### Important Swift Concepts

* `URL(string:)` returns an optional.
* Use `if let` for safe unwrapping.
* Network tasks are asynchronous.
* Completion handlers run after the task finishes.
* Always handle errors before processing data.
* Convert `Data` to a readable format when needed.
* Use **HTTPS**, not HTTP.

---

## Summary

Swift networking with `URLSession` involves creating a URL, creating a session, assigning a data task, and starting the task with `resume()`. Because network requests take time, a completion handler is used to process results asynchronously. Returned data, responses, and errors are handled inside the completion handler, and secure HTTPS connections are required for successful API requests. Future lessons introduce **closures**, which provide a more common and concise way to write completion handlers.
