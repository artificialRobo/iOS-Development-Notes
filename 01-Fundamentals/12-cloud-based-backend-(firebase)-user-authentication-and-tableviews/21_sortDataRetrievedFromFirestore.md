# Notes: Sort Data Retrieved from Firestore

## Objective

* Display chat messages in the order they were sent (chronological order).
* Achieve this by storing a timestamp with each message and sorting messages by that timestamp.

---

## 1. Add a Timestamp to Each Message

When saving a message to Firestore, store three fields:

* `sender`
* `body`
* `date`

Example:

```swift
[
    "sender": ...,
    "body": ...,
    "date": Date().timeIntervalSince1970
]
```

### `Date().timeIntervalSince1970`

* Returns the number of **seconds since January 1, 1970 (Unix Epoch)**.
* Commonly used as a timestamp.
* Makes it easy to compare and sort dates.

---

## 2. Delete Old Documents

Previously stored messages don't contain the new `date` field.

Therefore:

* Delete the existing `messages` collection.
* Create new messages so every document includes:

  * `sender`
  * `body`
  * `date`

---

## 3. Verify the Timestamp

After sending new messages:

* Open Firestore.
* Each document should contain a numeric `date` value.
* This timestamp will be used for sorting instead of the document ID.

---

## 4. Sort Messages

Firestore provides the `order(by:)` method.

Example:

```swift
db.collection(K.FStore.collectionName)
    .order(by: K.FStore.dateField)
    .addSnapshotListener { ... }
```

### Notes

* Sorts messages using the `date` field.
* Default order is **ascending** (oldest → newest).
* Can also sort in descending order.
* Firestore also supports:

  * `limit()`
  * additional query methods
  * multiple query options

---

## 5. Method Chaining

Firestore queries are often written using chained methods.

Example:

```swift
db.collection(...)
    .order(by: ...)
    .addSnapshotListener(...)
```

Formatting each method on a new line improves readability.

---

## 6. Result

Messages now appear:

* A
* B
* C

in the exact order they were sent, regardless of the random Firestore document IDs.

The app now ignores document IDs and relies on timestamps for ordering.

---

## 7. Secure Firestore

### Initial Rules (Testing)

Initially, Firestore rules allowed:

* Anyone to read
* Anyone to write

This is only suitable for testing.

### Updated Rules

Replace the testing rules with **authentication-required** rules.

New behavior:

* Authenticated users can read.
* Authenticated users can write.
* Unauthenticated users cannot access the database.

After updating the rules, click **Publish**.

---

## 8. What Has Been Learned

By this point, the app can:

* Save data to Firestore
* Retrieve data
* Listen for real-time updates (`addSnapshotListener`)
* Sort data using timestamps
* Query Firestore collections
* Secure the database with authentication rules

---

## Quick Revision

* Store message timestamps using `Date().timeIntervalSince1970`.
* Add a `date` field to every Firestore document.
* Delete old documents that don't contain timestamps.
* Sort messages with `.order(by: K.FStore.dateField)`.
* Use method chaining for cleaner Firestore queries.
* Ignore document IDs for ordering.
* Update Firestore security rules to allow only authenticated users to read and write.
* Next topic: improving keyboard and chat UI behavior.

---

## Next Lesson

Improve the chat app's user experience by fixing the keyboard issue:

* On a physical device, the keyboard hides the **Send** button.
* The next lesson focuses on adjusting the UI so users can send messages while the keyboard is visible.