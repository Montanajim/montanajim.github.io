# Radio and Check Boxes



Radio buttons and checkboxes are two of the most common ways a web page collects “choice” input, but they behave very differently: radios enforce a single decision inside a shared group (only one option can be selected at a time), while checkboxes allow multiple independent selections (zero, one, or many). This example demonstrates both patterns in one clean page: the radio section listens for `change` events and uses `document.querySelector('input[name="grp1"]:checked')` to grab the one currently-selected radio and immediately print a message, while the checkbox section waits for a button click, uses `document.querySelectorAll('input[type="checkbox"]:checked')` to gather every checked box, and then builds a readable summary by matching each checkbox to its `<label>` via `label[for="..."]`. In other words, the DOM becomes a searchable map: `querySelector` is your “find the first match” tool for single answers (the selected radio), and `querySelectorAll` is your “collect all matches” tool for plural answers (the checked checkboxes).



```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Radio + Checkbox Demo</title>

  <style>
    .div1 {
            width: 75%;
            background-color: cornsilk;
            padding: 20px;
            margin-left: auto;
            margin-right: auto;
            margin-top: 50px;
            margin-bottom: 50px;
    }
  </style>
</head>

<body>
  <div class="div1">
    <h1>Radio Buttons</h1>

    <input type="radio" id="rad1" name="grp1" value="10" />
    <label for="rad1">Option 1</label><br />

    <input type="radio" id="rad2" name="grp1" value="20" checked />
    <label for="rad2">Option 2</label><br />

    <input type="radio" id="rad3" name="grp1" value="30" />
    <label for="rad3">Option 3</label><br />

    <br />
    <hr />
    <br />

    <h1>Check Boxes</h1>

    <input type="checkbox" id="cb1" name="cbgrp" value="11" />
    <label for="cb1">check box 1</label><br />

    <input type="checkbox" id="cb2" name="cbgrp" value="22" />
    <label for="cb2">check box 2</label><br />

    <input type="checkbox" id="cb3" name="cbgrp" value="33" />
    <label for="cb3">check box 3</label><br /><br />

    <input type="button" value="Show selected checkboxes" onclick="checkboxCheck()" />

    <br /><br />
    <hr />
    <br />

    <p id="radioMess"></p>
    <p id="checkMess"></p>
  </div>

  <script>
      
    function updateRadioMessage() {
        
      // Select the first thing that is named "grp1" that is checked
      const selected = document.querySelector('input[name="grp1"]:checked');
      const radioOut = document.getElementById("radioMess");

      if (!selected) {
        radioOut.textContent = "No radio option selected.";
        return;
      }

      let message;
      if (selected.value === "10") message = "rad1 selected (value 10)";
      else if (selected.value === "20") message = "rad2 selected (value 20)";
      else message = "rad3 selected (value 30)";

      radioOut.textContent = message;
    }

    function checkboxCheck() {
        
      // all of the selected checkboxes are collected and put into an array checkedBoxes  
      const checkedBoxes = document.querySelectorAll('input[type="checkbox"]:checked');
      console.log(checkedBoxes);

      const checkOut = document.getElementById("checkMess");

      // nothing has been checked
      if (checkedBoxes.length === 0) {
        checkOut.textContent = "No checkboxes selected.";
        return;
      }

      let message = "Checked: ";

      for (let i = 0; i < checkedBoxes.length; i++) {
        const cb = checkedBoxes[i];

        const label = document.querySelector('label[for="' + cb.id + '"]');

        let labelText;
        if (label) {
          labelText = label.textContent.trim();
        } else {
          labelText = cb.id;
        }

        if (i > 0) {
          message += ", ";
        }

        message += labelText + " (value " + cb.value + ")";
      }

      checkOut.textContent = message;
    }

    // add listeners for radio buttons
    document.querySelectorAll('input[name="grp1"]').forEach(radio => {
      radio.addEventListener("change", updateRadioMessage);
    });

    // add listeners for check boxes
    document.querySelectorAll('input[name="cbgrp"]').forEach(checkbox=>{
            checkbox.addEventListener("change",checboxCheck);
    });

    updateRadioMessage();
  </script>
</body>
</html>
```

## Document.querySelector

`document.querySelector(...)` is the browser’s “find me the first matching thing” function.

It takes a **CSS selector string** (the same kind of selector you write in a stylesheet) and searches the page (the DOM). It returns **the first element that matches**, or `null` if nothing matches.

So it’s like telling the DOM: “scan the page, stop at the first match, hand it to me.”

### What it can select

It uses **CSS selector syntax**, so it can match by:

ID:

```js
document.querySelector("#radioMess")
```

Finds the first element with `id="radioMess"`.

Class:

```js
document.querySelector(".div1")
```

Finds the first element with `class="div1"`.

Tag name:

```js
document.querySelector("input")
```

Finds the first `<input>` element.

Attribute matches:

```js
document.querySelector('input[name="grp1"]')
```

Finds the first `<input>` with `name="grp1"`.

Pseudo-classes (state-based selectors):

```js
document.querySelector('input[name="grp1"]:checked')
```

Finds the first radio in that group that is currently selected.

### Why it matters in your code

When your code does:

```js
const selected = document.querySelector('input[name="grp1"]:checked');
```

it’s not grabbing “rad1” or “rad2” directly. It’s saying: “whichever radio in group `grp1` is checked right now—give me that one.” That’s the correct mental model for radios.

When your checkbox code does:

```js
const label = document.querySelector('label[for="' + cb.id + '"]');
```

it’s saying: “find the `<label>` whose `for` attribute points to this checkbox’s id.” That’s how it pulls the human-readable text next to the checkbox.

### querySelector vs querySelectorAll

`querySelector` returns **one element** (first match).
`querySelectorAll` returns **all matches** as a NodeList.

So if you want “the selected radio” (only one), `querySelector` is perfect.
If you want “every checked checkbox” (could be many), `querySelectorAll` is the right tool.



---

## Quick Cheat Sheet

Think of each selector as a GPS address for elements in the DOM—CSS-style.

```js
// By ID (finds the element with id="radioMess")
document.querySelector("#radioMess");

// By class (finds the first element with class="div1")
document.querySelector(".div1");

// By tag name (finds the first <input> on the page)
document.querySelector("input");

// By attribute (first input whose name is grp1)
document.querySelector('input[name="grp1"]');

// By attribute + state (the currently selected radio in the grp1 radio group)
document.querySelector('input[name="grp1"]:checked');

// All radios in the group (returns a NodeList of all three radios)
document.querySelectorAll('input[name="grp1"]');

// All checked checkboxes (returns a NodeList of whichever boxes are checked)
document.querySelectorAll('input[type="checkbox"]:checked');

// A specific checkbox by its id (same idea as #cb2)
document.querySelector("#cb2");

// The label attached to checkbox cb2 (matches <label for="cb2">...</label>)
document.querySelector('label[for="cb2"]');

// The label attached to a checkbox variable cb (dynamic version)
document.querySelector('label[for="' + cb.id + '"]');
```

A few “read it like English” translations:

`#radioMess` means “the element with id radioMess.”
`.div1` means “the first element with class div1.”
`input[name="grp1"]` means “an input whose name attribute is grp1.”
`:checked` means “only the one that’s currently selected/checked.”
`label[for="cb2"]` means “a label whose for attribute is cb2.”

One practical rule: use `querySelector` when you expect one thing (like the selected radio); use `querySelectorAll` when you expect many (like checked checkboxes). If you use `querySelectorAll`, you loop it. If you use `querySelector`, you null-check it.