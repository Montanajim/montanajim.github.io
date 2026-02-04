# **Modern DOM Selection: querySelector/querySelectorAll vs getElement(s)By…**



`document.querySelector()` / `document.querySelectorAll()` and the old-school `document.getElementsBy...` family solve the same problem—“find me elements”—but they do it with different power tools, different return types, and different gotchas. Think of it like a modern search bar versus a set of specialized filing cabinets.

## What each one is, in plain terms

`querySelector(cssSelector)` finds the **first** element that matches a **CSS selector string**.

`querySelectorAll(cssSelector)` finds **all** matching elements and returns a **static list**.

The `getElementsBy...` family are **specialized** finders:

- `getElementById(id)` → one element (or `null`)
- `getElementsByClassName(className)` → a **live HTMLCollection**
- `getElementsByTagName(tagName)` → a **live HTMLCollection**
- `getElementsByName(name)` → a **live NodeList** (mostly used for form controls)

## Selector power: CSS vs “one trick per method”

This is the big difference.

With `querySelector(All)`, you can target almost anything you can describe in CSS:

- `'#menu .item.active'`
- `'input[name="grp1"]:checked'`
- `'ul > li:first-child'`
- `'.card[data-state="open"]'`

With `getElementsBy...`, you get only the built-in categories (id, class, tag, name). If your selection needs “class + inside this container + has attribute + currently checked,” the `getElementsBy...` tools start to feel like trying to do calculus with a ruler.



## Return types: the part that bites people

### `querySelector()`

Returns a single `Element` (or `null`).

### `querySelectorAll()`

Returns a `NodeList` that is **static**: it does **not** automatically update if the DOM changes after the call.

### `getElementsByClassName()` / `getElementsByTagName()`

Return an `HTMLCollection` that is **live**: it **does** update as the DOM changes.

### `getElementsByName()`

Returns a `NodeList` that is typically **live** as well (behavior can vary by context, but you should treat it as live in practice).

Why this matters: if you add/remove elements, a live collection can “change under your feet” while you loop it, which is a subtle way to accidentally skip items or double-handle them.

## Looping and convenience

`querySelectorAll()`’s `NodeList` supports `forEach()` in modern browsers, which makes it pleasant.

`HTMLCollection` is array-like but not an array; it usually **doesn’t** have `forEach()`. You can loop it with `for...of` (modern) or a classic index loop.

If you want to use array methods reliably:

```js
const items = Array.from(document.getElementsByClassName("item"));
items.filter(/* ... */);
```

or

```js
const items = [...document.querySelectorAll(".item")];
```

## Performance: usually not your bottleneck (but here’s the real story)

- `getElementById()` is extremely direct and typically fastest in micro-benchmarks.
- `getElementsByClassName()` / `getElementsByTagName()` can be fast, but the “live” behavior has overhead and can create surprising costs if you cause lots of DOM changes.
- `querySelector(All)` does more work because it parses a CSS selector, but for typical UI sizes it’s “fast enough,” and the clarity often wins.

If you’re optimizing DOM selection in 2026, you’re probably already doing something else wrong—like querying inside a loop or forcing layout repeatedly.

## Practical “when to use what” (no fluff)

Use `querySelector()` when:

- you want a single thing and it’s easiest to describe with CSS (`:checked`, `[data-x]`, descendant selectors, etc.)
- you want readable code that matches what you’d write in CSS

Use `querySelectorAll()` when:

- you need a snapshot of many elements and you don’t want the list mutating while you work
- you want easy iteration

Use `getElementById()` when:

- you truly have an ID and it’s the clearest way to say what you mean (also great for beginners)

Use `getElementsByClassName()` / `getElementsByTagName()` when:

- you specifically want a live collection that stays up to date (rare, but sometimes useful)
- you’re maintaining older code and consistency matters

## One concrete compare example

Say you want the currently-selected radio button in a group:

With `querySelector`:

```js
const selected = document.querySelector('input[name="grp1"]:checked');
```

With `getElementsByName` you’d do more manual work:

```js
const radios = document.getElementsByName("grp1");
let selected = null;
for (const r of radios) {
  if (r.checked) { selected = r; break; }
}
```

Same result. One is a laser pointer; the other is a flashlight and patience.

## Common pitfalls

1. People expect `querySelectorAll()` to update when new elements are added. It won’t. Call it again, or use event delegation.
2. People loop a live `HTMLCollection` while removing nodes and accidentally skip elements because the collection shrinks as they go.
3. People forget that `getElementById()` is singular and `getElementsBy...` is plural for a reason (and returns collections even if there’s only one match).

