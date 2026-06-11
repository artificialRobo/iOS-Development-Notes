# Notes: OpenWeather API and URL Parameters

## 1. What is an API?

**API = Application Programming Interface**

An API is a set of commands, functions, protocols, and objects that allow:

* Developers to build software more easily.
* Applications to communicate with external systems.

### Benefits of APIs

* Provide standard functionality.
* Save developers from writing everything from scratch.
* Create a consistent way to interact with services.

### Examples

* Apple APIs (e.g., `AVAudioPlayer`) help developers add features like audio playback.
* External APIs (e.g., OpenWeatherMap, Facebook) provide data from external services.

---

## 2. APIs as a Contract

An API can be thought of as a **contract** between:

* The developer (API user)
* The API provider

### Developer agrees to:

* Follow the API documentation.
* Use the required parameters and formats.

### API provider agrees to:

* Maintain the API structure.
* Return data in the expected format.

**Example:**

* User enters a city name.
* App sends a request to OpenWeatherMap.
* OpenWeatherMap returns weather data.

---

## 3. OpenWeatherMap API

OpenWeatherMap provides:

* Current weather
* Hourly forecasts
* Daily forecasts
* Other weather-related data

Documentation:

* Current weather can be requested by:

  * City name
  * City ID
  * Coordinates (latitude/longitude)
  * ZIP code

---

## 4. API Keys

Most public APIs require an **API Key**.

### Purpose

* Identifies the developer.
* Prevents abuse of the service.
* Tracks API usage.

### Steps

1. Create an account.
2. Navigate to **API Keys** section.
3. Copy your unique API key.
4. Store it securely.

> API keys may take a few minutes or hours to become active.

---

## 5. Structure of an API Request

Example URL:

```text
api.openweathermap.org/data/2.5/weather?q=London&appid=YOUR_API_KEY
```

### Components

#### Base URL

```text
api.openweathermap.org/data/2.5/weather
```

#### Query Parameters

Start with:

```text
?
```

Then add parameters:

```text
parameter=value
```

Multiple parameters are separated by:

```text
&
```

Example:

```text
?q=London&appid=YOUR_API_KEY
```

### Important Parameters

| Parameter | Purpose           |
| --------- | ----------------- |
| q         | City name         |
| appid     | API key           |
| units     | Temperature units |

---

## 6. Temperature Units

OpenWeatherMap returns temperatures in **Kelvin** by default.

Example:

```text
293
```

This is Kelvin, not Celsius or Fahrenheit.

### Convert Units

Metric (Celsius):

```text
&units=metric
```

Imperial (Fahrenheit):

```text
&units=imperial
```

Example:

```text
?q=London&appid=YOUR_API_KEY&units=metric
```

---

## 7. JSON Response

API responses are returned in **JSON format**.

### Easier JSON Viewing

Chrome Extension:

**JSON View Awesome**

Benefits:

* Formats raw JSON into a readable tree structure.
* Makes debugging easier.

---

## 8. Creating a WeatherManager

Create a new Swift file:

```swift
WeatherManager.swift
```

Create a struct:

```swift
struct WeatherManager {

}
```

### Store Base URL

```swift
let weatherURL = "YOUR_BASE_URL"
```

The city name is not included in the base URL because it changes dynamically.

---

## 9. Building the URL Dynamically

Create a method:

```swift
func fetchWeather(cityName: String) {

}
```

Construct the URL:

```swift
let urlString = "\(weatherURL)&q=\(cityName)"
```

### Why?

* `weatherURL` remains constant.
* User-entered city names are appended dynamically.

---

## 10. Using WeatherManager in ViewController

Create an instance:

```swift
var weatherManager = WeatherManager()
```

Get text from the search field:

```swift
if let city = searchTextField.text {
    weatherManager.fetchWeather(cityName: city)
}
```

### Optional Unwrapping

`searchTextField.text` is an optional:

```swift
String?
```

Use:

```swift
if let city = searchTextField.text
```

to safely unwrap it into a regular `String`.

---

## 11. Debugging the URL

Print the generated URL:

```swift
print(urlString)
```

Example output:

```text
https://api.openweathermap.org/...&units=metric&q=Paris
```

### Testing

1. Copy the printed URL.
2. Paste it into a browser.
3. Verify that weather data is returned.

---

## Key Takeaways

* APIs allow apps to communicate with external services.
* APIs function as a contract between developers and providers.
* OpenWeatherMap requires an API key.
* Requests are built using query parameters.
* Important parameters:

  * `appid`
  * `q`
  * `units`
* Temperatures default to Kelvin; use `metric` or `imperial`.
* Build URLs dynamically using user input.
* Use optional unwrapping when retrieving text from a UITextField.
* Printing and testing URLs is a useful debugging technique.
* The next step after building the URL is **networking**, which involves actually fetching data from the internet.
