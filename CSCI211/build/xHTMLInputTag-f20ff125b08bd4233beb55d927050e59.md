# HTML Input Tag

![Picture Of a form utilizing all of the input type attributes](./assets/inputtag.png)

## Using Inline  (inline event handlers)

In the **Inline** version, behavior is attached directly inside the HTML using attributes like `oninput="..."` and `onchange="..."`. That means the HTML doesn’t just describe structure—it also tells the browser *what code to run* when something happens. It’s immediate and readable for beginners: you can point to a single line and say “this fires the function.”

**Best use cases:** tiny demos, learning exercises, quick one-off prototypes where clarity beats architecture.
 **Worst use cases:** real applications, shared codebases, or anything you expect to maintain. Inline handlers get messy fast, duplicate logic, and blur separation of concerns. It’s also harder to refactor because your behavior is scattered across markup.

```html
<!DOCTYPE html>
<!--
  This document demonstrates many HTML <input> types.
  Each input triggers a JavaScript function that logs
  user interaction directly to the DOM.
-->

<head>
  <!-- Page title shown in the browser tab -->
  <title>Input types</title>

  <style>
    /*
      Simple container styling to center the demo
      and make it visually distinct from the page background
    */
    .div1 {
      width: 75%;
      background-color: cornsilk;
      padding: 25px;
      margin-left: auto;
      margin-right: auto;
      margin-top: 50px;
      margin-bottom: 50px;
    }
  </style>
</head>

<body>

  <!-- Main demo container -->
  <div class="div1">

    <!-- Page heading -->
    <h1>HTML Input Types – DOM Logging</h1>
    <p>Every interaction is logged below.</p>

    <!--
      Log area:
      JavaScript dynamically inserts messages here
      instead of using console.log()
    -->
    <div id="log" style="border:1px solid #444; 
      padding:10px; 
      height:200px; 
      overflow-y:auto; 
      margin-bottom: 20px;
      background:#f9f9f9;">
    </div>

    <!--
      Demo form:
      Each input element demonstrates a different input type.
      Event handlers call JavaScript functions on change or input.
    -->
    <form id="demoForm">
      <table>

        <!-- Text input (fires on every keystroke) -->
        <tr>
          <td><label for="textInput">Text:</label></td>
          <td><input type="text" id="textInput" oninput="handleText(this.value)"></td>
        </tr>

        <!-- Password input (value intentionally hidden in logs) -->
        <tr>
          <td><label for="passwordInput">Password:</label></td>
          <td><input type="password" id="passwordInput" onchange="handlePassword()"></td>
        </tr>

        <!-- Email input with built-in browser validation -->
        <tr>
          <td><label for="emailInput">Email:</label></td>
          <td><input type="email" id="emailInput" onchange="handleEmail(this.value)"></td>
        </tr>

        <!-- Numeric input -->
        <tr>
          <td><label for="numberInput">Number:</label></td>
          <td><input type="number" id="numberInput" onchange="handleNumber(this.value)"></td>
        </tr>

        <!-- Search input -->
        <tr>
          <td><label for="searchInput">Search:</label></td>
          <td><input type="search" id="searchInput" oninput="handleSearch(this.value)"></td>
        </tr>

        <!-- Telephone input with a validation pattern -->
        <tr>
          <td><label for="telInput">Tel:</label></td>
          <td>
            <input type="tel" id="telInput"
              onchange="handleTel(this.value)"
              placeholder="555-555-5555"
              pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}">
          </td>
        </tr>

        <!-- URL input with HTTPS pattern enforcement -->
        <tr>
          <td><label for="urlInput">URL:</label></td>
          <td><input type="url" id="urlInput" onchange="handleURL(this.value)" pattern="https://.*"></td>
        </tr>

        <!-- Date picker -->
        <tr>
          <td><label for="dateInput">Date:</label></td>
          <td><input type="date" id="dateInput" onchange="handleDate(this.value)"></td>
        </tr>

        <!-- Time picker -->
        <tr>
          <td><label for="timeInput">Time:</label></td>
          <td><input type="time" id="timeInput" onchange="handleTime(this.value)"></td>
        </tr>

        <!-- Combined date and time picker -->
        <tr>
          <td><label for="datetimeInput">DateTime-Local:</label></td>
          <td><input type="datetime-local" id="datetimeInput" onchange="handleDateTime(this.value)"></td>
        </tr>

        <!-- Month picker -->
        <tr>
          <td><label for="monthInput">Month:</label></td>
          <td><input type="month" id="monthInput" onchange="handleMonth(this.value)"></td>
        </tr>

        <!-- Week picker -->
        <tr>
          <td><label for="weekInput">Week:</label></td>
          <td><input type="week" id="weekInput" onchange="handleWeek(this.value)"></td>
        </tr>

        <!-- Range slider -->
        <tr>
          <td><label for="rangeInput">Range:</label></td>
          <td><input type="range" id="rangeInput" min="0" max="100" oninput="handleRange(this.value)"></td>
        </tr>

        <!-- Color picker -->
        <tr>
          <td><label for="colorInput">Color:</label></td>
          <td>
            <input type="color" id="colorInput"
              onchange="handleColor(this.value)">
          </td>
        </tr>

        <!-- Checkbox -->
        <tr>
          <td><label for="checkboxInput">Checkbox:</label></td>
          <td><input type="checkbox" id="checkboxInput" onchange="handleCheckbox(this.checked)"></td>
        </tr>

        <!-- Radio buttons (grouped by name attribute) -->
        <tr>
          <td><label for="radioA">Radio A:</label></td>
          <td><input type="radio" id="radioA" name="group1" value="A" onchange="handleRadio(this.value)"></td>
        </tr>
        <tr>
          <td><label for="radioB">Radio B:</label></td>
          <td><input type="radio" id="radioB" name="group1" value="B" onchange="handleRadio(this.value)"></td>
        </tr>

        <!-- File upload -->
        <tr>
          <td><label for="fileInput">File:</label></td>
          <td><input type="file" id="fileInput" onchange="handleFile(this.files)"></td>
        </tr>

        <!-- Hidden field (not visible to users, still submitted) -->
        <tr style="display: none;">
          <td colspan="2">
            <input type="hidden" id="hiddenInput" value="classified">
          </td>
        </tr>

        <!-- Form control buttons -->
        <tr>
          <td colspan="2" style="text-align: center;">
            <input type="button" value="Button" onclick="handleButton()">
            <input type="reset" value="Reset" onclick="handleReset()">
            <input type="submit" value="Submit">
          </td>
        </tr>

      </table>
    </form>
  </div>

  <script>
    /*
      Core logging function.
      Appends messages to the log div and auto-scrolls.
    */
    function log(message) {

      // Clear log when the form is reset
      if (message === "Form reset") {
        document.getElementById("log").innerHTML = "";
      }

      const logDiv = document.getElementById("log");
      const entry = document.createElement("div");
      entry.textContent = message;
      logDiv.appendChild(entry);

      // Keep newest log entry visible
      logDiv.scrollTop = logDiv.scrollHeight;
    }

    // Individual handlers for each input type
    function handleText(value) { log("Text: " + value); }
    function handlePassword() { log("Password changed (value hidden, on purpose)"); }
    function handleEmail(value) { log("Email: " + value); }
    function handleNumber(value) { log("Number: " + value); }
    function handleSearch(value) { log("Search: " + value); }
    function handleTel(value) { log("Tel: " + value); }
    function handleURL(value) { log("URL: " + value); }
    function handleDate(value) { log("Date: " + value); }
    function handleTime(value) { log("Time: " + value); }
    function handleDateTime(value) { log("DateTime: " + value); }
    function handleMonth(value) { log("Month: " + value); }
    function handleWeek(value) { log("Week: " + value); }
    function handleRange(value) { log("Range: " + value); }
    function handleColor(value) { log("Color: " + value); }
    function handleCheckbox(checked) { log("Checkbox checked: " + checked); }
    function handleRadio(value) { log("Radio selected: " + value); }

    // File input handler (optional chaining avoids errors)
    function handleFile(files) {
      log("File selected: " + (files[0]?.name || "none"));
    }

    function handleButton() { log("Button clicked"); }
    function handleReset() { log("Form reset"); }

    /*
      Form submission handler.
      Prevents actual submission and logs hidden input data.
    */
    document.getElementById("demoForm").onsubmit = function (e) {
      e.preventDefault();
      log("Form submitted");
      log("Hidden value: " + document.getElementById("hiddenInput").value);
    };
  </script>

</body>

```



