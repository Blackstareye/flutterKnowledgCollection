---
title: Flutter Coding
tags: flutter coding
aliases: 
created at: 2024-07-18
---


# Flutter

##  On Build Method change State and build again Context

```dart
WidgetsBinding.instance.addPostFrameCallback((_) {
})
```

https://api.flutter.dev/flutter/scheduler/SchedulerBinding/addPostFrameCallback.html
#### of-Method 

source: https://stackoverflow.com/questions/65271259/meaning-of-the-term-of-in-flutter

In the Flutter SDK the `.of` methods are a kind of service locator function that take the framework BuildContext as an argument and return an internal API related to the named class but created by widgets higher up the widget tree. These APIs can then be used by child widgets to access state set on a parent widget and in some cases (such as Navigator) to manipulate them. The pattern encourages componentization and decouples the production of information related to the build tree with its consumption.

In addition to `Navigator.of` (returns a NavigatorState) there are:

- `Theme.of` (returns a ThemeData containing the ambient theme settings)
- `MediaQuery.of` (returns a MediaQueryData containing information computed about the device screen size)
- `Directionality.of` (returns a TextDirection containing information about text display)


## Get System Theme information

There are two ways:

1. **NO `context` required**. Can be used in `initState` for example:
    
    ```dart
    var brightness = SchedulerBinding.instance.platformDispatcher.platformBrightness;
    bool isDarkMode = brightness == Brightness.dark;
    ```
    
2. **`context` is required**:
    
    ```dart
    var brightness = MediaQuery.of(context).platformBrightness;
    bool isDarkMode = brightness == Brightness.dark;
    ```
    
    or
    
    ```dart
    var brightness = View.of(context).platformDispatcher.platformBrightness;
    bool isDarkMode = brightness == Brightness.dark;
    ```


## Future

Future are like `Promises` in Javascript.


## Clipping 

```dart

class BeamClipper extends CustomClipper<Path> {
  const BeamClipper();

  @override
  getClip(Size size) {
    return Path()
      ..lineTo(size.width / 2, size.height / 2)
      ..lineTo(size.width, size.height)
      ..lineTo(0, size.height)
      ..lineTo(size.width / 2, size.height / 2)
      ..close();
  }

  /// Return false always because we always clip the same area.
  @override
  bool shouldReclip(CustomClipper oldClipper) => false;
}
```

Result:
![](../assets/Pasted%20image%2020240711230632.png)
