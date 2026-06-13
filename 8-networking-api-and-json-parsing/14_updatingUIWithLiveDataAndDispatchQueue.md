# Notes: Updating UI with Live Weather Data & DispatchQueue

## Objective

* Display live weather data from OpenWeatherMap in the app's UI.
* Learn why and how to use `DispatchQueue.main.async` when updating UI elements.

---

## 1. Updating the Temperature Label

Inside `didUpdateWeather`, use the weather data to update the temperature label:

```swift
temperatureLabel.text = weather.temperatureString
```

### `temperatureString`

* Comes from `WeatherModel`.
* Temperature is rounded to 1 decimal place.
* Converted to a `String` for display in a `UILabel`.

---

## 2. Runtime Crash: UI Updates from Background Thread

### Error Message

```
UILabel.text must be used from main thread only
```

### Why It Happens

* Weather data is fetched through a network request.
* Network requests are long-running tasks.
* These tasks run in the **background thread** to keep the app responsive.
* The completion handler executes on that background thread.
* UIKit components (`UILabel`, `UIImageView`, etc.) can only be updated from the **main thread**.

---

## 3. Completion Handlers and Background Execution

### Purpose of Completion Handlers

* Used for tasks that take time (e.g., networking).
* Allow the app to continue responding to user interactions while waiting for data.

### Without Background Execution

* The UI would freeze while waiting for the network response.
* Users might think the app has crashed.

---

## 4. Using `DispatchQueue.main.async`

To safely update UI elements, wrap UI code inside:

```swift
DispatchQueue.main.async {
    self.temperatureLabel.text = weather.temperatureString
}
```

### What It Does

* Sends the UI update task to the main thread.
* Ensures UIKit components are updated safely.
* Prevents runtime crashes.

### Note

Inside the closure, use `self` when referencing properties:

```swift
self.temperatureLabel.text = weather.temperatureString
```

---

## 5. Updating the Weather Condition Image

Set the image for `conditionImageView` using SF Symbols:

```swift
self.conditionImageView.image =
    UIImage(systemName: weather.conditionName)
```

### How It Works

* `conditionName` is provided by `WeatherModel`.
* It converts OpenWeatherMap weather condition IDs into SF Symbol names.
* `UIImage(systemName:)` creates an image from the SF Symbol string.

---

## 6. WeatherModel's Role

`WeatherModel` provides:

#### `temperatureString`

* Formatted temperature value.

#### `conditionName`

* Converts weather condition codes into SF Symbol names.
* Makes it easy to display weather icons.

---

## Code Example

```swift
func didUpdateWeather(_ weatherManager: WeatherManager, weather: WeatherModel) {

    DispatchQueue.main.async {

        self.temperatureLabel.text = weather.temperatureString

        self.conditionImageView.image =
            UIImage(systemName: weather.conditionName)
    }
}
```

### Result

* Temperature label updates with live weather data.
* Weather icon changes according to conditions.
* No crashes caused by background-thread UI updates.

---

## Key Takeaways

* Network requests run on background threads.
* Completion handlers execute after the network task finishes.
* UIKit elements must only be updated on the main thread.
* Use `DispatchQueue.main.async` for all UI updates after networking.
* SF Symbols can be displayed using:

  ```swift
  UIImage(systemName:)
  ```
* `WeatherModel` helps format weather data for the UI.