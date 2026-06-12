# Notes: Typealiases, and Delegates & Protocols Challenge in Swift

## 1. Typealiases: Codable, Decodable, and Encodable

* `Decodable` allows JSON data to be converted into Swift objects.
* `Encodable` allows Swift objects to be converted into JSON.
* `Codable` is a **typealias** that combines both:

  ```swift
  typealias Codable = Decodable & Encodable
  ```
* Using `Codable` saves time when a model needs both encoding and decoding capabilities.

---

## 2. Returning Data from `parseJSON()`

* After decoding JSON, a `WeatherModel` object is created.
* The method should return the created weather object:

  ```swift
  return weather
  ```
* However, decoding can fail and enter the `catch` block.
* In that case, there is no weather object to return.

### Solution: Return an Optional

```swift
func parseJSON(_ weatherData: Data) -> WeatherModel?
```

* Return `nil` when decoding fails:

  ```swift
  catch {
      print(error)
      return nil
  }
  ```

---

## 3. Optional Binding

* Since `parseJSON()` now returns an optional, unwrap it before use:

  ```swift
  if let weather = parseJSON(weatherData) {
      // use weather
  }
  ```
* `weather` inside the `if let` block is a fully unwrapped `WeatherModel`.

---

## 4. Why Not Directly Reference `WeatherViewController`?

A direct approach would be:

```swift
weatherVC.didUpdateWeather(weather)
```

### Problem:

* `WeatherManager` becomes tightly coupled to `WeatherViewController`.
* The code becomes less reusable.
* Future projects would require modifications to `WeatherManager`.

---

## 5. Delegate Pattern Solution

Use a delegate instead of directly referencing another class.

### Benefits:

* Keeps `WeatherManager` reusable.
* Separates responsibilities.
* Any class can receive weather updates by becoming the delegate.

---

## 6. Creating the Delegate Protocol

```swift
protocol WeatherManagerDelegate {
    func didUpdateWeather(weather: WeatherModel)
}
```

### Protocol Requirement:

Any class adopting this protocol must implement:

```swift
func didUpdateWeather(weather: WeatherModel)
```

---

## 7. Adding a Delegate Property

Inside `WeatherManager`:

```swift
var delegate: WeatherManagerDelegate?
```

* Optional because a delegate may or may not be assigned.

---

## 8. Calling the Delegate Method

After successfully parsing weather data:

```swift
self.delegate?.didUpdateWeather(weather: weather)
```

### Notes:

* `self` is required because the call occurs inside a closure.
* Optional chaining (`?.`) ensures the method is called only if a delegate exists.

---

## 9. Adopting the Protocol in `WeatherViewController`

```swift
class WeatherViewController: UIViewController, WeatherManagerDelegate {
    
    func didUpdateWeather(weather: WeatherModel) {
        print(weather.temperature)
    }
}
```

* The controller conforms to `WeatherManagerDelegate`.
* It implements the required method.

---

## 10. Setting the Delegate

A common mistake is forgetting to assign the delegate:

```swift
weatherManager.delegate = self
```

### Why?

* Without this assignment, `delegate` remains `nil`.
* Delegate methods will never be called.

---

## 11. Data Flow Summary

```text
-> OpenWeather API
-> JSON Response
-> WeatherManager
-> parseJSON()
-> WeatherModel
-> delegate?.didUpdateWeather(...)
-> WeatherViewController
-> Update UI (temperature, condition image, etc.)
```

---

## Key Takeaways

* `Codable = Decodable + Encodable`.
* Return an optional model (`WeatherModel?`) when decoding may fail.
* Use optional binding (`if let`) to safely unwrap results.
* Avoid directly connecting `WeatherManager` to `WeatherViewController`.
* Use the **Delegate Pattern** to keep code reusable and loosely coupled.
* Create a protocol, assign a delegate, and notify it when weather data is available.
* Always remember:

  ```swift
  weatherManager.delegate = self
  ```

  otherwise delegate methods won't execute.
