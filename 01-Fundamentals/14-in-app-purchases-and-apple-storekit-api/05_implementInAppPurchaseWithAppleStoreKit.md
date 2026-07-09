# Notes: Implementing In-App Purchases with StoreKit

## Goal

* Trigger an **in-app purchase** when the user taps **"Get More Quotes"**.
* Use **StoreKit** to communicate with the App Store.

---

## 1. Create the Product Identifier

* Define a constant for the product ID.
* The product ID must exactly match the one created in **App Store Connect → Features → In-App Purchases**.

Example:

```swift
let productID = "com.yourapp.premiumquotes"
```

**Purpose:**

* Identifies which in-app purchase the app is requesting from Apple.

---

## 2. Import StoreKit

```swift
import StoreKit
```

**StoreKit** provides all the APIs needed for:

* In-app purchases
* Payment processing
* Transaction handling

---

## 3. Check if the User Can Make Purchases

Before requesting payment:

```swift
if SKPaymentQueue.canMakePayments() {
    // Continue with purchase
} else {
    print("User can't make payments")
}
```

**Why?**

* Some devices have **Parental Controls/Screen Time restrictions** that disable purchases.

---

## 4. Create a Payment Request

Create an `SKMutablePayment` object:

```swift
let paymentRequest = SKMutablePayment()
paymentRequest.productIdentifier = productID
```

This tells the App Store:

* Which product the user wants to purchase.

---

## 5. Add the Payment to the Queue

Submit the request:

```swift
SKPaymentQueue.default().add(paymentRequest)
```

**Result:**

* StoreKit displays Apple's purchase dialog.
* The user authenticates the purchase.

### Payment Flow

```
User taps "Get More Quotes"
        ↓
Create Payment Request
        ↓
Add Request to SKPaymentQueue
        ↓
App Store handles payment
        ↓
User confirms purchase
        ↓
App receives transaction result
```

---

## 6. Observe Payment Transactions

Simply sending a payment request isn't enough.

The app must know:

* Purchase succeeded
* Purchase failed
* Purchase restored

To do this, conform to:

```swift
SKPaymentTransactionObserver
```

---

## 7. Add the Observer Protocol

Example:

```swift
class QuoteTableViewController:
UITableViewController,
SKPaymentTransactionObserver
```

This allows the class to receive transaction updates.

---

## 8. Implement the Required Delegate Method

```swift
paymentQueue(_:updatedTransactions:)
```

This method is automatically called whenever a transaction changes state.

---

## 9. Register the Observer

Inside `viewDidLoad()`:

```swift
SKPaymentQueue.default().add(self)
```

This registers the current view controller to receive payment updates.

**Note:**
There are two different `.add()` methods:

* `.add(payment)` → Adds a payment request.
* `.add(observer)` → Registers a transaction observer.

Swift distinguishes them by their parameter types.

---

## 10. Process Transactions

Loop through every transaction:

```swift
for transaction in transactions {
    ...
}
```

Multiple transactions may exist in the payment queue.

---

## 11. Check Transaction State

### Successful Purchase

```swift
if transaction.transactionState == .purchased
```

Actions:

* Unlock premium features.
* Print:

  ```
  Transaction successful!
  ```

---

### Failed Purchase

```swift
else if transaction.transactionState == .failed
```

Possible reasons:

* User cancelled the purchase.
* Payment error occurred.

Print:

```
Transaction failed!
```

---

## Other Transaction States

StoreKit also supports:

* `.purchasing`

  * Purchase is currently being processed.

* `.restored`

  * Restores purchases after reinstalling the app or switching devices.

---

## Complete Purchase Flow

```
Tap "Get More Quotes"
        ↓
Check canMakePayments()
        ↓
Create SKMutablePayment
        ↓
Set productIdentifier
        ↓
Add payment to SKPaymentQueue
        ↓
Apple shows purchase popup
        ↓
User authenticates purchase
        ↓
paymentQueue(updatedTransactions:)
        ↓
Check transactionState
        ↓
Purchased / Failed / Restored
```

---

## Testing In-App Purchases

**Important:**

* Does **not** work in the iOS Simulator.
* Test on a **physical iPhone or iPad**.

To avoid paying real money during testing:

* Create an **Apple Sandbox Test User**.
* Use the sandbox account to simulate purchases without charges.

---

## Key Takeaways

* Store the App Store product ID in a constant.
* Import **StoreKit**.
* Verify purchases are allowed using `SKPaymentQueue.canMakePayments()`.
* Create an `SKMutablePayment` with the product ID.
* Add the payment to `SKPaymentQueue`.
* Conform to `SKPaymentTransactionObserver`.
* Register the observer with `SKPaymentQueue.default().add(self)`.
* Handle transaction updates in `paymentQueue(_:updatedTransactions:)`.
* Check transaction states (`.purchased`, `.failed`, `.restored`, `.purchasing`).
* Always test on a **real device** using a **Sandbox Test User**.
