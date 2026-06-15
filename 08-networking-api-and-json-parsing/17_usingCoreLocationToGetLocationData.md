# Notes: Adding Current Location Weather Feature to the Clima App

## 1. Using Core Location

* Import **CoreLocation** framework.
* Create a location manager:

```swift
let locationManager = CLLocationManager()
```

* The `CLLocationManager` is responsible for accessing the device's GPS location.

---

## 2. Requesting User Permission

Because location data is private, apps must request permission before accessing it.

```swift
locationManager.requestWhenInUseAuthorization()
```

### Update Info.plist

Add:

**Privacy - Location When In Use Usage Description**

Example value:

> "We need your location to get the current weather for where you are."

This text appears in the permission popup shown to the user.

---

## 3. Requesting the Current Location

After permission is granted:

```swift
locationManager.requestLocation()
```

### Why use `requestLocation()`?

* Gets location once.
* Ideal for weather apps.

### Alternative: `startUpdatingLocation()`

* Continuously tracks location.
* Better for navigation or fitness apps.

---

## 4. Using Delegates

Location data is returned through delegate methods.

Adopt the protocol:

```swift
CLLocationManagerDelegate
```

Example extension:

```swift
extension WeatherViewController: CLLocationManagerDelegate {
    
}
```

---

## 5. Set the Delegate

Before requesting location:

```swift
locationManager.delegate = self
```

Important:

* Set the delegate **before** calling `requestLocation()`.
* Otherwise the app may crash.

---

## 6. Required Delegate Methods

### Successful Location Update

```swift
func locationManager(
    _ manager: CLLocationManager,
    didUpdateLocations locations: [CLLocation]
) {
    print("Got location data")
}
```

### Error Handling

```swift
func locationManager(
    _ manager: CLLocationManager,
    didFailWithError error: Error
) {
    print(error)
}
```

Both methods are required when using `requestLocation()`.

---

## 7. Getting Latitude and Longitude

Retrieve the most accurate location:

```swift
if let location = locations.last {
    let latitude = location.coordinate.latitude
    let longitude = location.coordinate.longitude
}
```

Why `locations.last`?

* Location Manager may provide multiple location updates.
* The last location is usually the most accurate.

---

## 8. Testing Location in Simulator

In Xcode:

**Debug → Location**

Options include:

* Apple Headquarters
* Custom Location
* Other preset locations

To apply changes, you may need to:

1. Delete the app from the simulator.
2. Run the app again.

---

## 9. OpenWeather API with Coordinates

Weather can be requested using coordinates instead of a city name.

Example URL:

```text
...&lat=51&lon=-0.1
```

Remember to Use:

* `lat`
* `lon`

Not:

* `long`

---

## 10. Creating a New Weather Fetch Method

Add an overloaded method:

```swift
func fetchWeather(
    latitude: CLLocationDegrees,
    longitude: CLLocationDegrees
)
```

Build URL:

```swift
let urlString =
"\(weatherURL)&lat=\(latitude)&lon=\(longitude)"
```

Then:

```swift
performRequest(with: urlString)
```

---

## 11. Fetching Weather from Current Location

Inside:

```swift
didUpdateLocations
```

Call:

```swift
weatherManager.fetchWeather(
    latitude: latitude,
    longitude: longitude
)
```

The existing networking and JSON parsing code can be reused.

---

## 12. Updating the City Label

OpenWeather returns a city name in the JSON response.

Update UI:

```swift
cityLabel.text = weather.cityName
```

This allows:

* Current location → displays detected city.
* Manual city search → displays searched city.

---

## 13. Location Button Challenge Solution

Create an IBAction:

```swift
@IBAction func locationPressed(_ sender: UIButton) {
    
}
```

When pressed:

```swift
locationManager.requestLocation()
```

This requests the current location again and refreshes weather data.

---

## 14. Stopping Location Updates

After receiving a location:

```swift
locationManager.stopUpdatingLocation()
```

Flow:

1. Set delegate.
2. Request location.
3. Receive location.
4. Stop updating.
5. Fetch weather.

This allows future location requests to work properly when the user presses the location button.

---

## Key Concepts Learned

### Core Location

* `CLLocationManager`
* GPS access
* Permission handling

### Protocols & Delegates

* `CLLocationManagerDelegate`
* Delegate methods for success and failure

### Extensions

* Organizing delegate code separately

### Networking

* API requests using `URLSession`

### JSON Parsing

* Converting API responses into Swift models

### Weather Features Implemented

- Search weather by city name
- Get weather from current location
- Display current city name
- Refresh weather using location button
- Handle location permissions and errors

---

## App Flow

```text
-> App Launch
-> Request Location Permission
-> Request Current Location
-> didUpdateLocations
-> Get Latitude & Longitude
-> Fetch Weather from OpenWeather API
-> Parse JSON
-> Update UI
-> Show:
- Temperature
- Weather Icon
- City Name
```

This lesson completed the weather app by enabling **current-location weather retrieval** while reinforcing **Core Location, delegates, networking, JSON parsing, and UI updates**.
