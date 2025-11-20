# YouTube Demo



```php
<?php
// Simple YouTube video manager using PDO (PHP Data Objects) and SQLite.
// This script is a single-page app that can:
// - Add YouTube videos with a title, genre, and description
// - Store them in an SQLite database file
// - Show one selected video in an embedded player
// - List all saved videos and let you delete them

// Enforce strict typing for function parameters and return types.
// This helps catch some type-related mistakes early.
declare(strict_types=1);

// Build the path to the SQLite database file.
// __DIR__ is the directory where this PHP file lives.
$dbPath = __DIR__ . '/videos.sqlite';

// The DSN (Data Source Name) tells PDO which database driver to use and where it is.
// For SQLite, the format is "sqlite:/path/to/file".
$dsn = 'sqlite:' . $dbPath;

try {
    // Create a new PDO connection to the SQLite database.
    $pdo = new PDO($dsn);

    // Tell PDO to throw exceptions when errors happen.
    // This makes error handling easier.
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e) {
    // If anything goes wrong with the connection, stop the script
    // and show a safe error message.
    die('Database connection failed: ' . htmlspecialchars($e->getMessage()));
}

// Create the "videos" table if it does not already exist.
// This is a simple schema for our video manager.
$pdo->exec(
    'CREATE TABLE IF NOT EXISTS videos (
        id INTEGER PRIMARY KEY AUTOINCREMENT,  -- Unique ID for each video
        title TEXT NOT NULL,                   -- Video title
        url TEXT NOT NULL,                     -- Original YouTube URL
        video_id TEXT NOT NULL,                -- Extracted YouTube video ID
        genre TEXT NOT NULL,                   -- Category/genre
        description TEXT NOT NULL,             -- Description written by the user
        created_at TEXT NOT NULL               -- When the entry was created (ISO timestamp)
    )'
);

// This will hold feedback messages for the user (success or error).
$message = '';

/**
 * Extract the 11-character YouTube video ID from a URL.
 *
 * This function supports several common YouTube URL formats:
 *  - https://youtu.be/VIDEO_ID
 *  - https://www.youtube.com/watch?v=VIDEO_ID
 *  - https://www.youtube.com/embed/VIDEO_ID
 *  - https://www.youtube.com/shorts/VIDEO_ID
 *
 * If it can't find a valid ID, it returns null.
 */
function extractYouTubeId(string $url): ?string
{
    // Regular expressions to match different YouTube URL patterns.
    $patterns = [
        '#youtu\\.be/([\\w-]{11})#i',
        '#youtube\\.com/watch\\?v=([\\w-]{11})#i',
        '#youtube\\.com/embed/([\\w-]{11})#i',
        '#youtube\\.com/shorts/([\\w-]{11})#i',
    ];

    // Try each pattern until one matches.
    foreach ($patterns as $pattern) {
        if (preg_match($pattern, $url, $matches)) {
            // $matches[1] contains the captured video ID.
            return $matches[1];
        }
    }

    // If we get here, none of the simple patterns matched.
    // As a fallback, look at the query string (e.g., ?v=VIDEO_ID&t=123).
    $parts = parse_url($url);
    if (!empty($parts['query'])) {
        // Turn "key=value&key2=value2" into an associative array.
        parse_str($parts['query'], $query);
        // Check for a "v" parameter that looks like a valid video ID.
        if (!empty($query['v']) && preg_match('#^[\\w-]{11}$#', $query['v'])) {
            return $query['v'];
        }
    }

    // If no valid ID was found, return null.
    return null;
}

// Handle form submissions (POST requests).
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    // "action" tells us what the user wants to do (add or delete).
    $action = $_POST['action'] ?? '';

    // Handle adding a new video.
    if ($action === 'add') {
        // Read and trim form inputs (remove extra spaces).
        $title = trim($_POST['title'] ?? '');
        $url = trim($_POST['url'] ?? '');
        $genre = trim($_POST['genre'] ?? '');
        $description = trim($_POST['description'] ?? '');

        // Basic validation: all fields are required.
        if ($title === '' || $url === '' || $genre === '' || $description === '') {
            $message = 'All fields are required.';
        } else {
            // Try to extract the YouTube video ID from the given URL.
            $videoId = extractYouTubeId($url);

            if ($videoId === null) {
                // If the URL doesn't look like a valid YouTube link.
                $message = 'Unable to determine YouTube video ID from the provided link.';
            } else {
                // Prepare an INSERT statement using named placeholders.
                // This helps prevent SQL injection and keeps code clean.
                $stmt = $pdo->prepare(
                    'INSERT INTO videos (title, url, video_id, genre, description, created_at)
                     VALUES (:title, :url, :video_id, :genre, :description, :created_at)'
                );

                // Execute the prepared statement with actual values.
                $stmt->execute([
                    ':title' => $title,
                    ':url' => $url,
                    ':video_id' => $videoId,
                    ':genre' => $genre,
                    ':description' => $description,
                    // Store the current time in a standard format (ISO 8601).
                    ':created_at' => (new DateTimeImmutable())->format(DateTimeInterface::ATOM),
                ]);

                $message = 'Video added successfully!';
            }
        }
    }
    // Handle deleting a video.
    elseif ($action === 'delete') {
        // Read the video ID from the form and cast it to an integer.
        $id = isset($_POST['id']) ? (int) $_POST['id'] : 0;

        if ($id > 0) {
            // Use a prepared statement to safely delete the row.
            $stmt = $pdo->prepare('DELETE FROM videos WHERE id = :id');
            $stmt->execute([':id' => $id]);
            $message = 'Video deleted.';
        }
    }
}

// Fetch all videos from the database, newest first.
$videosStmt = $pdo->query('SELECT * FROM videos ORDER BY created_at DESC');

// fetchAll(PDO::FETCH_ASSOC) returns an array of associative arrays.
$videos = $videosStmt->fetchAll(PDO::FETCH_ASSOC);

// Determine which video should be shown in the player.
// If the URL has ?watch=ID, use that. Otherwise, use the first video.
$selectedId = isset($_GET['watch']) ? (int) $_GET['watch'] : null;
$selectedVideo = null;

// Look through the list to find the selected video by ID.
if ($selectedId !== null) {
    foreach ($videos as $video) {
        if ((int) $video['id'] === $selectedId) {
            $selectedVideo = $video;
            break;
        }
    }
}

// If nothing is selected but there are videos, use the first one.
if ($selectedVideo === null && !empty($videos)) {
    $selectedVideo = $videos[0];
}

?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <!-- Make the page responsive on phones and tablets -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YouTube Video Manager</title>
    <style>
        /* Basic page styling using CSS */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background: #f3f4f6;
            color: #1f2933;
        }
        header {
            background: #1a73e8;
            color: white;
            padding: 1rem 2rem;
        }
        main {
            padding: 2rem;
            max-width: 1200px;
            margin: 0 auto;
        }
        .section {
            background: white;
            border-radius: 8px;
            padding: 1.5rem;
            margin-bottom: 1.5rem;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        form .field {
            display: flex;
            flex-direction: column;
            margin-bottom: 1rem;
        }
        form label {
            font-weight: bold;
            margin-bottom: 0.5rem;
        }
        form input[type="text"],
        form textarea {
            padding: 0.75rem;
            border: 1px solid #cbd5e1;
            border-radius: 4px;
            font-size: 1rem;
        }
        form textarea {
            resize: vertical;
            min-height: 100px;
        }
        form button {
            background: #1a73e8;
            color: white;
            border: none;
            padding: 0.75rem 1.5rem;
            font-size: 1rem;
            border-radius: 4px;
            cursor: pointer;
            transition: background 0.2s ease-in-out;
        }
        form button:hover {
            background: #1558b0;
        }
        .message {
            margin-bottom: 1rem;
            color: #0f5132;
        }
        .video-player iframe {
            width: 100%;
            height: 420px;
            border: none;
            border-radius: 8px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            padding: 0.75rem;
            border-bottom: 1px solid #e2e8f0;
            text-align: left;
            vertical-align: top;
        }
        th {
            background: #f8fafc;
        }
        .actions {
            display: flex;
            gap: 0.5rem;
        }
        .actions a,
        .actions button {
            padding: 0.5rem 1rem;
            border-radius: 4px;
            text-decoration: none;
            font-size: 0.9rem;
        }
        .play-button {
            background: #22c55e;
            color: white;
        }
        .play-button:hover {
            background: #16a34a;
        }
        .delete-button {
            background: #ef4444;
            color: white;
            border: none;
            cursor: pointer;
        }
        .delete-button:hover {
            background: #dc2626;
        }
        .description {
            white-space: pre-wrap; /* Preserve line breaks in descriptions */
        }
        @media (max-width: 768px) {
            .actions {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
<header>
    <h1>YouTube Video Manager</h1>
</header>
<main>
    <!-- Section: Form to add a new video -->
    <section class="section">
        <h2>Add a New Video</h2>

        <!-- Show any success or error message to the user -->
        <?php if ($message !== ''): ?>
            <p class="message">
                <?php echo htmlspecialchars($message, ENT_QUOTES, 'UTF-8'); ?>
            </p>
        <?php endif; ?>

        <!-- "Add video" form -->
        <form method="post">
            <!-- Hidden field tells PHP that this form is for "add" action -->
            <input type="hidden" name="action" value="add">

            <div class="field">
                <label for="title">Title</label>
                <input type="text" id="title" name="title" required>
            </div>

            <div class="field">
                <label for="url">YouTube Link</label>
                <input type="text" id="url" name="url" required>
            </div>

            <div class="field">
                <label for="genre">Genre</label>
                <input type="text" id="genre" name="genre" required>
            </div>

            <div class="field">
                <label for="description">Description</label>
                <textarea id="description" name="description" required></textarea>
            </div>

            <button type="submit">Add Video</button>
        </form>
    </section>

    <!-- Section: Selected video player -->
    <section class="section video-player">
        <h2>Selected Video</h2>

        <?php if ($selectedVideo): ?>
            <!-- Show the selected video's title -->
            <h3>
                <?php echo htmlspecialchars($selectedVideo['title'], ENT_QUOTES, 'UTF-8'); ?>
            </h3>

            <!-- Embed the YouTube video using the extracted video_id -->
            <iframe
                src="https://www.youtube.com/embed/<?php echo htmlspecialchars($selectedVideo['video_id'], ENT_QUOTES, 'UTF-8'); ?>"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen>
            </iframe>

            <!-- Show the genre and description -->
            <p>
                <strong>Genre:</strong>
                <?php echo htmlspecialchars($selectedVideo['genre'], ENT_QUOTES, 'UTF-8'); ?>
            </p>
            <p class="description">
                <?php
                // nl2br() converts line breaks to <br> tags for better formatting.
                echo nl2br(htmlspecialchars($selectedVideo['description'], ENT_QUOTES, 'UTF-8'));
                ?>
            </p>
        <?php else: ?>
            <!-- When no videos exist yet -->
            <p>No videos available yet. Add one above to get started!</p>
        <?php endif; ?>
    </section>

    <!-- Section: Table listing all videos -->
    <section class="section">
        <h2>All Videos</h2>

        <?php if (empty($videos)): ?>
            <p>No videos saved.</p>
        <?php else: ?>
            <table>
                <thead>
                <tr>
                    <th>Title</th>
                    <th>Genre</th>
                    <th>Description</th>
                    <th>Link</th>
                    <th>Actions</th>
                </tr>
                </thead>
                <tbody>
                <!-- Loop through all videos and show each in a table row -->
                <?php foreach ($videos as $video): ?>
                    <tr>
                        <td>
                            <?php echo htmlspecialchars($video['title'], ENT_QUOTES, 'UTF-8'); ?>
                        </td>
                        <td>
                            <?php echo htmlspecialchars($video['genre'], ENT_QUOTES, 'UTF-8'); ?>
                        </td>
                        <td class="description">
                            <?php echo nl2br(htmlspecialchars($video['description'], ENT_QUOTES, 'UTF-8')); ?>
                        </td>
                        <td>
                            <!-- Link to the original YouTube URL in a new tab -->
                            <a href="<?php echo htmlspecialchars($video['url'], ENT_QUOTES, 'UTF-8'); ?>"
                               target="_blank" rel="noopener noreferrer">
                                Open
                            </a>
                        </td>
                        <td>
                            <div class="actions">
                                <!-- "Play" button just reloads the page with ?watch=ID -->
                                <a class="play-button"
                                   href="?watch=<?php echo (int) $video['id']; ?>">
                                    Play
                                </a>

                                <!-- "Delete" form for this specific video -->
                                <form method="post"
                                      onsubmit="return confirm('Are you sure you want to delete this video?');">
                                    <input type="hidden" name="action" value="delete">
                                    <input type="hidden" name="id"
                                           value="<?php echo (int) $video['id']; ?>">
                                    <button type="submit" class="delete-button">
                                        Delete
                                    </button>
                                </form>
                            </div>
                        </td>
                    </tr>
                <?php endforeach; ?>
                </tbody>
            </table>
        <?php endif; ?>
    </section>
</main>
</body>
</html>

```