## Using Listeners (addEventListener)

In the **Listeners** version, the HTML stays clean and JavaScript does the wiring with `addEventListener`. This is the “grown-up” baseline: structure in HTML, behavior in JS. It also avoids common inline pitfalls like mixing quoting rules, creating hidden dependencies, and accidentally triggering code before the DOM is ready.

**Best use cases:** most projects, especially when you want maintainable code and clear separation of concerns. Great for small-to-medium forms where each input has unique logic.
 **Worst use cases:** very large forms with many similar elements, where attaching a separate listener to every element becomes repetitive and noisy (and sometimes slightly wasteful).

```html
<!DOCTYPE html>
<!--
  Demonstration of HTML <input> types using JavaScript event listeners.
  All events are attached in JavaScript to reinforce separation of concerns.

  Below is the same behavior, same UI, same logging—but 
  all inline event handlers are removed and replaced with addEventListener. 
The comments now explicitly call out why this approach matters.
-->

<head>
  <title>Input types</title>

  <style>
    /* Visual container for the demo */
    .div1 {
      width: 75%;
      background-color: cornsilk;
      padding: 25px;
      margin: 50px auto;
    }
  </style>
</head>

<body>

  <div class="div1">
    <h1>HTML Input Types – DOM Logging</h1>
    <h2>Adding Event Listeners</h2>
    <p>Every interaction is logged below.</p>

    <!-- Log output area -->
    <div id="log" style="border:1px solid #444;
      padding:10px;
      height:200px;
      overflow-y:auto;
      margin-bottom:20px;
      background:#f9f9f9;">
    </div>

    <!--
      Form contains examples of many HTML input types.
      No inline JavaScript is used here.
    -->
    <form id="demoForm">
      <table>
        <tr><td>Text:</td><td><input type="text" id="textInput"></td></tr>
        <tr><td>Password:</td><td><input type="password" id="passwordInput"></td></tr>
        <tr><td>Email:</td><td><input type="email" id="emailInput"></td></tr>
        <tr><td>Number:</td><td><input type="number" id="numberInput"></td></tr>
        <tr><td>Search:</td><td><input type="search" id="searchInput"></td></tr>
        <tr>
          <td>Tel:</td>
          <td>
            <input type="tel" id="telInput"
              placeholder="555-555-5555"
              pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}">
          </td>
        </tr>
        <tr><td>URL:</td><td><input type="url" id="urlInput" pattern="https://.*"></td></tr>
        <tr><td>Date:</td><td><input type="date" id="dateInput"></td></tr>
        <tr><td>Time:</td><td><input type="time" id="timeInput"></td></tr>
        <tr><td>DateTime:</td><td><input type="datetime-local" id="datetimeInput"></td></tr>
        <tr><td>Month:</td><td><input type="month" id="monthInput"></td></tr>
        <tr><td>Week:</td><td><input type="week" id="weekInput"></td></tr>
        <tr><td>Range:</td><td><input type="range" id="rangeInput" min="0" max="100"></td></tr>
        <tr><td>Color:</td><td><input type="color" id="colorInput"></td></tr>
        <tr><td>Checkbox:</td><td><input type="checkbox" id="checkboxInput"></td></tr>
        <tr><td>Radio A:</td><td><input type="radio" name="group1" value="A" id="radioA"></td></tr>
        <tr><td>Radio B:</td><td><input type="radio" name="group1" value="B" id="radioB"></td></tr>
        <tr><td>File:</td><td><input type="file" id="fileInput"></td></tr>

        <!-- Hidden input demonstrates non-visible form data -->
        <tr style="display:none;">
          <td colspan="2"><input type="hidden" id="hiddenInput" value="classified"></td>
        </tr>

        <tr>
          <td colspan="2" style="text-align:center;">
            <input type="button" id="buttonInput" value="Button">
            <input type="reset" value="Reset">
            <input type="submit" value="Submit">
          </td>
        </tr>
      </table>
    </form>
  </div>

  <script>
    /*
      Utility function to append messages to the log div.
      Keeps the UI responsive and readable.
    */
    function log(message) {
      if (message === "Form reset") {
        document.getElementById("log").innerHTML = "";
      }

      const logDiv = document.getElementById("log");
      const entry = document.createElement("div");
      entry.textContent = message;
      logDiv.appendChild(entry);
      logDiv.scrollTop = logDiv.scrollHeight;
    }

    /*
      Event listeners are attached AFTER the DOM loads.
      This avoids race conditions and inline JavaScript.
    */
    document.addEventListener("DOMContentLoaded", () => {

      document.getElementById("textInput")
        .addEventListener("input", e => log("Text: " + e.target.value));

      document.getElementById("passwordInput")
        .addEventListener("change", () => log("Password changed (value hidden, on purpose)"));

      document.getElementById("emailInput")
        .addEventListener("change", e => log("Email: " + e.target.value));

      document.getElementById("numberInput")
        .addEventListener("change", e => log("Number: " + e.target.value));

      document.getElementById("searchInput")
        .addEventListener("input", e => log("Search: " + e.target.value));

      document.getElementById("telInput")
        .addEventListener("change", e => log("Tel: " + e.target.value));

      document.getElementById("urlInput")
        .addEventListener("change", e => log("URL: " + e.target.value));

      document.getElementById("dateInput")
        .addEventListener("change", e => log("Date: " + e.target.value));

      document.getElementById("timeInput")
        .addEventListener("change", e => log("Time: " + e.target.value));

      document.getElementById("datetimeInput")
        .addEventListener("change", e => log("DateTime: " + e.target.value));

      document.getElementById("monthInput")
        .addEventListener("change", e => log("Month: " + e.target.value));

      document.getElementById("weekInput")
        .addEventListener("change", e => log("Week: " + e.target.value));

      document.getElementById("rangeInput")
        .addEventListener("input", e => log("Range: " + e.target.value));

      document.getElementById("colorInput")
        .addEventListener("change", e => log("Color: " + e.target.value));

      document.getElementById("checkboxInput")
        .addEventListener("change", e => log("Checkbox checked: " + e.target.checked));

      document.querySelectorAll("input[name='group1']")
        .forEach(radio =>
          radio.addEventListener("change", e => log("Radio selected: " + e.target.value))
        );

      document.getElementById("fileInput")
        .addEventListener("change", e =>
          log("File selected: " + (e.target.files[0]?.name || "none"))
        );

      document.getElementById("buttonInput")
        .addEventListener("click", () => log("Button clicked"));

      document.getElementById("demoForm")
        .addEventListener("reset", () => log("Form reset"));

      document.getElementById("demoForm")
        .addEventListener("submit", e => {
          e.preventDefault();
          log("Form submitted");
          log("Hidden value: " + document.getElementById("hiddenInput").value);
        });
    });
  </script>
</body>

```





