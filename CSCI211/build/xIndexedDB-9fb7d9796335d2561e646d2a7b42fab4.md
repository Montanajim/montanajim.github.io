# IndexedDB

**IndexedDB** is a powerful database built directly into the browser. You can think of it as a much more capable version of `localStorage`.

Here are its main characteristics based on the sources:

**Purpose:** It's designed for offline-first applications, caching large amounts of data, and storing structured records or large files (blobs).

**Asynchronous:** Unlike `localStorage`, it operates asynchronously, meaning it won't freeze the user interface during read or write operations.

**Transactions:** All data operations must happen within a "transaction." This ensures data integrity—either the entire group of operations succeeds together, or they all fail safely.

**Structure:** It stores data in "object stores" (similar to tables in traditional databases) and allows you to query data using unique keys or specific indexes.

The tradeoff for this power is complexity. The native API relies heavily on events and requires managing schema versions manually.



---



IndexedDB is the browser’s built-in **client-side database** for storing **large amounts of structured data**. Unlike `localStorage`, which is just a small synchronous key/value bin, IndexedDB is **asynchronous**, **transactional**, and built to store records in **object stores** with **indexes** for fast lookup. The official spec defines it as a database of records made of **keys and values**, with indexes layered on top for efficient retrieval. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API?utm_source=chatgpt.com))

The mental model is this: an IndexedDB database contains one or more **object stores**; each object store holds records; each record has a **primary key** and a **value**; and you can create **indexes** on fields you want to search by frequently. Reads and writes happen inside **transactions**, usually `readonly` or `readwrite`. Records in an object store are sorted by key, which is why lookups and ordered retrieval are efficient. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IDBDatabase?utm_source=chatgpt.com))

Its major uses are practical and blunt: offline-first web apps, local caching of API data, storing large structured datasets in the browser, queueing work while offline and syncing later, saving user-generated content such as drafts, and storing binary data like files or blobs. MDN explicitly notes that IndexedDB is suited for significant amounts of structured data, including files/blobs, and is a better fit than Web Storage when the data is larger or more structured. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API?utm_source=chatgpt.com))

The key advantage is not elegance. IndexedDB is not elegant. It is powerful. If `localStorage` is a sticky note, IndexedDB is a filing cabinet with an index and a lock on the drawer. The cost is complexity: the native API is verbose, event-driven, and easy to misuse. That is why many developers wrap it with libraries like Dexie. But the underlying database matters because the wrappers are standing on its shoulders, not replacing its rules. This complexity follows from its asynchronous request/transaction model documented in the platform APIs. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB?utm_source=chatgpt.com))

## Core pieces

You usually start with:

```javascript
const request = indexedDB.open("PetsDB", 1);
```

That `open()` call can trigger three major events: success, error, and upgrade. The **upgrade** path is where you create or modify object stores and indexes. That schema work happens during version changes, not casually in the middle of normal reads and writes. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB?utm_source=chatgpt.com))

A typical setup looks like this:

```javascript
const request = indexedDB.open("PetsDB", 1);

request.onupgradeneeded = (event) => {
  const db = event.target.result;

  const store = db.createObjectStore("pets", {
    keyPath: "id",
    autoIncrement: true
  });

  store.createIndex("name", "name", { unique: false });
  store.createIndex("type", "type", { unique: false });
};

request.onsuccess = (event) => {
  const db = event.target.result;
  console.log("Database opened");
};

request.onerror = (event) => {
  console.error("Database error:", event.target.error);
};
```

Here, `pets` is the object store, `id` is the primary key, and `name` and `type` are indexed fields. Object stores and indexes are official IndexedDB concepts, and `createIndex()` is the standard way to define searchable fields. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/createIndex?utm_source=chatgpt.com))

## Datatypes IndexedDB can store

IndexedDB stores values using the browser’s **structured clone algorithm**. That means it can store much more than plain strings. MDN notes that IndexedDB indexes can contain JavaScript data types and stored objects are serialized with structured clone semantics. In practice, that means you can store ordinary objects, arrays, dates, numbers, strings, booleans, blobs, files, and other cloneable structured data. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/createIndex?utm_source=chatgpt.com))

A few practical categories matter most:

