# Stateless and Stateful Widgets

[TOC]



------

## **Stateless Widget**

- **Definition:** A widget that does not change once it is built.
- **Use Case:** Good for static content that depends only on its configuration (constructor parameters) and the parent widget’s context.
- **Lifecycle:** It is built once and does not rebuild unless the parent rebuilds it.
- **Examples:** `Text`, `Icon`, `Container` (when used with fixed values).

**Code Example:**

```dart
class MyStatelessWidget extends StatelessWidget {
  final String title;

  MyStatelessWidget({required this.title});

  @override
  Widget build(BuildContext context) {
    return Text(title);
  }
}
```

------

## **Stateful Widget**

- **Definition:** A widget that can change its appearance or behavior in response to events, user input, or data changes.
- **Use Case:** Good for interactive widgets that update dynamically, such as forms, animations, or buttons that change when pressed.
- **Lifecycle:** A `StatefulWidget` has two classes:
  1. The **widget class** (immutable).
  2. The **State class** (mutable, where the logic and changing data live).
      Flutter rebuilds the UI when `setState()` is called inside the `State` class.

**Code Example:**

```dart
class MyStatefulWidget extends StatefulWidget {
  @override
  _MyStatefulWidgetState createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  int counter = 0;

  void _increment() {
    setState(() {
      counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('Counter: $counter'),
        ElevatedButton(
          onPressed: _increment,
          child: Text('Increment'),
        ),
      ],
    );
  }
}
```

------

**Key Difference in One Sentence**

- A **StatelessWidget** is **immutable** (cannot change after it’s built).
- A **StatefulWidget** is **mutable** (can rebuild itself when its state changes).

------

Here’s a clear **side-by-side comparison table** of **Stateless vs Stateful Widgets** in Flutter that you can use for teaching:

------

| Feature             | **StatelessWidget**                                       | **StatefulWidget**                                           |
| ------------------- | --------------------------------------------------------- | ------------------------------------------------------------ |
| **Mutability**      | Immutable – cannot change once built                      | Mutable – can change during runtime                          |
| **Rebuild Trigger** | Rebuilt only when parent widget rebuilds                  | Can rebuild itself using `setState()`                        |
| **Lifecycle**       | Has only the `build()` method                             | Has both widget class and `State` class with lifecycle methods (`initState`, `setState`, `dispose`) |
| **Data Handling**   | Displays data that never changes (static content)         | Manages data that may change over time (dynamic content)     |
| **Use Cases**       | Static UI like `Text`, `Icon`, `Container` (fixed values) | Interactive UI like counters, forms, animations, checkboxes  |
| **Performance**     | Lightweight and efficient                                 | Slightly heavier due to state management                     |
| **Examples**        | `Text("Hello")`, `Icon(Icons.star)`                       | Counter app, toggle switches, form inputs                    |

------

**Summary:**

- Use **StatelessWidget** for **static UI**.
- Use **StatefulWidget** for **interactive/dynamic UI**.

---

## **Why a Stateful Widget needs a `State` class**

A `StatefulWidget` is split into **two parts**:

1. **The widget class**
   - Immutable.
   - Holds configuration data (like constructor parameters).
   - Exists only to tell Flutter: “Here is how my UI should be built.”
2. **The `State` class**
   - Mutable.
   - Holds the data that can change over time.
   - Provides the logic for updating the UI.
   - Calls `setState()` to tell Flutter to rebuild the widget tree.

------

### **Why not just put everything in one class?**

Flutter’s UI system is built around immutability:

- All widgets in Flutter are immutable (their fields cannot change once created).
- When something changes, Flutter doesn’t “mutate” the widget — it **rebuilds** a new widget tree.

If `StatefulWidget` itself were mutable, it would break this consistency. By separating configuration (`StatefulWidget`) from behavior (`State`), Flutter achieves:

- **Performance efficiency:** only the `State` object is preserved during rebuilds, not the whole widget.
- **Clarity:** you can see which parts are static (the widget class) and which parts are dynamic (the state).
- **Reusability:** the same widget class can be paired with different states in different contexts.

------

### **How it works in practice**

When Flutter rebuilds:

1. The old `State` object is kept.
2. The new `StatefulWidget` object is created (with new config data if needed).
3. The existing `State` is reattached to this new widget.

That’s why you must inherit from `State` — so Flutter knows:

- where to store your mutable data, and
- how to rebuild your widget when that data changes.

------

### **In short:**

 A `StatefulWidget` is immutable by design. Its mutable companion, the `State` class, exists to hold data and logic that can change. That’s why every `StatefulWidget` must be paired with a `State` subclass.