## Using Delegation (event delegation)

In the **Delegation** version, you attach *one* listener (or a few) to the parent container (here, the `<form>`). Events bubble up from the input to the form, and your code inspects `event.target` to figure out which input triggered it. This is the “one guard at the door checks everyone’s ID” approach.

**Best use cases:** large dynamic UIs, long forms, tables of inputs, and interfaces where elements are added/removed after page load. It’s also excellent when many inputs share similar handling.
 **Worst use cases:** complex forms where different inputs need radically different event timing or custom rules. Delegation can become a logic maze if you pile too many special cases into one handler.

```html
<!DOCTYPE html>
<!--
  HTML input types demo using EVENT DELEGATION.
  A single event listener handles all inputs by inspecting the event target.

  What follows is event delegation: one listener on the form, 
  the DOM bubbling events upward, and JavaScript calmly deciding what happened. 
  Fewer listeners, less repetition, clearer intent. 
  The browser already did half the work.
-->

<head>
  <title>Input types</title>

  <style>
    .div1 {
      width: 75%;
      background-color: cornsilk;
      padding: 25px;
      margin: 50px auto;
    }
  </style>
</head>

<body>

  <div class="div1">
    <h1>HTML Input Types – Event Delegation</h1>
    <p>All input events are handled by one listener.</p>

    <!-- Log output -->
    <div id="log" style="border:1px solid #444;
      padding:10px;
      height:200px;
      overflow-y:auto;
      margin-bottom:20px;
      background:#f9f9f9;">
    </div>

    <!-- Form with many input types -->
    <form id="demoForm">
      <table>
        <tr><td>Text:</td><td><input type="text" id="textInput"></td></tr>
        <tr><td>Password:</td><td><input type="password" id="passwordInput"></td></tr>
        <tr><td>Email:</td><td><input type="email" id="emailInput"></td></tr>
        <tr><td>Number:</td><td><input type="number" id="numberInput"></td></tr>
        <tr><td>Search:</td><td><input type="search" id="searchInput"></td></tr>
        <tr><td>Tel:</td><td><input type="tel" id="telInput"></td></tr>
        <tr><td>URL:</td><td><input type="url" id="urlInput"></td></tr>
        <tr><td>Date:</td><td><input type="date" id="dateInput"></td></tr>
        <tr><td>Time:</td><td><input type="time" id="timeInput"></td></tr>
        <tr><td>DateTime:</td><td><input type="datetime-local" id="datetimeInput"></td></tr>
        <tr><td>Month:</td><td><input type="month" id="monthInput"></td></tr>
        <tr><td>Week:</td><td><input type="week" id="weekInput"></td></tr>
        <tr><td>Range:</td><td><input type="range" id="rangeInput" min="0" max="100"></td></tr>
        <tr><td>Color:</td><td><input type="color" id="colorInput"></td></tr>
        <tr><td>Checkbox:</td><td><input type="checkbox" id="checkboxInput"></td></tr>
        <tr>
          <td>Radio A:</td>
          <td><input type="radio" name="group1" value="A"></td>
        </tr>
        <tr>
          <td>Radio B:</td>
          <td><input type="radio" name="group1" value="B"></td>
        </tr>
        <tr><td>File:</td><td><input type="file" id="fileInput"></td></tr>

        <!-- Hidden input -->
        <tr style="display:none;">
          <td colspan="2"><input type="hidden" id="hiddenInput" value="classified"></td>
        </tr>

        <tr>
          <td colspan="2" style="text-align:center;">
            <input type="button" id="buttonInput" value="Button">
            <input type="reset" value="Reset">
            <input type="submit" value="Submit">
          </td>
        </tr>
      </table>
    </form>
  </div>

  <script>
    /*
      Writes a message to the log div and auto-scrolls.
    */
    function log(message) {
      if (message === "Form reset") {
        document.getElementById("log").innerHTML = "";
      }

      const logDiv = document.getElementById("log");
      const entry = document.createElement("div");
      entry.textContent = message;
      logDiv.appendChild(entry);
      logDiv.scrollTop = logDiv.scrollHeight;
    }

    /*
      One listener. One decision point.
      The event bubbles up from the input to the form.
    */
    document.addEventListener("DOMContentLoaded", () => {

      const form = document.getElementById("demoForm");

      form.addEventListener("input", handleEvent);
      form.addEventListener("change", handleEvent);

      form.addEventListener("reset", () => log("Form reset"));

      form.addEventListener("submit", e => {
        e.preventDefault();
        log("Form submitted");
        log("Hidden value: " + document.getElementById("hiddenInput").value);
      });

      document.getElementById("buttonInput")
        .addEventListener("click", () => log("Button clicked"));
    });

    /*
      Centralized event handler.
      Determines behavior based on input type and attributes.
    */
    function handleEvent(e) {

      const el = e.target;

      if (el.tagName !== "INPUT") return;

      switch (el.type) {

        case "text":
          log("Text: " + el.value);
          break;

        case "password":
          log("Password changed (value hidden, on purpose)");
          break;

        case "email":
          log("Email: " + el.value);
          break;

        case "number":
          log("Number: " + el.value);
          break;

        case "search":
          log("Search: " + el.value);
          break;

        case "tel":
          log("Tel: " + el.value);
          break;

        case "url":
          log("URL: " + el.value);
          break;

        case "date":
          log("Date: " + el.value);
          break;

        case "time":
          log("Time: " + el.value);
          break;

        case "datetime-local":
          log("DateTime: " + el.value);
          break;

        case "month":
          log("Month: " + el.value);
          break;

        case "week":
          log("Week: " + el.value);
          break;

        case "range":
          log("Range: " + el.value);
          break;

        case "color":
          log("Color: " + el.value);
          break;

        case "checkbox":
          log("Checkbox checked: " + el.checked);
          break;

        case "radio":
          log("Radio selected: " + el.value);
          break;

        case "file":
          log("File selected: " + (el.files[0]?.name || "none"));
          break;
      }
    }
  </script>
</body>

```



