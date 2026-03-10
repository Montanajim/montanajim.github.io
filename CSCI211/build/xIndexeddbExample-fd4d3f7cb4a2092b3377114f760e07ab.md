# Indexeddb -Example



```javascript
<!doctype html>
<html lang="en">

<head>
  <!-- Character encoding for the page -->
  <meta charset="utf-8" />

  <!-- Makes the page responsive on phones and tablets -->
  <meta name="viewport" content="width=device-width,initial-scale=1" />

  <!-- Title shown in the browser tab -->
  <title>IndexedDB CRUD: Pets</title>

  <style>
    /* Basic page layout and font styling */
    body {
      font-family: system-ui, sans-serif;
      max-width: 900px;
      margin: 24px auto;
      padding: 0 12px;
    }

    /* Box styling for grouped form sections */
    fieldset {
      border: 1px solid #ccc;
      padding: 12px;
      border-radius: 8px;
    }

    /* Put labels on their own line with spacing */
    label {
      display: block;
      margin: 10px 0 4px;
    }

    /* Make text fields fill available width */
    input {
      padding: 8px;
      width: 100%;
      box-sizing: border-box;
    }

    /* Basic button styling */
    button {
      padding: 10px 12px;
      margin-top: 12px;
      cursor: pointer;
    }

    /* Optional hover effect for buttons
    button:hover {
      background-color: antiquewhite;
    }
    */

    /* Two-column grid layout used in several form sections */
    .row {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
    }

    /* Log output box */
    #log {
      white-space: pre-wrap;
      background: #f7f7f7;
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #e5e5e5;
    }

    /* Card layout for each pet record */
    .card {
      display: grid;
      grid-template-columns: 120px 1fr;
      gap: 12px;
      align-items: center;
      padding: 12px;
      border: 1px solid #ddd;
      border-radius: 10px;
      margin: 12px 0;
    }

    /* Uniform image styling */
    img {
      width: 120px;
      height: 120px;
      object-fit: cover;
      border-radius: 10px;
      border: 1px solid #ddd;
    }

    /* Space buttons apart inside action areas */
    .actions button {
      margin-right: 8px;
    }

    /* Muted text for less important notes */
    .muted {
      color: #666;
      font-size: 0.95em;
    }
  </style>
</head>

<body>
  <!-- Main heading -->
  <h1>IndexedDB CRUD Demo: Pets</h1>

  <!-- Small explanation of stored fields -->
  <p class="muted">Fields: petPicture (Blob), ownerFN, ownerLN. Uses auto-increment id as primary key.</p>

  <!-- Section for creating a new record or updating an existing one -->
  <fieldset>
    <legend>Create / Update</legend>

    <!-- ID field: leave blank to create a new record -->
    <label>Record ID (leave blank to create new)</label>
    <input id="idInput" type="number" placeholder="e.g., 1" />

    <!-- First and last name inputs side by side -->
    <div class="row">
      <div>
        <label>Owner First Name</label>
        <input id="fnInput" type="text" placeholder="Ada" />
      </div>
      <div>
        <label>Owner Last Name</label>
        <input id="lnInput" type="text" placeholder="Lovelace" />
      </div>
    </div>

    <!-- File upload for pet image -->
    <label>Pet Picture</label>
    <input id="picInput" type="file" accept="image/*" />

    <!-- Save and clear buttons -->
    <div class="row">
      <button id="saveBtn">Save (Create if no ID, else Update)</button>
      <button id="clearBtn" type="button">Clear Form</button>
    </div>
  </fieldset>

  <!-- Section for reading and deleting records -->
  <fieldset style="margin-top:16px;">
    <legend>Read / Delete</legend>

    <div class="row">
      <div>
        <!-- Lookup a single record by ID -->
        <label>Lookup ID</label>
        <input id="lookupId" type="number" placeholder="e.g., 1" />
        <button id="getBtn" type="button">Get by ID</button>
        <button id="deleteBtn" type="button">Delete by ID</button>
      </div>
      <div>
        <!-- Buttons for listing and deleting all records -->
        <label>All Records</label>
        <button id="listBtn" type="button">List All</button>
        <button id="nukeBtn" type="button">Delete ALL (danger)</button>
      </div>
    </div>
  </fieldset>

  <!-- Where pet records are displayed -->
  <h2>Records</h2>
  <div id="records"></div>

  <!-- Where status and error messages are displayed -->
  <h2>Log</h2>
  <div id="log"></div>

  <script>
    // IIFE (Immediately Invoked Function Expression)
    // Keeps variables and functions out of the global scope.
    (() => {
      // Database name, version, and object store name
      const DB_NAME = "PetsDB";
      const DB_VERSION = 1;
      const STORE = "pets";

      // Short helper to get DOM elements by id
      const el = (id) => document.getElementById(id);

      // References to the log and records containers
      const logEl = el("log");
      const recordsEl = el("records");

      // Writes a timestamped message into the log area
      function log(msg) {
        logEl.textContent = `[${new Date().toLocaleTimeString()}] ${msg}\n` + logEl.textContent;
      } //----- end of function log -----

      // ------------------------------
      // IndexedDB helper functions
      // ------------------------------

      // Opens the database and creates the object store if needed
      function openDB() {
        return new Promise((resolve, reject) => {
          const req = indexedDB.open(DB_NAME, DB_VERSION);

          // Runs only when the database is first created
          // or when the version number increases
          req.onupgradeneeded = (e) => {
            const db = req.result;

            // Create the store only if it does not already exist
            if (!db.objectStoreNames.contains(STORE))
            {
              const store = db.createObjectStore(STORE, { keyPath: "id", autoIncrement: true });

              // Create indexes to support searching by owner names later if needed
              store.createIndex("ownerLN", "ownerLN", { unique: false });
              store.createIndex("ownerFN", "ownerFN", { unique: false });
            }
          };

          // Database opened successfully
          req.onsuccess = () => resolve(req.result);

          // Database open failed
          req.onerror = () => reject(req.error);
        });
      } //----- end of function openDB -----

      // Opens a transaction and gives access to the object store
      async function withStore(mode, fn) {
        const db = await openDB();

        return new Promise((resolve, reject) => {
          const tx = db.transaction(STORE, mode);
          const store = tx.objectStore(STORE);

          let result;

          try
          {
            // Run the callback that performs an operation on the store
            result = fn(store);
          } catch (err)
          {
            reject(err);
            return;
          }

          // Close DB when transaction completes successfully
          tx.oncomplete = () => { db.close(); resolve(result); };

          // Close DB and reject if transaction fails
          tx.onerror = () => { db.close(); reject(tx.error); };
          tx.onabort = () => { db.close(); reject(tx.error); };
        });
      } //----- end of function withStore -----

      // Converts an IndexedDB request into a Promise
      function reqToPromise(req) {
        return new Promise((resolve, reject) => {
          req.onsuccess = () => resolve(req.result);
          req.onerror = () => reject(req.error);
        });
      } //----- end of function reqToPromise -----

      // ------------------------------
      // CRUD operations
      // ------------------------------

      // Create a new pet record
      async function createPet({ ownerFN, ownerLN, petPicture }) {
        return withStore("readwrite", (store) => reqToPromise(store.add({ ownerFN, ownerLN, petPicture })));
      } //----- end of function createPet -----

      // Read one pet record by ID
      async function readPet(id) {
        return withStore("readonly", (store) => reqToPromise(store.get(id)));
      } //----- end of function readPet -----

      // Read all pet records
      async function readAllPets() {
        return withStore("readonly", (store) => reqToPromise(store.getAll()));
      } //----- end of function readAllPets -----

      // Update an existing pet record by ID
      async function updatePet(id, { ownerFN, ownerLN, petPicture }) {
        // IndexedDB put() replaces the entire object for a key,
        // so first fetch the existing record, then merge changes into it.
        const existing = await readPet(id);
        if (!existing) throw new Error(`No record with id=${id}`);

        const updated = {
          ...existing,
          ownerFN: ownerFN ?? existing.ownerFN,
          ownerLN: ownerLN ?? existing.ownerLN,
          // Keep old image if no new one was supplied
          petPicture: petPicture ?? existing.petPicture,
          id
        };

        return withStore("readwrite", (store) => reqToPromise(store.put(updated)));
      } //----- end of function updatePet -----

      // Delete a single pet by ID
      async function deletePet(id) {
        return withStore("readwrite", (store) => reqToPromise(store.delete(id)));
      } //----- end of function deletePet -----

      // Delete all pet records
      async function deleteAllPets() {
        return withStore("readwrite", (store) => reqToPromise(store.clear()));
      } //----- end of function deleteAllPets -----

      // ------------------------------
      // UI helper functions
      // ------------------------------

      // Convert uploaded file to Blob
      // In practice, a File already is a Blob
      function fileToBlob(file) {
        return file ?? null;
      } //----- end of function fileToBlob -----

      // Create a temporary browser URL for displaying an image blob
      function blobToObjectURL(blob) {
        return blob ? URL.createObjectURL(blob) : null;
      } //----- end of function blobToObjectURL -----

      // Render all records into the page
      function render(records) {
        recordsEl.innerHTML = "";

        // Show a message if there are no records
        if (!records || records.length === 0)
        {
          recordsEl.innerHTML = `<p class="muted">No records yet. Add one above.</p>`;
          return;
        }

        // Create a card for each record
        for (const r of records)
        {
          const url = blobToObjectURL(r.petPicture);
          const card = document.createElement("div");
          card.className = "card";

          card.innerHTML = `
        <div>
          ${url ? `<img alt="Pet picture for record ${r.id}" src="${url}">` : `<div class="muted">No image</div>`}
        </div>
        <div>
          <div><strong>ID:</strong> ${r.id}</div>
          <div><strong>Owner:</strong> ${escapeHTML(r.ownerFN)} ${escapeHTML(r.ownerLN)}</div>
          <div class="actions" style="margin-top:10px;">
            <button data-action="load" data-id="${r.id}">Load into form</button>
            <button data-action="delete" data-id="${r.id}">Delete</button>
          </div>
        </div>
      `;

          // Revoke object URL after a while to reduce memory leaks
          if (url)
          {
            setTimeout(() => URL.revokeObjectURL(url), 30_000);
          }

          recordsEl.appendChild(card);
        }
      } //----- end of function render -----

      // Escape HTML special characters to prevent HTML injection
      function escapeHTML(s) {
        return String(s ?? "").replace(/[&<>"']/g, (c) => ({
          "&": "&amp;",
          "<": "&lt;",
          ">": "&gt;",
          '"': "&quot;",
          "'": "&#39;"
        }[c]));
      } //----- end of function escapeHTML -----

      // Reset the form fields
      function clearForm() {
        el("idInput").value = "";
        el("fnInput").value = "";
        el("lnInput").value = "";
        el("picInput").value = "";
      } //----- end of function clearForm -----

      // Reload all records and display them
      async function refreshList() {
        const all = await readAllPets();

        // Sort by newest record first
        all.sort((a, b) => (b.id ?? 0) - (a.id ?? 0));

        render(all);
      } //----- end of function refreshList -----

      // ------------------------------
      // Event listeners
      // ------------------------------

      // Save button: create a new record or update an existing one
      el("saveBtn").addEventListener("click", async () => {
        try
        {
          const idRaw = el("idInput").value.trim();
          const ownerFN = el("fnInput").value.trim();
          const ownerLN = el("lnInput").value.trim();
          const file = el("picInput").files[0];

          // Basic validation
          if (!ownerFN || !ownerLN) throw new Error("Owner first/last name required.");

          const petPicture = fileToBlob(file);

          // If no ID is entered, create a new record
          if (!idRaw)
          {
            if (!petPicture) throw new Error("For a new record, choose an image file.");

            const newId = await createPet({ ownerFN, ownerLN, petPicture });
            log(`CREATE ok: id=${newId}`);
            clearForm();
          } 
          else
          {
            // Otherwise update the existing record
            const id = Number(idRaw);
            if (!Number.isInteger(id) || id <= 0) throw new Error("ID must be a positive integer.");

            // Update names and optionally replace the image
            await updatePet(id, { ownerFN, ownerLN, petPicture: petPicture || null });
            log(`UPDATE ok: id=${id} (image ${petPicture ? "replaced" : "unchanged"})`);
          }

          await refreshList();
        } catch (err)
        {
          log(`ERROR: ${err.message || err}`);
        }
      });

      // Clear form button
      el("clearBtn").addEventListener("click", () => clearForm());

      // Read one record by ID
      el("getBtn").addEventListener("click", async () => {
        try
        {
          const id = Number(el("lookupId").value);
          if (!Number.isInteger(id) || id <= 0) throw new Error("Lookup ID must be a positive integer.");

          const rec = await readPet(id);

          if (!rec)
          {
            log(`READ (by id) : id=${id} not found`);
            return;
          }

          log(`READ (by id) ok: id=${id} => ${rec.ownerFN} ${rec.ownerLN} (hasImage=${!!rec.petPicture})`);
        } catch (err)
        {
          log(`ERROR: ${err.message || err}`);
        }
      });

      // Delete one record by ID
      el("deleteBtn").addEventListener("click", async () => {
        try
        {
          const id = Number(el("lookupId").value);
          if (!Number.isInteger(id) || id <= 0) throw new Error("Delete ID must be a positive integer.");

          await deletePet(id);
          log(`DELETE ok: id=${id}`);
          await refreshList();
        } catch (err)
        {
          log(`ERROR: ${err.message || err}`);
        }
      });

      // List all records
      el("listBtn").addEventListener("click", async () => {
        try
        {
          await refreshList();
          const all = await readAllPets();
          log(`READ ALL ok: count=${all.length}`);
        } catch (err)
        {
          log(`ERROR: ${err.message || err}`);
        }
      });

      // Delete all records
      el("nukeBtn").addEventListener("click", async () => {
        try
        {
          // No confirmation dialog here
          await deleteAllPets();
          log("DELETE ALL ok");
          await refreshList();
        } catch (err)
        {
          log(`ERROR: ${err.message || err}`);
        }
      });

      // Handle clicks on dynamically created buttons in each record card
      recordsEl.addEventListener("click", async (e) => {
        const btn = e.target.closest("button");
        if (!btn) return;

        const action = btn.dataset.action;
        const id = Number(btn.dataset.id);

        try
        {
          if (action === "delete")
          {
            // Delete record from card button
            await deletePet(id);
            log(`DELETE ok: id=${id}`);
            await refreshList();
          } 
          else if (action === "load")
          {
            // Load record data into the form for editing
            const rec = await readPet(id);
            if (!rec) throw new Error(`No record with id=${id}`);

            el("idInput").value = rec.id;
            el("fnInput").value = rec.ownerFN ?? "";
            el("lnInput").value = rec.ownerLN ?? "";

            // Browsers do not allow code to set a file input value
            el("picInput").value = "";

            log(`Loaded id=${id} into form (choose a new image only if you want to replace it).`);
          }
        } catch (err)
        {
          log(`ERROR: ${err.message || err}`);
        }
      });

      // Load and display any existing records when the page first opens
      refreshList().catch(err => log(`ERROR: ${err.message || err}`));
    })();
  </script>
</body>

</html>
```

