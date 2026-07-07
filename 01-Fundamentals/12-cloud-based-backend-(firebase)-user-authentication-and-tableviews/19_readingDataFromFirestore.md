# Notes: Reading Data From Firestore

## Objective

* Read messages from **Cloud Firestore**.
* Display saved messages in the app's table view when `ChatViewController` loads.

---

## 1. Loading Messages

* Call `loadMessages()` inside `viewDidLoad()`.
* Purpose:

  * Remove dummy messages.
  * Fetch all messages from Firestore.
  * Populate the table view.

```swift
messages = []
```

---

## 2. Fetch Documents from Firestore

Access the **messages** collection and retrieve all documents.

```swift
db.collection(K.FStore.collectionName).getDocuments { querySnapshot, error in
    ...
}
```

Returns:

* `querySnapshot` → Contains retrieved documents.
* `error` → Contains an error if something went wrong.

---

## 3. Handle Errors

```swift
if let e = error {
    print("There was an issue retrieving data: \(e)")
}
```

If there's no error, continue processing the data.

---

## 4. Access Retrieved Documents

`querySnapshot?.documents` returns an array of `QueryDocumentSnapshot`.

```swift
if let snapshotDocuments = querySnapshot?.documents {
    ...
}
```

Each document contains a dictionary of key-value pairs.

---

## 5. Loop Through Documents

```swift
for doc in snapshotDocuments {
    let data = doc.data()
}
```

Each document's data can be accessed using:

```swift
data["fieldName"]
```

---

## 6. Extract Sender and Message

Firestore stores values as `Any`, so they must be downcast.

```swift
if let sender = data[K.FStore.senderField] as? String,
   let messageBody = data[K.FStore.bodyField] as? String {
    ...
}
```

### Why cast?

* Dictionary values are of type `Any`.
* Firebase supports multiple data types.
* We know these fields should be `String`.

---

## 7. Create a Message Object

```swift
let newMessage = Message(
    sender: sender,
    body: messageBody
)
```

Append it to the messages array.

```swift
self.messages.append(newMessage)
```

---

## 8. Reload the Table View

Since Firestore fetches data **asynchronously**, the table view may load before the messages arrive.

Reload the table after new data is added.

```swift
DispatchQueue.main.async {
    self.tableView.reloadData()
}
```

### Why use `DispatchQueue.main.async`?

* Firestore completion handlers run in the background.
* UI updates must happen on the **main thread**.

---

## Firestore Data Flow

```
viewDidLoad()
       |
       V
loadMessages()
       |
       V
Clear messages array
       |
       V
getDocuments()
       |
       V
Receive QuerySnapshot
       |
       V
Loop through documents
       |
       V
Extract sender & body
       |
       V
Create Message object
       |
       V
Append to messages array
       |
       V
Reload Table View (Main Thread)
```

---

## Key Firestore Classes

### `QuerySnapshot`

* Represents all documents returned by a query.
* Useful properties:

  * `documents`
  * `count`
  * `isEmpty`

### `QueryDocumentSnapshot`

* Represents a single document.
* Access its contents with:

```swift
doc.data()
```

---

## Important Concepts

* `getDocuments()` retrieves all documents in a collection.
* Always clear old data before loading new data.
* Handle Firestore errors safely.
* Use optional binding (`if let`) when working with Firestore results.
* Downcast `Any` values to the expected type (`String`).
* Create model objects (`Message`) from Firestore data.
* Reload the table view after asynchronous data retrieval.
* Perform UI updates on the **main thread**.

---

## Limitation of Current Approach

After sending a new message:

* The message is saved to Firestore.
* The UI does **not** update automatically.

Reason:

* `getDocuments()` only fetches data once.

**Next improvement:** Use Firestore's **real-time listeners** (`addSnapshotListener`) to automatically update the chat whenever the database changes.
