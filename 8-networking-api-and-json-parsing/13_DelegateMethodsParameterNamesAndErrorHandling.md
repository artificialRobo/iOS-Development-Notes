# Notes: Delegate Methods, Parameter Names, and Error Handling

## 1. Improving Delegate Method Design

* Follow Apple's delegate method conventions.
* The first parameter in a delegate method should identify the object that triggered the event.
* For the weather app, the triggering object is `WeatherManager`.

**Before:**

```swift
didUpdateWeather(weather: WeatherModel)
```

**After:**

```swift
didUpdateWeather(_ weatherManager: WeatherManager, weather: WeatherModel)
```

* Update both:

  * The protocol definition.
  * Any method calls using the delegate.

**Delegate Call:**

```swift
delegate.didUpdateWeather(self, weather: weather)
```

* `self` refers to the current `WeatherManager` instance.

---

## 2. Using Omitted External Parameter Names

* Use `_` to remove unnecessary external parameter names.
* Makes method calls cleaner and more readable.

**Example:**

```swift
func parseJSON(_ weatherData: Data)
```

Instead of:

```swift
parseJSON(weatherData: safeData)
```

Use:

```swift
parseJSON(safeData)
```

---

## 3. Creating More Readable Function Names

* Swift encourages method names that read naturally in English.

**Before:**

```swift
performRequest(urlString: urlString)
```

**After:**

```swift
func performRequest(with urlString: String)
```

**Call:**

```swift
performRequest(with: urlString)
```

Benefits:

* Cleaner syntax.
* Easier to understand.
* More maintainable for future developers.

---

## 4. Adding Error Handling Through Delegation

Create a new delegate method:

```swift
func didFailWithError(error: Error)
```

Purpose:

* Notify the delegate when something goes wrong in `WeatherManager`.
* Pass errors out instead of handling them internally.

---

## 5. Handling Network Errors

Instead of printing errors directly:

```swift
print(error)
```

Use:

```swift
self.delegate?.didFailWithError(error: error)
```

This allows the delegate to decide how to respond.

Possible causes:

* No internet connection.
* Network request failures.
* Server issues.

---

## 6. Handling JSON Parsing Errors

Errors can also occur while decoding JSON.

Inside the `catch` block:

```swift
delegate?.didFailWithError(error: error)
```

Possible causes:

* Invalid JSON structure.
* Mismatch between JSON and data model.
* Decoding failures.

---

## 7. Implementing Error Handling in the View Controller

Since the protocol now requires it, implement:

```swift
func didFailWithError(error: Error) {
    print(error)
}
```

Current approach:

* Print errors to the console for debugging.

Future possibilities:

* Show alerts to users.
* Display friendly error messages.
* Retry failed requests.

---

## Key Takeaways

* Delegate methods should identify the object that triggered the event.
* Use `_` to omit unnecessary external parameter names.
* Design method names to read naturally in English.
* Add delegate methods for error reporting.
* Pass network and parsing errors back to the delegate.
* Handle errors in the view controller, typically through logging or user feedback.
