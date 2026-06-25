# Notes: Weather Model & Computed Properties in Swift

## 1. Getting Weather Condition IDs from OpenWeatherMap

* OpenWeatherMap provides **weather condition codes (IDs)** that represent different weather conditions.
* Example:

  * `200–232` → Thunderstorms
  * `803` → Broken clouds (51–84% cloud coverage)
* These IDs are found in the weather data returned by the API.

### Updating the Weather Struct

Instead of using the weather description:

```swift
description: String
```

Use:

```swift
id: Int
```

Accessing the weather ID:

```swift
let id = decodedData.weather[0].id
```

---

## 2. Mapping Weather IDs to SF Symbols

### Goal

Convert weather condition IDs into SF Symbol names so the app can display appropriate weather icons.

Example mappings:

| Weather Condition | SF Symbol    |
| ----------------- | ------------ |
| Thunderstorm      | `cloud.bolt` |
| Rain              | `cloud.rain` |
| Clouds            | `cloud`      |
| Sunny             | `sun.max`    |

### Using a Switch Statement

Create a function:

```swift
func getConditionName(weatherId: Int) -> String
```

Use a `switch` statement with ranges:

```swift
switch weatherId {
case 200...232:
    return "cloud.bolt"
case 300...321:
    return "cloud.drizzle"
case 500...531:
    return "cloud.rain"
default:
    return "cloud"
}
```

### Key Concept

* Switch statements can match **ranges** using `...`.
* Useful for grouping multiple weather codes under a single icon.

---

## 3. Refactoring with MVC

As the app grows, code becomes harder to manage.

### Solution

Create a separate model file:

```swift
WeatherModel.swift
```

### WeatherModel Structure

```swift
struct WeatherModel {
    let conditionId: Int
    let cityName: String
    let temperature: Double
}
```

### Benefits

* Keeps weather-related logic inside the model.
* Makes `WeatherManager` cleaner and easier to maintain.
* Follows the **MVC (Model-View-Controller)** design pattern.

---

## 4. Creating a Weather Object

Extract values from decoded data:

```swift
let id = decodedData.weather[0].id
let temp = decodedData.main.temp
let name = decodedData.name
```

Create a weather model:

```swift
let weather = WeatherModel(
    conditionId: id,
    cityName: name,
    temperature: temp
)
```

---

## 5. Computed Properties

### What is a Computed Property?

A property whose value is calculated rather than stored.

### Stored Properties

```swift
let conditionId: Int
let cityName: String
let temperature: Double
```

These simply store data.

### Computed Property Example

```swift
var conditionName: String {
    switch conditionId {
    case 200...232:
        return "cloud.bolt"
    default:
        return "cloud"
    }
}
```

Now you can access:

```swift
weather.conditionName
```

instead of:

```swift
weather.getConditionName(weatherId: id)
```

### Advantages

* Cleaner code
* Easier to read
* Logic belongs to the model

---

## 6. General Syntax of Computed Properties

```swift
var propertyName: DataType {
    return computedValue
}
```

Example:

```swift
var aProperty: Int {
    return 2 + 5
}
```

Result:

```swift
aProperty == 7
```

### Rules

* Must use `var` (not `let`)
* Must specify a data type
* Must return a value

---

## 7. Temperature String Computed Property

### Goal

Convert a temperature `Double` into a formatted string with one decimal place.

### Computed Property

```swift
var temperatureString: String {
    return String(format: "%.1f", temperature)
}
```

### Usage

```swift
print(weather.temperatureString)
```

### Example Output

If:

```swift
temperature = 25.678
```

Then:

```swift
temperatureString = "25.7"
```

### Benefit

The temperature is already formatted and ready to display in a label.

---

# Key Takeaways

* OpenWeatherMap uses **condition IDs** to represent weather types.
* Use **switch statements with ranges** to map IDs to SF Symbols.
* Move weather-related logic into a **WeatherModel** for better MVC structure.
* Use **computed properties** to calculate values dynamically.
* `conditionName` and `temperatureString` are examples of computed properties that make the code cleaner and easier to use.
