# XSS Examples

This short chapter demonstrates two common XSS scenarios and how to fix them:

1. **Reflected XSS** — user input (from the query string) is immediately written back into the page. The vulnerable example prints the raw query value; the fixed example escapes it with `htmlspecialchars` so any injected `<script>` becomes harmless text.
2. **Stored XSS (toy guestbook)** — a user-submitted message is stored in session and later rendered for all visitors. The vulnerable example renders the raw stored value, which will execute in the browser. The fixed example sanitizes stored values on output using a small `sanitize()` helper that performs `trim()`, `strip_tags()` and `htmlspecialchars()` (ENT_QUOTES, UTF-8).

Read the inline comments — I call out the vulnerable lines and explain the remediation. Use these pages in a classroom or lab to safely demonstrate how an attacker’s `<script>` turns into harmless text once properly escaped.

------

## `index.php` — home page with demo links

```php
<?php
// index.php
// Simple landing page linking to the vulnerable and fixed demo pages.
//
// This file is purely HTML. Links include an example exploit payload to
// illustrate how a reflected XSS payload would look in the query string.
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1.0" />
    <title>XSS Home Demo</title>
    <style>
        .div1 {
            width: 50%;
            background-color: cornsilk;
            margin: 50px auto 0 auto;
            padding: 1rem;
            border-radius: 6px;
            font-family: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
        }
        a { display:block; margin:8px 0; }
    </style>
</head>
<body>
    <div class="div1">
        <h1>XSS Demos</h1>

        <!--
          The query string contains a classic demo payload:
          ?q=<script>alert('Hacked')</script>
        -->
        <a href="page1_reflect.php?q=<script>alert('Hacked')</script>">
            Page 1 — Reflect (VULNERABLE)
        </a>

        <a href="page1_reflect_prevent.php?q=<script>alert('Hacked')</script>">
            Page 1 — Reflect (Prevented)
        </a>

        <a href="stored_hacked.php">Stored — Guestbook (VULNERABLE)</a>
        <a href="stored_hacked_prevent.php">Stored — Guestbook (Prevented)</a>

        <a href="index.php">Home</a>
    </div>
</body>
</html>
```

------

## `page1_reflect.php` — **vulnerable** reflected XSS (don't use in production)

```php
<?php
// page1_reflect.php
// Demonstrates reflected XSS by echoing a query parameter directly.
// *** VULNERABLE: the raw $q value is injected into the HTML output. ***

// Use null coalescing so page still works without ?q= in the URL.
$q = $_GET['q'] ?? '';
?>
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <title>Hacked (Reflect - Vulnerable)</title>
    <style>
        .div1 { width:50%; background:cornsilk; margin:50px auto; padding:1rem; }
    </style>
</head>
<body>
    <div class="div1">
        <h1>Search</h1>

        <!-- VULNERABLE LINE: raw echo of user input -->
        <!-- If q contains <script>... it will run in the visitor's browser. -->
        <p>You searched for: <?= $q ?></p> <!-- VULNERABLE -->

        <br>
        <a href="index.php">Home</a>
    </div>
</body>
</html>
```

**Teaching note:** open `page1_reflect.php?q=<script>alert('Hacked')</script>` to see how an attacker-supplied `<script>` executes. The vulnerability comes from outputting unescaped input into an HTML context.

------

## `page1_reflect_prevent.php` — reflected XSS **fixed**

```php
<?php
// page1_reflect_prevent.php
// Fixed version of reflected XSS demo. Escape output with htmlspecialchars
// so any HTML tags supplied in the query string are rendered as text.

$q = $_GET['q'] ?? '';

// Use a small helper for clarity (context-aware escaping for HTML).
function e($s) {
    // ENT_QUOTES encodes both double and single quotes.
    // 'UTF-8' ensures proper encoding for multibyte characters.
    return htmlspecialchars((string)$s, ENT_QUOTES, 'UTF-8');
}
?>
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <title>Hacked (Reflect - Prevented)</title>
    <style>.div1 { width:50%; background:cornsilk; margin:50px auto; padding:1rem; }</style>
</head>
<body>
    <div class="div1">
        <h1>Search</h1>

        <!-- SAFE OUTPUT: any < or > in $q are converted to &lt; &gt; -->
        <p>You searched for: <?= e($q) ?></p> <!-- NOT VULNERABLE -->

        <br>
        <a href="index.php">Home</a>
    </div>
</body>
</html>
```

**Teaching note:** `htmlspecialchars()` is the appropriate escape for HTML body content. If you output into other contexts (e.g., attribute, JS, CSS, URL) you must use a different encoding or a trusted library for context-aware encoding.

------

## `stored_hacked.php` — **vulnerable** stored XSS guestbook

