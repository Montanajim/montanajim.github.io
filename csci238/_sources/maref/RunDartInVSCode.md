# Run Dart In VS Code



Certainly. **Guide:**

------

## Running Dart from VS Code (with or without Flutter)

### 1. Install Dart SDK (if no Flutter)

- Download from [dart.dev](https://dart.dev/get-dart).
- Add the `bin` folder of the SDK to your system PATH so your terminal knows what `dart` means.

### 2. Use Dart bundled with Flutter (if Flutter is installed)

- Flutter includes its own Dart SDK inside:

  ```
  <flutter_installation_directory>\bin\cache\dart-sdk
  ```

- The easy route: add this to your PATH instead:

  ```
  <flutter_installation_directory>\bin
  ```

  That way, both Flutter and Dart commands just work.

- Verify with:

  ```
  dart --version
  ```

### 3. Set up VS Code

1. Open VS Code.
2. Install the **Dart** extension from the marketplace (search “Dart” by Dart Code).
   - If you’ll be doing Flutter, install **Flutter** extension too.
3. Open a folder where your project will live.

### 4. Create a Dart project or file

- Run in terminal:

  ```
  dart create my_project
  ```

- Or just make a file called `main.dart` with something trivial:

  ```dart
  void main() {
    print('Dart is alive inside VS Code.');
  }
  ```

### 5. Run Dart code

- From the integrated terminal:

  ```
  dart run main.dart
  ```

- Or use the Run ▶ button in VS Code’s editor if the extension is installed.

------

Recommendation: If you already have Flutter, don’t install Dart separately—just use Flutter’s bundled SDK.
 Next step: Add `<flutter>\bin` to PATH, install the Dart extension in VS Code, and test with a simple `main.dart`.



###### 8/25