## Using Objects (data-driven handlers)

In the **Objects** version, you keep delegation, but replace the long `switch` statement with an **object lookup table** that maps an input’s type (like `"email"` or `"date"`) to the appropriate handler function. This is the cleanest scaling strategy: adding a new input often becomes “add one row to the handler table.”

**Best use cases:** scalable systems, maintainable demos, codebases where you want to add new behavior without editing a monster conditional. This is also a stepping stone toward more advanced patterns (config-driven forms, reusable components, validation maps).
 **Worst use cases:** when the type alone isn’t enough to determine behavior. If two text inputs need different logic, mapping only by `type` can be too blunt—then you’ll want to dispatch by `id`, `name`, or `data-*` attributes instead.

```html
<!DOCTYPE html>
<!--
  HTML input types demo using:
    - Event delegation (one listener for many inputs)
    - Data-driven handlers (mapping input types to functions)

  same interface, same behavior, 
  but now the JavaScript is data-driven. 
  Instead of a long switch, we have a lookup table (an object) 
  that maps input types to handler functions.
-->

<head>
  <title>Input types</title>

  <style>
    .div1 {
      width: 75%;
      background-color: cornsilk;
      padding: 25px;
      margin: 50px auto;
    }
  </style>
</head>

<body>

  <div class="div1">
    <h1>HTML Input Types – Data-Driven Event Handling</h1>
    <p>Input types are mapped to handler functions through a lookup table.</p>

    <!-- Log output -->
    <div id="log" style="border:1px solid #444;
      padding:10px;
      height:200px;
      overflow-y:auto;
      margin-bottom:20px;
      background:#f9f9f9;">
    </div>

    <!-- Form with many input types -->
    <form id="demoForm">
      <table>
        <tr><td>Text:</td><td><input type="text" id="textInput"></td></tr>
        <tr><td>Password:</td><td><input type="password" id="passwordInput"></td></tr>
        <tr><td>Email:</td><td><input type="email" id="emailInput"></td></tr>
        <tr><td>Number:</td><td><input type="number" id="numberInput"></td></tr>
        <tr><td>Search:</td><td><input type="search" id="searchInput"></td></tr>
        <tr><td>Tel:</td><td><input type="tel" id="telInput"></td></tr>
        <tr><td>URL:</td><td><input type="url" id="urlInput"></td></tr>
        <tr><td>Date:</td><td><input type="date" id="dateInput"></td></tr>
        <tr><td>Time:</td><td><input type="time" id="timeInput"></td></tr>
        <tr><td>DateTime:</td><td><input type="datetime-local" id="datetimeInput"></td></tr>
        <tr><td>Month:</td><td><input type="month" id="monthInput"></td></tr>
        <tr><td>Week:</td><td><input type="week" id="weekInput"></td></tr>
        <tr><td>Range:</td><td><input type="range" id="rangeInput" min="0" max="100"></td></tr>
        <tr><td>Color:</td><td><input type="color" id="colorInput"></td></tr>
        <tr><td>Checkbox:</td><td><input type="checkbox" id="checkboxInput"></td></tr>
        <tr>
          <td>Radio A:</td>
          <td><input type="radio" name="group1" value="A"></td>
        </tr>
        <tr>
          <td>Radio B:</td>
          <td><input type="radio" name="group1" value="B"></td>
        </tr>
        <tr><td>File:</td><td><input type="file" id="fileInput"></td></tr>

        <!-- Hidden input -->
        <tr style="display:none;">
          <td colspan="2"><input type="hidden" id="hiddenInput" value="classified"></td>
        </tr>

        <tr>
          <td colspan="2" style="text-align:center;">
            <input type="button" id="buttonInput" value="Button">
            <input type="reset" value="Reset">
            <input type="submit" value="Submit">
          </td>
        </tr>
      </table>
    </form>
  </div>

  <script>
    /*
      Writes a message to the log div and auto-scrolls.
    */
    function log(message) {
      if (message === "Form reset") {
        document.getElementById("log").innerHTML = "";
      }

      const logDiv = document.getElementById("log");
      const entry = document.createElement("div");
      entry.textContent = message;
      logDiv.appendChild(entry);
      logDiv.scrollTop = logDiv.scrollHeight;
    }

    /*
      Handler table:
      Keys are input "type" values.
      Values are functions that know how to log that type.
      This replaces a long switch statement.
    */
    const inputHandlers = {
      text: el => log("Text: " + el.value),
      password: el => log("Password changed (value hidden, on purpose)"),
      email: el => log("Email: " + el.value),
      number: el => log("Number: " + el.value),
      search: el => log("Search: " + el.value),
      tel: el => log("Tel: " + el.value),
      url: el => log("URL: " + el.value),
      date: el => log("Date: " + el.value),
      time: el => log("Time: " + el.value),
      "datetime-local": el => log("DateTime: " + el.value),
      month: el => log("Month: " + el.value),
      week: el => log("Week: " + el.value),
      range: el => log("Range: " + el.value),
      color: el => log("Color: " + el.value),
      checkbox: el => log("Checkbox checked: " + el.checked),
      radio: el => log("Radio selected: " + el.value),
      file: el => log("File selected: " + (el.files[0]?.name || "none"))
    };

    /*
      Attach a few top-level listeners when the DOM is ready:
        - Delegated 'input' and 'change' on the form
        - 'reset' and 'submit' on the form
        - Separate click handler for the plain button
    */
    document.addEventListener("DOMContentLoaded", () => {

      const form = document.getElementById("demoForm");

      // Delegated listeners: any input inside the form bubbles up here
      form.addEventListener("input", handleDelegatedEvent);
      form.addEventListener("change", handleDelegatedEvent);

      form.addEventListener("reset", () => log("Form reset"));

      form.addEventListener("submit", e => {
        e.preventDefault();
        log("Form submitted");
        log("Hidden value: " + document.getElementById("hiddenInput").value);
      });

      document.getElementById("buttonInput")
        .addEventListener("click", () => log("Button clicked"));
    });

    /*
      Central delegated handler:
      - Makes sure the event came from an <input>
      - Looks up a handler by input type
      - Calls that handler if it exists
    */
    function handleDelegatedEvent(e) {
      const el = e.target;

      if (el.tagName !== "INPUT") return;

      const handler = inputHandlers[el.type];

      if (handler) {
        handler(el, e); // pass element (and event if needed later)
      }
    }
  </script>
</body>

```



## Practical Summary: When Each Approach Wins (and Loses)

Inline events are a bicycle with no brakes: perfect for learning balance, a bad idea on a downhill commute. Event listeners are the standard, clean and professional. Delegation is the power tool you reach for when the number of inputs explodes or the DOM changes dynamically. Objects turn delegation into a system: fewer moving parts, clearer intent, and easier growth.

Inline shows *what events do* → listeners show *where code should live* → delegation shows *how to scale events* → objects show *how to scale logic*.

