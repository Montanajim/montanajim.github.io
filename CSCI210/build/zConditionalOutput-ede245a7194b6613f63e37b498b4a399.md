# Conditional Output: Two Ways to Format HTML

In web development, PHP often acts as the decision-maker behind what users see on a webpage. This example demonstrates how PHP can dynamically control HTML output based on user input from a simple form. By clicking **“true”** or **“false,”** the user triggers server-side logic that determines whether certain HTML elements are displayed. Two approaches are illustrated: **Section A**, which embeds HTML directly within PHP conditionals, and **Section B**, which uses PHP’s `echo()` function to output HTML as text. Both techniques achieve the same result but showcase different styles of blending PHP logic with presentation — an essential skill for building responsive, data-driven web applications.

```php
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PHP Conditional Display</title>

    <style>
        /* Basic styling for centered container */
        .div1 {
            width: 50%;
            background-color: cornsilk;
            margin: 50px auto;
        }
    </style>
</head>

<body>
    <div class="div1">
        <h1>Conditional PHP Example</h1>

        <!-- Simple form with two submit buttons -->
        <form method="POST" action="">
            <input type="submit" name="choice" value="true"> &nbsp;
            <input type="submit" name="choice" value="false"><br>
        </form>

        <?php
            // Check if 'choice' was submitted via POST
            if (!empty($_POST['choice'])) {

                // Use ternary operator to set $run to true or false
                $run = ($_POST['choice'] == "true") ? true : false;

                // --- Section A ---
                // If $run is true, output HTML directly (PHP and HTML mixed)
                if ($run) { ?>
                    <h1>This works</h1>
                    <p>yada yada yada yada yada yada yada </p>
                    <p>yada yada yada yada yada yada yada </p>
                    <p>yada yada yada yada yada yada yada </p>
                <?php }

                // --- Section B ---
                // Same result, but outputs HTML using echo and heredoc-style string
                if ($run) {
                    echo ('
                        <h1>This works</h1>
                        <p>yada yada yada yada yada yada yada </p>
                        <p>yada yada yada yada yada yada yada </p>
                        <p>yada yada yada yada yada yada yada </p>
                    ');
                }
            }
        ?>
    </div>
</body>
</html>
```

### Quick Explanation

- **Section A**: Embeds HTML directly inside PHP’s conditional block. Easy to read, but not ideal for large dynamic sections.
- **Section B**: Uses `echo()` to print HTML as a string — tidier for logic-heavy pages or when generating HTML dynamically.
- **Ternary Operator**: `condition ? true_value : false_value` — a shorthand for simple `if/else` assignments.