```php
<?php
// stored_hacked.php
// Toy guestbook that demonstrates stored XSS by rendering session-stored messages
// without escaping them. DO NOT deploy this as-is.

session_start();

// Place a malicious demo message in session to simulate previously stored content.
$_SESSION['messages'] = ["<script>alert('hacked stored!')</script>"];

// Load messages for display.
$messages = $_SESSION['messages'] ?? [];

// If the user posts something, the code below intentionally follows your original
// request: keep the `if (!empty($_POST['msg']))` check exactly as provided.
if (!empty($_POST['msg'])) {
    // NOTE: this block is intentionally left minimal to match the original demo.
    // In the vulnerable demo we would append raw values to the messages array.
    // For clarity we simply reload messages here (no safe write).
    $messages = $_SESSION['messages'];
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <title>Stored — Guestbook (Vulnerable)</title>
    <style>.div1 { width:50%; background:cornsilk; margin:50px auto; padding:1rem; }</style>
</head>
<body>
    <div class="div1">
        <h1>Guestbook</h1>

        <!-- Simple form to demonstrate posting -->
        <form method="post" action="">
            <input name="msg" placeholder="Say hi" value="Hello">
            <button>POST</button>
        </form>

        <ul>
            <?php foreach ($messages as $m): ?>
                <!-- VULNERABLE: stored messages are printed raw, so a stored <script> will execute -->
                <li><?= (string) $m ?></li> <!-- VULNERABLE -->
            <?php endforeach; ?>
        </ul>

        <br>
        <a href="index.php">Home</a>
    </div>
</body>
</html>
```

**Teaching note:** Stored XSS occurs when untrusted data is persisted (database, session, file) and later served to users without cleaning/escaping. The attack becomes more dangerous because many visitors might execute the injected script.

------

## `stored_hacked_prevent.php` — stored XSS **prevented** (sanitizing on output)

```php
<?php
// stored_hacked_prevent.php
// Prevents stored XSS by escaping/sanitizing messages before output.
// Uses the same `if (!empty($_POST['msg']))` check as requested.

session_start();

// Demo initial message that simulates previously stored malicious content.
$_SESSION['messages'] = ["<script>alert('hacked stored!')</script>"];

// Retrieve messages array from session
$messages = $_SESSION['messages'] ?? [];

// Keep original check as requested (no substitution)
if (!empty($_POST['msg'])) {
    // In a real app we would append the submitted message to the session or DB.
    // For the classroom demo we show the flow but avoid writing raw content.
    $messages = $_SESSION['messages'];
}

/**
 * sanitize()
 * - trim() removes leading/trailing whitespace
 * - strip_tags() removes HTML/PHP tags
 * - htmlspecialchars() escapes remaining special characters for HTML output
 *
 * This function is defensive and simple — it's for demonstration and classroom use.
 * In production consider more context-aware measures (e.g., policies, CSP, output encoding libraries).
 */
function sanitize($value)
{
    $value = trim((string)$value);                       // trim whitespace
    $value = strip_tags($value);                        // remove HTML tags
    $value = htmlspecialchars($value, ENT_QUOTES, 'UTF-8'); // escape for HTML context
    return $value;
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <title>Stored — Guestbook (Prevented)</title>
    <style>.div1 { width:50%; background:cornsilk; margin:50px auto; padding:1rem; }</style>
</head>
<body>
    <div class="div1">
        <h1>Guestbook — Prevented</h1>

        <form method="post" action="">
            <input name="msg" placeholder="Say hi" value="Hello">
            <button>POST</button>
        </form>

        <ul>
            <?php foreach ($messages as $m): ?>
                <!-- SAFE: sanitize() neutralizes script tags and encodes special chars -->
                <li><?= sanitize($m) ?></li> <!-- NOT VULNERABLE -->
            <?php endforeach; ?>
        </ul>

        <br>
        <a href="index.php">Home</a>
    </div>
</body>
</html>
```

**Teaching note:** the safest approach is to **escape on output** for the context you are rendering into. Sanitizing on input can help (reduce stored attack surface), but **escaping at output** is the strongest, context-specific defense.

------

## Observations

1. Visit `page1_reflect.php?q=<script>alert('XSS')</script>` and then `page1_reflect_prevent.php?q=<script>alert('XSS')</script>` — compare behavior.

2. Visit `stored_hacked.php` and observe the alert from the session-stored message. Then load `stored_hacked_prevent.php` to see the sanitized result.

3. Discuss: what happens if you put `onerror="..."` into an `<img>` tag inside a message? (Context matters — attribute vs body.)

4. Discuss Content Security Policy (CSP) as a further mitigation, and why it’s complementary (not a substitute) to proper escaping.

   ---

##### 10/2025

