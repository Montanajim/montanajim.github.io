# Displaying Text

The differences and use cases for `JTextArea`, `JTextPane`, and `JEditorPane` in Java Swing:

## **JTextArea**:

- **Description**: A `JTextArea` is a versatile component that displays **multiple lines of text** and optionally allows the user to edit the content.
- Pros:
  - Simple and lightweight.
  - Suitable for displaying and editing plain text.
  - Supports line wrapping.
  - Can be placed inside a `JScrollPane` for scrolling behavior.
- Cons:
  - Limited formatting capabilities (no styles or images).
  - Not suitable for rich text or complex layouts.

## **JTextPane**:

- **Description**: A `JTextPane` extends `JEditorPane` and provides an editable text component with **rich text formatting capabilities**.
- Pros:
  - Supports styled text (fonts, colors, styles).
  - Allows embedding images and components directly.
  - Suitable for implementing text editors, document viewers, etc.
- Cons:
  - More complex than `JTextArea`.
  - Requires understanding of styled documents and attributes.
  - Limited HTML support compared to `JEditorPane`.

## **JEditorPane**:

- **Description**: A `JEditorPane` supports display/editing of **HTML and RTF content**. It can be extended by creating custom `EditorKit` implementations.
- Pros:
  - Supports HTML and RTF.
  - Can display web content.
  - Customizable with different `EditorKit` implementations.
- Cons:
  - Limited CSS support.
  - Not as feature-rich as a full web browser.
  - Requires handling different content types.

In summary:

- Use `JTextArea` for simple, unstyled text.
- Use `JTextPane` for styled text (fonts, colors) and embedding images.
- Use `JEditorPane` for HTML/RTF content and custom text formats.