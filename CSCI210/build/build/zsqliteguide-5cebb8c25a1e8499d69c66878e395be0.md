# **PHP + SQLite Shortcut Guide**

*A fast, practical reference for learning and teaching SQLite with PDO.*

------

## **0. What Is SQLite? **

SQLite is a **self-contained, serverless SQL database engine** that stores everything in **one single file**.
 There is *no* database server to install.
 There are *no* usernames, no passwords, no ports, no daemons, no configuration files.

If PHP can write to a folder, it can use SQLite.

SQLite is embedded in:

- PHP
- Python
- Android & iOS
- Firefox
- Windows & macOS
- Thousands of apps and devices

This makes SQLite:

- **Faster to set up** than MySQL
- **Simpler to teach** than PostgreSQL
- **Perfect for classroom exercises**
- **Rock-solid** for local or embedded data storage

------

## **Best Use Cases for SQLite**

SQLite is your “pocket database”—small, steady, and always ready.

### ✔ Ideal For:

- Teaching SQL and PDO
- Small to medium websites with modest traffic
- Desktop apps
- Mobile apps (Android/iOS)
- Prototyping and rapid development
- Apps that need offline local storage
- Research tools and student projects

### ❌ Not Ideal For:

- High-traffic websites with heavy write operations
- Large multi-user applications
- Massive datasets (hundreds of GB)
- Systems requiring advanced permissions or replication

Use SQLite for **simplicity + reliability**.
 Use a server DB for **scalability + concurrency**.

------

## **0.5. How to Create a SQLite Database**

SQLite database files are created **automatically**—as soon as PHP connects to a file that doesn’t exist, SQLite creates it.

You can create databases in three main ways:

------

### **Method 1 — Auto-Create Via PHP PDO **

Just connect to a file. If it doesn't exist, SQLite generates it instantly:

```php
$dbFile = __DIR__ . "/database.sqlite";

$db = new PDO("sqlite:" . $dbFile);
$db->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
```

✔ Zero setup
 ✔ Creates the DB automatically
 ✔ Works on every OS
 ✔ Perfect for teaching

------

### **Method 2 — Create with sqlite3 Command Line**

```bash
sqlite3 mydb.sqlite
```

In the SQLite shell:

```sql
CREATE TABLE test (id INTEGER);
.quit
```

Useful for:

- Inspecting the DB
- Running test queries
- Manually creating schemas

------

### **Method 3 — Create with a Graphical Tool (Beginner-Friendly)**

Recommended GUIs:

- DB Browser for SQLite
- SQLiteStudio
- TablePlus

Steps:

1. Create a new database file
2. Add tables
3. Import/export data visually

Great for visual learners.

------

## **Best Location for Your Database File**

```
project/
    db/
        database.sqlite
    public/
        index.php
```

Store the DB **outside the public folder** for security.

------

## **1. Connect to SQLite**

```php
$db = new PDO("sqlite:" . __DIR__ . "/database.sqlite");
$db->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
```

------

## **2. Create a Table**

```php
$db->exec("
    CREATE TABLE IF NOT EXISTS students (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL,
        major TEXT NOT NULL,
        created_at TEXT NOT NULL
    )
");
```

------

## **3. Insert Data (CREATE)**

```php
$stmt = $db->prepare("
    INSERT INTO students (name, major, created_at)
    VALUES (:name, :major, :created)
");
$stmt->execute([
    ':name'    => $name,
    ':major'   => $major,
    ':created' => date('Y-m-d H:i:s')
]);
```

------

## **4. Read Data (SELECT)**

```php
$rows = $db->query("
    SELECT * FROM students ORDER BY id DESC
")->fetchAll(PDO::FETCH_ASSOC);
```

------

## **5. Search / Filtering**

```php
$stmt = $db->prepare("
    SELECT * FROM students
    WHERE name LIKE :q OR major LIKE :q
");
$stmt->execute([':q' => '%' . $search . '%']);
$rows = $stmt->fetchAll(PDO::FETCH_ASSOC);
```

------

## **6. Update Data**

```php
$stmt = $db->prepare("
    UPDATE students
    SET name = :name, major = :major
    WHERE id = :id
");
$stmt->execute([
    ':name' => $newName,
    ':major' => $newMajor,
    ':id' => $id
]);
```

------

## **7. Delete Data**

```php
$stmt = $db->prepare("DELETE FROM students WHERE id = :id");
$stmt->execute([':id' => $id]);
```

------

## **8. Common SQLite Functions**

| Purpose           | Function               |
| ----------------- | ---------------------- |
| Current timestamp | `datetime('now')`      |
| Count rows        | `COUNT(*)`             |
| Max value         | `MAX(column)`          |
| Sort              | `ORDER BY column DESC` |
| Limit             | `LIMIT 10`             |

------

## **9. SQLite File Location Tips**

```php
$db = new PDO("sqlite:" . __DIR__ . "/db/mydb.sqlite");
```

------

## **10. Error Checking**

```php
try {
    // your PDO code
} catch (PDOException $e) {
    echo "Error: " . htmlspecialchars($e->getMessage());
}
```

------

#3 **11. Security Must-Knows**

- Always use prepared statements
- Never embed variables directly in SQL strings
- Validate all user inputs
- Escape HTML output with `htmlspecialchars()`
- Keep SQLite files outside public web directories

------

## **12. Useful PDO Fetch Modes**

```php
PDO::FETCH_ASSOC
PDO::FETCH_NUM
PDO::FETCH_OBJ
PDO::FETCH_COLUMN
```

------

## **13. Check if a Table Exists**

```php
$result = $db->query("
    SELECT name FROM sqlite_master
    WHERE type='table' AND name='students'
");
```

------

## **14. Drop a Table**

```php
$db->exec("DROP TABLE IF EXISTS students");
```

------

#3 **15. List All Tables**

```php
$tables = $db->query("
    SELECT name FROM sqlite_master WHERE type='table'
")->fetchAll(PDO::FETCH_COLUMN);
```

------

## **16. CRUD Workflow (Commit This to Memory)**

```
1. Connect
2. Prepare
3. Bind
4. Execute
5. Fetch (optional)
```

------

## **17. Working with BLOBs (Images, PDFs, Binary Data)**

SQLite supports BLOBs for storing binary data or Base64 strings.

------

### **Store a Raw BLOB**

```php
$data = file_get_contents("photo.jpg");

$stmt = $db->prepare("
    INSERT INTO photos (title, image)
    VALUES (:t, :img)
");
$stmt->bindValue(':t', "Sunset");
$stmt->bindValue(':img', $data, PDO::PARAM_Lob);
$stmt->execute();
```

------

### **Retrieve a BLOB**

```php
$stmt = $db->prepare("SELECT image FROM photos WHERE id = :id");
$stmt->execute([':id' => $id]);
$row = $stmt->fetch(PDO::FETCH_ASSOC);

header("Content-Type: image/jpeg");
echo $row['image'];
```

------

### **Base64 Method (Great for Beginners)**

```php
$b64 = base64_encode(file_get_contents("photo.jpg"));
```

Display:

```html
<img src="data:image/jpeg;base64,<?= $b64 ?>">
```

------

## **BLOB Use Cases**

✔ Teaching
 ✔ Thumbnails
 ✔ Small apps
 ✔ Offline tools

❌ Large images
 ❌ Video files
 ❌ High-traffic apps

Production rule:
 **Store files on disk, store filenames in the DB.**

