# JFrame



- In Java's Swing framework, a `JFrame` is one of the fundamental building blocks for creating graphical user interfaces (GUIs). A `JFrame` acts as a top-level window with a title bar, border, and buttons for minimizing, maximizing, and closing the window. Developers use `JFrame` to host other GUI components like buttons, panels, and text fields. Creating a `JFrame` involves configuring its properties—such as size, title, and layout—and responding to user actions or system events—such as closing the window or resizing it. Together, properties and event handling allow `JFrame` to serve as a flexible and interactive window for desktop applications.

  ------

  **Common `JFrame` Properties**:

  - **`title`** (`setTitle(String title)`): Sets the text displayed in the window's title bar.
  - **`size`** (`setSize(int width, int height)`): Sets the dimensions of the window.
  - **`location`** (`setLocation(int x, int y)`): Specifies the window’s position on the screen.
  - **`resizable`** (`setResizable(boolean resizable)`): Enables or disables the user's ability to resize the window.
  - **`visible`** (`setVisible(boolean visible)`): Controls whether the frame is shown on the screen.
  - **`defaultCloseOperation`** (`setDefaultCloseOperation(int operation)`): Determines the behavior when the user initiates a "close" on the frame (e.g., exit the application, hide the window).
  - **`iconImage`** (`setIconImage(Image image)`): Sets the image displayed in the title bar (optional).
  - **`layout`** (`setLayout(LayoutManager manager)`): Sets the layout manager that controls component arrangement.
  - **`contentPane`** (`setContentPane(Container contentPane)`): Sets the primary container for adding components.
  - **`background`** (`setBackground(Color color)`): Sets the background color of the frame.

  **Key `JFrame` Events**:

  - **`WindowListener`**: An interface for receiving window events.
    - `windowOpened(WindowEvent e)`: Invoked when the window is first opened.
    - `windowClosing(WindowEvent e)`: Invoked when the user attempts to close the window.
    - `windowClosed(WindowEvent e)`: Invoked after the window has been closed.
    - `windowIconified(WindowEvent e)`: Invoked when the window is minimized.
    - `windowDeiconified(WindowEvent e)`: Invoked when the window is restored from minimized state.
    - `windowActivated(WindowEvent e)`: Invoked when the window gains focus.
    - `windowDeactivated(WindowEvent e)`: Invoked when the window loses focus.
  - **`ComponentListener`**: For detecting resize, move, show, or hide actions.
    - `componentResized(ComponentEvent e)`: Invoked when the frame is resized.
    - `componentMoved(ComponentEvent e)`: Invoked when the frame is moved.
    - `componentShown(ComponentEvent e)`: Invoked when the frame is shown.
    - `componentHidden(ComponentEvent e)`: Invoked when the frame is hidden.