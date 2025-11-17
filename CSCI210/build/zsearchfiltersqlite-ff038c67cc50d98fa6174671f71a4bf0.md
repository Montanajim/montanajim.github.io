# Search Filter - SQLITE

```php
<?php
declare(strict_types=1);

$dbPath = __DIR__ . "/database.sqlite";
$pdo = new PDO("sqlite:" . $dbPath);
$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

// Create table if it doesn't exist
$pdo->exec("
    CREATE TABLE IF NOT EXISTS students (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL,
        major TEXT NOT NULL,
        created_at TEXT NOT NULL
    )
");


// HANDLE FORM ACTIONS
// -----------------------------

// ADD new student
if (isset($_POST['add'])) {
    $name  = trim($_POST['name'] ?? '');
    $major = trim($_POST['major'] ?? '');

    if ($name !== '' && $major !== '') {
        $stmt = $pdo->prepare("
            INSERT INTO students (name, major, created_at)
            VALUES (:n, :m, :c)
        ");
        $stmt->execute([
            ':n' => $name,
            ':m' => $major,
            ':c' => date('Y-m-d H:i:s'),
        ]);
    }
}

// UPDATE existing student
if (isset($_POST['update'])) {
    $id    = (int)($_POST['id'] ?? 0);
    $name  = trim($_POST['edit_name'] ?? '');
    $major = trim($_POST['edit_major'] ?? '');

    if ($id > 0 && $name !== '' && $major !== '') {
        $stmt = $pdo->prepare("
            UPDATE students
            SET name = :n, major = :m
            WHERE id = :id
        ");
        $stmt->execute([
            ':n'  => $name,
            ':m'  => $major,
            ':id' => $id,
        ]);
    }
}

// DELETE student
if (isset($_POST['delete'])) {
    $id = (int)($_POST['id'] ?? 0);
    if ($id > 0) {
        $stmt = $pdo->prepare("DELETE FROM students WHERE id = :id");
        $stmt->execute([':id' => $id]);
    }
}


// SEARCH FILTER
// -----------------------------

$searchTerm = trim($_GET['q'] ?? '');

// If there is a search term, filter by name OR major
if ($searchTerm !== '') {
    $stmt = $pdo->prepare("
        SELECT * FROM students
        WHERE name  LIKE :q
           OR major LIKE :q
        ORDER BY id DESC
    ");
    $stmt->execute([':q' => '%' . $searchTerm . '%']);
    $rows = $stmt->fetchAll(PDO::FETCH_ASSOC);
} else {
    // No search term: show all
    // $rows = $pdo->query("
    //     SELECT * FROM students
    //     ORDER BY id DESC
    // ")->fetchAll(PDO::FETCH_ASSOC);

    $sqlstmt = "SELECT * FROM students ORDER BY name";
    $stmt = $pdo->query($sqlstmt);
    $rows = $stmt->fetchAll(PDO::FETCH_ASSOC);
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>SQLite + PHP CRUD Demo</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 800px; margin: 20px auto; }
        form { margin-bottom: 15px; }
        .student-card { border: 1px solid #ccc; padding: 10px; margin-bottom: 10px; }
        .inline-form { display: inline-block; margin-right: 10px; }
        input[type="text"] { padding: 4px; margin-right: 4px; }
        button { padding: 4px 8px; }
    </style>
</head>
<body>
    <h2>SQLite + PHP CRUD Demo</h2>

    <!-- SEARCH FORM (GET) -->
    <h3>Search Students</h3>
    <form method="GET">
        <input
            type="text"
            name="q"
            placeholder="Search by name or major"
            value="<?= htmlspecialchars($searchTerm) ?>"
        >
        <button type="submit">Search</button>
        <a href="search_filter.php"><button type="button">Clear</button></a>
    </form>

    <!-- ADD FORM -->
    <h3>Add New Student</h3>
    <form method="POST">
        <input type="text" name="name" placeholder="Student Name" required>
        <input type="text" name="major" placeholder="Major" required>
        <button type="submit" name="add">Add Student</button>
    </form>

    <!-- STUDENT LIST -->
    <h3>Students</h3>

    <?php if (empty($rows)): ?>
        <p><em>No students found.</em></p>
    <?php else: ?>
        <?php foreach ($rows as $r): ?>
            <div class="student-card">
                <p>
                    <strong>ID:</strong> <?= $r['id'] ?><br>
                    <strong>Name:</strong> <?= htmlspecialchars($r['name']) ?><br>
                    <strong>Major:</strong> <?= htmlspecialchars($r['major']) ?><br>
                    <small>Created at: <?= htmlspecialchars($r['created_at']) ?></small>
                </p>

                <!-- UPDATE FORM (inline) -->
                <form method="POST" class="inline-form">
                    <input type="hidden" name="id" value="<?= $r['id'] ?>">
                    <input
                        type="text"
                        name="edit_name"
                        value="<?= htmlspecialchars($r['name']) ?>"
                        placeholder="Name"
                        required
                    >
                    <input
                        type="text"
                        name="edit_major"
                        value="<?= htmlspecialchars($r['major']) ?>"
                        placeholder="Major"
                        required
                    >
                    <button type="submit" name="update">Update</button>
                </form>

                <!-- DELETE FORM -->
                <form method="POST" class="inline-form">
                    <input type="hidden" name="id" value="<?= $r['id'] ?>">
                    <button type="submit" name="delete" onclick="return confirm('Delete this student?');">
                        Delete
                    </button>
                </form>
            </div>
        <?php endforeach; ?>
    <?php endif; ?>
</body>
</html>

```

