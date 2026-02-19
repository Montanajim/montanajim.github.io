# Document Object Model

In a web page, the DOM—short for **Document Object Model**—is the browser’s *living* map of your HTML. Your HTML file is the blueprint you hand to the browser; the DOM is what the browser builds from it and keeps in memory so it can be inspected, updated, and interacted with while the page is running. If HTML is a script, the DOM is the stage set everyone actually walks around on.

The DOM is organized like a **tree**, because elements in HTML are nested inside other elements. At the top sits the `document` object, which represents the entire page. Under that is the `<html>` element, then `<head>` and `<body>`, and then everything visible on the page tends to live under `<body>`. Each item in this structure is called a **node**. Most nodes are **element nodes** (tags like `<div>` or `<p>`), but the characters inside an element are represented too (as **text nodes**), and details like attributes (`id`, `class`, `href`) are stored as part of the node’s information.

Here’s the basic shape, like a family tree for your page:

```
document
└── html
    ├── head
    │   ├── title
    │   └── meta / link / script ...
    └── body
        ├── h1
        │   └── "Welcome"
        ├── p
        │   └── "This is a page."
        └── div#main.container
            ├── button
            │   └── "Click me"
            └── img (src="photo.jpg")
```

Why this matters is the part that unlocks modern web pages: **JavaScript doesn’t “edit the HTML file.”** It works with the DOM. When you tell JavaScript to change the text of a heading, or hide a section, or add a new item to a list, what you’re really doing is changing the DOM node (or nodes). After the DOM changes, the browser updates what you see so the screen matches the current DOM. That’s the core loop of interactivity: something happens, code runs, the DOM updates, the display follows.

You interact with the DOM through the `document` object. Conceptually, you do three things over and over: you **select** a node, you **read or change** its data (text, attributes, classes, styles), and you **listen for events** on it. Events are the DOM’s way of announcing: “A click happened,” “a key was pressed,” “a form field changed,” “the mouse moved.” When you attach an event listener, you’re basically giving the page instructions on how to respond when something happens—like wiring a doorbell to a chime.

Here’s a simple “what happens when you click” illustration:

```
User clicks button
      ↓
Browser creates a "click" event
      ↓
Event travels to the button's DOM node
      ↓
Your event listener runs (JavaScript)
      ↓
Your code updates the DOM (maybe changes text)
      ↓
Browser re-renders the page to match the new DOM
```

One last detail that saves people a lot of confusion: the DOM is **live**, and it can drift away from the original HTML source file. If JavaScript adds a new `<li>` to a list, the page you’re looking at now contains that list item in the DOM—even if the original HTML file never had it. The DOM is the *current state of the page*; the HTML file is the *starting point*.

If you want one sentence to tattoo on your brain (temporary ink is fine): **The DOM is the browser’s object-based tree representation of a web page, and JavaScript makes pages interactive by reading from and writing to that tree.**