**Primitive values**: strings, numbers, booleans, big integers in modern environments.
**Structured values**: objects and arrays.
**Date-like and binary values**: `Date`, `Blob`, `File`, `ArrayBuffer`, typed arrays.
**Nested data**: hierarchical objects are explicitly part of the spec’s model. ([W3C](https://www.w3.org/TR/IndexedDB/?utm_source=chatgpt.com))

For **keys**, the story is narrower. Keys are not “anything JavaScript can dream up at 2 a.m.” They have to be valid IndexedDB key types. The spec defines keys separately from values, and object stores are sorted by those keys. In practice, developers most often use numbers, strings, dates, or arrays of key-compatible values as keys. ([W3C](https://www.w3.org/TR/IndexedDB/?utm_source=chatgpt.com))

A realistic record looks like this:

```javascript
{
  id: 1,
  name: "Luna",
  type: "Cat",
  age: 3,
  vaccinated: true,
  tags: ["friendly", "indoor"],
  photo: someBlob,
  adoptedAt: new Date()
}
```

That is the kind of structured object IndexedDB is designed to hold. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API?utm_source=chatgpt.com))

## Major CRUD examples

Below are the essential operations. This is the part that pays rent.

### Create

Use `add()` when you want to insert a new record and fail if the key already exists.

```javascript
function addPet(db, pet) {
  const tx = db.transaction("pets", "readwrite");
  const store = tx.objectStore("pets");
  const request = store.add(pet);

  request.onsuccess = () => {
    console.log("Pet added");
  };

  request.onerror = (event) => {
    console.error("Add failed:", event.target.error);
  };
}
```

Example call:

```javascript
addPet(db, {
  name: "Luna",
  type: "Cat",
  age: 3
});
```

MDN distinguishes `add()` from `put()`: `add()` creates a new record and errors on duplicate keys. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/add?utm_source=chatgpt.com))

### Read one record by primary key

Use `get()`.

```javascript
function getPet(db, id) {
  const tx = db.transaction("pets", "readonly");
  const store = tx.objectStore("pets");
  const request = store.get(id);

  request.onsuccess = () => {
    console.log("Found:", request.result);
  };

  request.onerror = (event) => {
    console.error("Read failed:", event.target.error);
  };
}
```

`get()` retrieves the object for a specific key and returns a structured clone of the stored value. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/get?utm_source=chatgpt.com))

### Read all records

Use `getAll()` for convenience.

```javascript
function getAllPets(db) {
  const tx = db.transaction("pets", "readonly");
  const store = tx.objectStore("pets");
  const request = store.getAll();

  request.onsuccess = () => {
    console.log("All pets:", request.result);
  };

  request.onerror = (event) => {
    console.error("Read all failed:", event.target.error);
  };
}
```

`getAll()` returns all matching objects, or all objects in the store if you provide no filter. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/getAll?utm_source=chatgpt.com))

### Read many records with iteration

Use a cursor when you want custom filtering, ordered traversal, or streaming through records one at a time.

```javascript
function listPetsWithCursor(db) {
  const tx = db.transaction("pets", "readonly");
  const store = tx.objectStore("pets");
  const request = store.openCursor();

  request.onsuccess = (event) => {
    const cursor = event.target.result;
    if (cursor) {
      console.log(cursor.key, cursor.value);
      cursor.continue();
    } else {
      console.log("No more records");
    }
  };

  request.onerror = (event) => {
    console.error("Cursor failed:", event.target.error);
  };
}
```

`openCursor()` is the standard iterator for walking an object store record by record. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/openCursor?utm_source=chatgpt.com))

### Update

Use `put()` when you want an upsert: update if the key exists, insert if it does not.

```javascript
function updatePet(db, pet) {
  const tx = db.transaction("pets", "readwrite");
  const store = tx.objectStore("pets");
  const request = store.put(pet);

  request.onsuccess = () => {
    console.log("Pet saved");
  };

  request.onerror = (event) => {
    console.error("Update failed:", event.target.error);
  };
}
```

Example:

```javascript
updatePet(db, {
  id: 1,
  name: "Luna",
  type: "Cat",
  age: 4
});
```

This is where students often get tripped up: `put()` is not strictly “update only.” It can also insert. If you need “insert only,” use `add()`. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/put?utm_source=chatgpt.com))

### Delete one record

Use `delete()`.

