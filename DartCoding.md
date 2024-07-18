---
title: Dart Coding
tags: dart flutter
aliases: 
created at: 2024-07-18
---

# Dart


##  Private Members

https://stackoverflow.com/questions/17488611/how-to-create-private-variables-in-dart

In `dart` '**`_`**' is used before the `variable name` to declare it as `private`. Unlike other programming languages, here `private` doesn't mean it is available only to the class it is in, private means it is **accessible in the library it is in** and **not accessible to other libraries**. A library can consists of multiple dart files as well using `part` and `part of`. For more information on **Dart libraries**, [check this](https://www.javatpoint.com/dart-libraries).


## Platform Dependent Code

```dart
import 'dart:io' show Platform;

if (Platform.isAndroid) {
  // Android-specific code
} else if (Platform.isIOS) {
  // iOS-specific code
}
```

or 
```dart
bool isIOS = Theme.of(context).platform == TargetPlatform.iOS;
```

e.g. persistent backend
### Platform Specific Import

```dart
import 'get_client.dart'
    if (dart.library.io) 'mobile_client.dart'
    if (dart.library.html) 'web_client.dart';
```


or: https://docs.flutter.dev/platform-integration/platform-channels


## Cascading Values

Cascades (`..`, `?..`) allow you to make a sequence of operations on the same object. In addition to accessing instance members, you can also call instance methods on that same object. This often saves you the step of creating a temporary variable and allows you to write more fluid code.

Consider the following code:

```dart
var paint = Paint()
  ..color = Colors.black
  ..strokeCap = StrokeCap.round
  ..strokeWidth = 5.0;
```

The constructor, `Paint()`, returns a `Paint` object. The code that follows the cascade notation operates on this object, ignoring any values that might be returned.


## Check Type

```dart

if (x is Foo) {}

x.runtimeType == ''
```

