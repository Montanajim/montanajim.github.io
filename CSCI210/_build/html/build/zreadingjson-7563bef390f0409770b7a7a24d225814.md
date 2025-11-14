# Reading json



This code displays a table of Harry Potter spells on a webpage. Here's a breakdown:

- HTML Structure:
  - Defines a basic webpage with a title ("Spells") and a content area.
  - Styles the content area and a table to improve presentation.
- PHP Script:
  - Retrieves JSON data (currently from a specific URL) containing spell information.
  - Decodes the JSON data into an array for easier access.
  - Builds an HTML table with headers for "Spell Name," "Incantation," "Spell Type," and "Effect."
  - Loops through each spell in the array and displays its details in a table row.



```php
<!DOCTYPE html>
<html>
<head>
  <title>Spells</title>
  <style>
    /* Style the table for better presentation */
    table {
      border-collapse: collapse; /* Remove borders between cells */
    }
    th {
      background-color: ivory; /* Set header background color */
      text-align: left; /* Align text left in headers */
    }
    tr:nth-child(even) {
      background-color: lightgrey; /* Alternate row background color */
    }
    .content {
      background-color: cornsilk; /* Set content area background color */
      margin: auto; /* Center the content horizontally */
      width: 65%; /* Set content area width to 50% */
    }
  </style>
</head>
<body>
<div class="content">
  <h1>Harry Potter Spells</h1>

  <?php

  // // Retrieve JSON data from a URL (replace with your actual URL)
  // $json = file_get_contents('url_here');
  // // Decode the JSON data into an object
  // $obj = json_decode($json);

  // Fetch JSON data from a specific URL (replace if needed)
  $url = 'https://flutter.locusnoesis.com/spellsinfo.php/';
  $json = file_get_contents($url);

  // Decode the JSON data into an array
  // Set second argument to true for associative array
  $spellsArr = json_decode($json, true); 
 

  // Start building the HTML table
  echo('<table border="1">
          <tr>
            <th>Spell Name</th>  <th>Incantation</th>
            <th>Spell Type</th>
            <th>Effect</th>
          </tr>');

  // Loop through each spell in the array
  for ($r = 0; $r < count($spellsArr); $r++) {
    echo('<tr>');

    // Access the current spell object
    $currentSpell = $spellsArr[$r];  

    // Loop through each property (key-value pair) of the current spell
    foreach ($currentSpell as $key => $value) {
      echo('<td>');
      echo($value);
      echo('</td>');
    }

    echo('</tr>');
  }

  echo('</table>');

  ?>
</div>
</body>
</html>
```

**Analysis:**

- The code displays a table of Harry Potter spells.
- It retrieves data (currently from a specific URL) in JSON format and parses it into an array.
- The code loops through the spells and displays each spell's properties (name, incantation, type, effect) in a table row.
- The styling section defines the table's appearance and the content area's layout.

**Improvements:**

- The commented-out section shows how to replace the placeholder URL with your actual data source.
- The `json_decode` function's second argument is set to `true` to ensure an associative array is returned, making it easier to access properties by their names.
- The code assumes the JSON data structure is consistent. Error handling could be added to handle unexpected data formats.