```javascript
function deletePet(db, id) {
  const tx = db.transaction("pets", "readwrite");
  const store = tx.objectStore("pets");
  const request = store.delete(id);

  request.onsuccess = () => {
    console.log("Pet deleted");
  };

  request.onerror = (event) => {
    console.error("Delete failed:", event.target.error);
  };
}
```

`delete()` removes a record by key, and it can also take an `IDBKeyRange` for multiple records. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/delete?utm_source=chatgpt.com))

### Delete everything

Use `clear()`.

```javascript
function clearPets(db) {
  const tx = db.transaction("pets", "readwrite");
  const store = tx.objectStore("pets");
  const request = store.clear();

  request.onsuccess = () => {
    console.log("All pets removed");
  };

  request.onerror = (event) => {
    console.error("Clear failed:", event.target.error);
  };
}
```

`clear()` wipes the entire object store, including index references to those records. It is a chainsaw, not a scalpel. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/clear?utm_source=chatgpt.com))

## Querying by index

Suppose you created this index:

```javascript
store.createIndex("type", "type", { unique: false });
```

You can later retrieve pets by type:

```javascript
function getPetsByType(db, type) {
  const tx = db.transaction("pets", "readonly");
  const store = tx.objectStore("pets");
  const index = store.index("type");
  const request = index.getAll(type);

  request.onsuccess = () => {
    console.log(`Pets of type ${type}:`, request.result);
  };

  request.onerror = (event) => {
    console.error("Index query failed:", event.target.error);
  };
}
```

This is one of the biggest reasons IndexedDB exists at all. Without indexes, you are just shoveling JSON into a browser cave. With indexes, you have searchable local data. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/createIndex?utm_source=chatgpt.com))

## Common mistakes

The biggest mistakes are predictable.

People think IndexedDB works like SQL. It does not. There is no SQL query language built in; the spec explicitly describes a low-level API over records and indexes, and a query language could be layered on top, but is not built in. ([W3C](https://www.w3.org/TR/IndexedDB/?utm_source=chatgpt.com))

People confuse `add()` and `put()`. That is a bug factory. `add()` is insert-only; `put()` is upsert. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/add?utm_source=chatgpt.com))

People try to read or write outside transactions. Also a bug factory. All data access is done within transactions. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IDBTransaction?utm_source=chatgpt.com))

People use IndexedDB when `localStorage` would have been enough, or worse, use `localStorage` when they actually need IndexedDB. If the data is tiny, flat, and synchronous access is acceptable, `localStorage` is simpler. If the data is structured, larger, indexed, or offline-critical, IndexedDB is the right hammer. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API?utm_source=chatgpt.com))

## A compact full example

Here is a minimal working pattern:

```javascript
const request = indexedDB.open("PetsDB", 1);

request.onupgradeneeded = (event) => {
  const db = event.target.result;
  const store = db.createObjectStore("pets", {
    keyPath: "id",
    autoIncrement: true
  });
  store.createIndex("name", "name", { unique: false });
  store.createIndex("type", "type", { unique: false });
};

request.onsuccess = (event) => {
  const db = event.target.result;

  // CREATE
  let tx = db.transaction("pets", "readwrite");
  let store = tx.objectStore("pets");
  store.add({ name: "Luna", type: "Cat", age: 3 });

  tx.oncomplete = () => {
    // READ ALL
    const readTx = db.transaction("pets", "readonly");
    const readStore = readTx.objectStore("pets");
    const getAllRequest = readStore.getAll();

    getAllRequest.onsuccess = () => {
      console.log("All pets:", getAllRequest.result);

      // UPDATE first record if present
      const pets = getAllRequest.result;
      if (pets.length > 0) {
        const firstPet = pets[0];
        firstPet.age = 4;

        const updateTx = db.transaction("pets", "readwrite");
        updateTx.objectStore("pets").put(firstPet);

        updateTx.oncomplete = () => {
          console.log("Updated pet");

          // DELETE by key
          const deleteTx = db.transaction("pets", "readwrite");
          deleteTx.objectStore("pets").delete(firstPet.id);

          deleteTx.oncomplete = () => {
            console.log("Deleted pet");
          };
        };
      }
    };
  };
};

request.onerror = (event) => {
  console.error("DB open failed:", event.target.error);
};
```

For primary references, use MDN’s IndexedDB guide and API reference, plus the W3C spec. ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB?utm_source=chatgpt.com))

