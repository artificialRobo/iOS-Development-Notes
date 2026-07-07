# Notes: Real-Time Updates on Firestore

## 1. Problem with `getDocuments()`

* `getDocuments()` fetches data **only once**.
* It must be called manually every time you want the latest documents.
* This is not ideal for apps like chat/messaging apps where data changes frequently.

---

## 2. Using `addSnapshotListener()`

* Firestore provides **`addSnapshotListener()`** for **real-time updates**.
* It automatically listens for changes in a collection.
* Whenever a new document is added, the listener is triggered again.
* This is perfect for messaging apps because new messages appear automatically.

**Change:**

```swift
getDocuments()
```

Replace with:

```swift
addSnapshotListener()
```

---

## 3. Issue After Switching to `addSnapshotListener()`

* Every time the listener runs, it appends messages to the existing array.
* Result: **Duplicate messages** appear in the table view.

---

## 4. Solution to Prevent Duplicates

* Clear the `messages` array **inside the snapshot listener closure** before adding new data.

Example:

```swift
self.messages.removeAll()
```

* Then reload the array with the latest documents.
* Since the closure accesses a class property, use:

```swift
self.messages
```

---

## 5. Result

* New messages are added in real time.
* No duplicate messages are displayed.
* The table view updates automatically whenever the database changes.

---

## New Problem: Incorrect Message Order

* Messages are ordered by their **Firestore document IDs**.
* Document IDs are automatically generated.
* Since IDs are random/alphanumeric, messages don't appear in the order they were sent.

Example ordering:

* Numbers come before letters.
* IDs determine display order, not send time.

---

## Next Step

* Instead of sorting by document ID, messages should be sorted by their **timestamp**.
* This will display chat messages in chronological order (oldest → newest).
