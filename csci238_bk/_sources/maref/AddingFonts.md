# Adding Fonts

Steps to Change Font Family in Flutter

1. Download the font

   Fonts can be downloaded at https://fonts.google.com/

2. Import the font into your project

   Create two folders assets/fonts

   Add the .tff file to the Fonts folder

   

   ![addfonttoproject](maimages/addfonttoproject.png)

   

3. Add the font to the pubspec.yaml file



```yaml
  fonts:
    - family: PermanentMarker
      fonts:
        - asset: Assets/Fonts/PermanentMarker-Regular.ttf
```



4. Use the new font in by changing it in the *style:* attribute of Text or RichText Widget



```dart
  TextStyle myQuoteStyle = const TextStyle(
    fontSize: 36,
    fontFamily: 'PermanentMarker',
  );
```



```dart
        Text("my text here", style: myQuoteStyle)
```







