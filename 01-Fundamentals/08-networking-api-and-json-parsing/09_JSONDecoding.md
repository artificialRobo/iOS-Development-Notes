# Notes: Parsing JSON Responses from OpenWeatherMap

## 1. Converting a Completion Handler to a Closure

* Replace a separate completion handler method with a Swift closure.
* Use `URLSession.dataTask(with:completionHandler:)`.
* Xcode can automatically create a trailing closure.
* Closure parameters:

  ```swift
  { data, response, error in
      // code
  }
  ```
* Move code from the old handler method into the closure.
* Benefits:

  * Cleaner code
  * More "Swifty"
  * Keeps related logic together

---

## 2. Understanding JSON

### What is JSON?

* **JSON = JavaScript Object Notation**
* A lightweight format used to transfer data over the internet.
* Represents objects using:

  * Curly braces `{ }`
  * Key-value pairs
  * Commas separating properties

Example:

```json
{
  "name": "Paris",
  "temp": 25.4
}
```

### Why JSON?

* Compact and efficient for network transfer.
* More popular than XML for APIs.
* Can be converted into native objects in different languages.

---

## 3. Parsing JSON into Swift Objects

Instead of working with unreadable raw data:

```swift
Data
```

Convert JSON into Swift structs using `JSONDecoder`.

### Create a Parsing Method

```swift
func parseJSON(_ weatherData: Data) {
    
}
```

Call it inside the completion handler:

```swift
self.parseJSON(safeData)
```

---

## 4. Why `self` is Required Inside Closures

Normally Swift automatically inserts `self`.

Example:

```swift
performRequest()
```

is actually:

```swift
self.performRequest()
```

Inside closures, Swift requires explicit `self` to avoid ambiguity:

```swift
self.parseJSON(safeData)
```

---

## 5. Making Models Decodable

Create a model file:

```swift
struct WeatherData: Decodable {
    let name: String
}
```

### Decodable Protocol

* Allows Swift to decode JSON into structs.
* Property names must match JSON keys exactly.

---

## 6. Using JSONDecoder

Create a decoder:

```swift
let decoder = JSONDecoder()
```

Decode JSON:

```swift
let decodedData = try decoder.decode(
    WeatherData.self,
    from: weatherData
)
```

### Why `.self`?

`decode()` expects a **type**, not an object.

```swift
WeatherData.self
```

refers to the type itself.

---

## 7. Error Handling with `do-catch`

`decode()` can throw errors.

Use:

```swift
do {
    let decodedData = try decoder.decode(
        WeatherData.self,
        from: weatherData
    )
} catch {
    print(error)
}
```

### Purpose

* Handles invalid JSON
* Prevents app crashes
* Displays decoding errors

---

## 8. Accessing Decoded Data

After decoding:

```swift
print(decodedData.name)
```

Example output:

```text
Belgrade
```

This confirms data is coming from the API, not user input.

---

## 9. Decoding Nested JSON Objects

JSON often contains nested objects.

Example:

```json
{
  "main": {
    "temp": 22.5
  }
}
```

### Create a Nested Struct

```swift
struct WeatherData: Decodable {
    let main: Main
}

struct Main: Decodable {
    let temp: Double
}
```

### Access Temperature

```swift
decodedData.main.temp
```

---

## 10. Important Rule for Property Names

Property names must match JSON keys exactly.

Correct:

```swift
let temp: Double
```

Incorrect:

```swift
let temperature: Double
```

Without custom coding keys, mismatched names cause decoding failures.

---

## 11. Decoding Arrays in JSON

Example:

```json
"weather": [
  {
    "description": "clear sky"
  }
]
```

### Swift Models

```swift
struct WeatherData: Decodable {
    let weather: [Weather]
}

struct Weather: Decodable {
    let description: String
}
```

### Access First Item

```swift
decodedData.weather[0].description
```

or

```swift
decodedData.weather.first?.description
```

---

## 12. JSON Structure Mapping Strategy

### Step 1: Inspect JSON

Example:

```json
{
  "name": "Paris",
  "main": {
    "temp": 22.5
  },
  "weather": [
    {
      "description": "clear sky"
    }
  ]
}
```

### Step 2: Create Matching Structs

```swift
struct WeatherData: Decodable {
    let name: String
    let main: Main
    let weather: [Weather]
}

struct Main: Decodable {
    let temp: Double
}

struct Weather: Decodable {
    let description: String
}
```

### Step 3: Decode

```swift
let decodedData = try decoder.decode(
    WeatherData.self,
    from: weatherData
)
```

### Step 4: Use the Data

```swift
print(decodedData.name)
print(decodedData.main.temp)
print(decodedData.weather[0].description)
```

---

# Key Takeaways

* Use **closures** instead of separate completion handler methods.
* JSON is the standard format for API responses.
* Use **Decodable** structs to describe JSON structure.
* Use **JSONDecoder** to convert JSON into Swift objects.
* Nested JSON requires nested structs.
* JSON arrays become Swift arrays.
* Property names must match JSON keys.
* Use `do-try-catch` for safe decoding.
* Use explicit `self` when calling methods inside closures.
* Access decoded data like normal Swift properties:

  ```swift
  decodedData.main.temp
  decodedData.weather[0].description
  ```
