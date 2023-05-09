# Run your first Dart example<br>  in Android Studio

https://o7planning.org/13965/dart-programming-with-dartpad-online-tool

####  View more Tutorials:

- [Dart Programming Tutorials](https://o7planning.org/12809/dart)



1. Article objective
2. The first Dart example with Android Studio

![img](https://s3.o7planning.com/images/idea-32.png)Follow us on our fanpages to receive notifications every time there are new articles. [![img](https://s2.o7planning.com/templates/o7planning/resources/icons/facebook-32.png) Facebook ](https://www.facebook.com/o7planning.org)[![img](https://s2.o7planning.com/templates/o7planning/resources/icons/twitter-32.png) Twitter](https://twitter.com/o7planning_org)

## 1- Article objective

In this article I'm going to show you how to create a simple **Dart** example on **Android Studio** and run it successfully. First and foremost, make sure that you have already installed the **Dart Plugin** in **Android Studio**, otherwise you can refer to the following article:

- [Install Dart Plugin for Android Studio](https://o7planning.org/12819/install-dart-plugin-for-android-studio)

Note that apart from **Android Studio**, there are a lot of **IDE**(s) in support of **Dart** programming, such as **Visual Studio Code,** **IntelliJ IDEA,** etc. Thus, the following articles may be useful for you:

- [Install Dart Code Extension for Visual Studio Code](https://o7planning.org/12827/install-dart-code-extension-for-visual-studio-code)

- [Run your first Dart example in Visual Studio Code](https://o7planning.org/12833/run-your-first-dart-example-in-visual-studio-code)

- [Dart programming with DartPad online tool](https://o7planning.org/13965/dart-programming-with-dartpad-online-tool)

## 2- The first Dart example with Android Studio

<iframe data-id="o7planning.org_880x280_responsive_2_DFP" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" topmargin="0" leftmargin="0" width="1" height="1" style="box-sizing: border-box;"></iframe>

First, create the **MyFirstDartProject** folder.

![img](https://s1.o7planning.com/en/12831/images/64403885.png)

Secondly, on **Android Studio**, open the folder you have just created.

- **File > Open**

![img](https://s1.o7planning.com/en/12831/images/64403891.png)

![img](https://s1.o7planning.com/en/12831/images/64403893.png)

Then create a new file:

- **File > New > File > MyFirstDart.dart**

![img](https://s1.o7planning.com/en/12831/images/64403899.png)

MyFirstDart.dart

```javascript
main() {

  print("Hello World!");
}
```

Next, you need to configure to tell **Android Studio** that this is a **Dart** project, so offer support to it.

- **File > Settings... > Languages / Frameworks > Dart**

After that, declare your **Dart SDK** location.

![img](https://s1.o7planning.com/en/12831/images/64403907.png)

> - [Install Dart SDK on Windows](https://o7planning.org/12813/install-dart-sdk-on-windows)

To run the **Dart** file on **Android Studio** you need to add a configuration.

![img](https://s1.o7planning.com/en/12831/images/64403947.png)

We will create a Configuration to run the **Dart** file based on an available **Template**. Select:

- **Template > Dart Command Line App > Create configuration**

![img](https://s1.o7planning.com/en/12831/images/64403955.png)

Enter the configuration name and the location of the **Dart** file.

![img](https://s1.o7planning.com/en/12831/images/64403959.png)

Now run the **Dart** file:

![img](https://s1.o7planning.com/en/12831/images/64403963.png)