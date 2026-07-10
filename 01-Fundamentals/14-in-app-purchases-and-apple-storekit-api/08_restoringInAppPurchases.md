# Notes: Restoring In-App Purchases (iOS StoreKit)

## Why Restore Purchases is Important

* Users may:

  * Get a new iPhone.
  * Update iOS.
  * Reinstall the app.
* Reinstalling removes the app's **UserDefaults**, so purchase status stored locally is lost.
* A **Restore Purchases** feature allows users to regain access to previously purchased content.

### Apple's Requirements

* Apple requires a **Restore Purchases** button for apps with non-consumable in-app purchases.
* The button should be:

  * Easy to find (or clearly explained during App Store review).
  * Otherwise, app approval may be delayed.

---

## How Restore Purchases Works

1. User taps the **Restore** button.
2. Call:

```swift
SKPaymentQueue.default().restoreCompletedTransactions()
```

3. StoreKit contacts Apple's servers.
4. Apple checks the user's Apple ID for previous purchases.
5. If a purchase exists, StoreKit returns a transaction with:

```swift
transaction.transactionState == .restored
```

---

## Handling Restored Transactions

When the transaction state is `.restored`:

* Unlock premium content.
* Print a confirmation message.
* Finish the transaction.

Example:

```swift
if transaction.transactionState == .restored {
    showPremiumQuotes()
    print("Transaction restored")
    SKPaymentQueue.default().finishTransaction(transaction)
}
```

---

## Testing Restore Purchases

1. Buy the premium content.
2. Delete the app.
3. Reinstall the app.
4. UserDefaults are reset.
5. Tap **Restore**.
6. Premium content becomes available again.

---

## Important Improvement

Originally:

* `UserDefaults` was only updated after a successful purchase.

Problem:

* After reinstalling the app, restoring the purchase unlocks content temporarily.
* Since `UserDefaults` isn't updated, the app forgets the purchase the next time it launches.

**Solution:**
Move the `UserDefaults` update into the shared method that unlocks premium content (`showPremiumQuotes()`).

Example:

```swift
func showPremiumQuotes() {
    UserDefaults.standard.set(true, forKey: "isPurchased")
    tableView.reloadData()
}
```

This ensures both:

* New purchases
* Restored purchases

save the purchase status locally.

---

## UI Improvement

After a successful restore:

* Remove the **Restore** button since it is no longer needed.

Example:

```swift
navigationItem.rightBarButtonItem = nil
```

or

```swift
navigationItem.setRightBarButton(nil, animated: true)
```

---

## Workflow Summary

**Purchase**

* User buys product.
* Unlock premium content.
* Save purchase status in `UserDefaults`.

**Restore**

* User taps Restore.
* Call `restoreCompletedTransactions()`.
* Apple verifies previous purchases.
* Transaction state becomes `.restored`.
* Unlock premium content.
* Save purchase status in `UserDefaults`.
* Finish the transaction.
* Remove the Restore button.

---

## Key StoreKit Methods

* `SKPaymentQueue.default()`
* `restoreCompletedTransactions()`
* `finishTransaction(transaction)`

### Key Transaction States

* `.purchased` → New purchase completed.
* `.restored` → Previous purchase successfully restored.

---

## Module Recap

This module covered:

* Setting up in-app purchases.
* Processing purchases.
* Unlocking premium content.
* Restoring previous purchases.
* Saving purchase status using `UserDefaults`.
* Improving the user experience after a successful restore.
