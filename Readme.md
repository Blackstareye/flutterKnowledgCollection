---
title: Flutter
tags: app development android dart flutter
aliases: 
created at: 2024-06-17
---

# Flutter

Refactoring Key: <kbd>alt</kbd>+<kbd>shift</kbd>+<kbd>t</kbd> - for "Transform"

Framework that is  based on Dart
 
 #Dart Cheatsheet: https://dart.dev/resources/dart-cheatsheet#optional-positional-parameters


- <https://www.freecodecamp.org/news/how-to-build-mobile-apps-with-flutter/>

- Video: <https://www.youtube.com/watch?v=1xipg02Wu8s>
- Learn Doku: https://flutter.dev/learn
- Simple Project: https://www.youtube.com/watch?v=D4nhaszNW4o

## Documentation

* Api: https://api.flutter.dev
* Animation Samples: https://github.com/flutter/samples/tree/main/animations#animation-samples
* Doc: https://docs.flutter.dev/
* Layout Introduction: https://docs.flutter.dev/ui/layout
* Layouts: https://docs.flutter.dev/ui/widgets/layout
* Widgets: https://docs.flutter.dev/ui/widgets
* Material Widgets: https://m3.material.io/components
* Unit Testing: https://docs.flutter.dev/cookbook/testing/unit/introduction
* Mocking Framework: https://docs.flutter.dev/cookbook/testing/unit/mocking
* Testing App to show all way of testing: https://github.com/flutter/samples/tree/main/testing_app
* Statemanagement in Flutter: https://www.youtube.com/watch?v=d_m5csmrf7I
* Performance Testing: https://medium.com/flutter/performance-testing-of-flutter-apps-df7669bb7df7

{}

## Codelabs

* https://docs.flutter.dev/codelabs

## Testing

{}

## Debugging

### Debugging Flag

```dart
if(kDebugMode) {

}

if(kReleaseMode) {

}

```
### Debug on Android device

```sh
flutter -v -d your_android_device run
```
(should be detected if adb is enabled)

```sh
// check devices
flutter devices
```


## Relevant Topics

### Adding Fonts and Assets

add them to `pubspec.yaml` and access them via path

### Notification Tutorial

{}
### Little Project
{}

### Monetization 

https://flutter.dev/monetization

### Build and Release - Android

https://flutter-ko.dev/deployment/android

### Pixel in Flutter


>[!note]
>  Flutter works with logical pixels as a unit of length. They are also sometimes called **device-independent pixels**. A padding of 8 pixels is visually the same regardless of whether the app is running on an old low-res phone or a newer ‘retina' device. There are roughly 38 logical pixels per centimeter, or about 96 logical pixels per inch, of the physical display.


## Hello world

```dart nums {34,35,37-41}
import 'package:english_words/english_words.dart';
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => MyAppState(),
      child: MaterialApp(
        title: 'Namer App',
        theme: ThemeData(
          useMaterial3: true,
          colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepOrange),
        ),
        home: MyHomePage(),
      ),
    );
  }
}

class MyAppState extends ChangeNotifier {
  var current = WordPair.random(); // -> subscriped to this
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var appState = context.watch<MyAppState>(); // this is an observer pattern

    return Scaffold(
      body: Column(
        children: [
          Text('Here is a thought:'),
          Text(appState.current.asLowerCase),
          ElevatedButton(
            onPressed: () {
              print('button pressed!');
            },
            child: Text('Next'),
          ),

        ],
      ),
    );
  }
}

```

1. Every widget defines a `build()` method that's automatically called every time the widget's circumstances change so that the widget is always up to date.
2. `MyHomePage` tracks changes to the app's current state using the `watch` method.
3. Every `build` method must return a widget or (more typically) a nested _tree_ of widgets. In this case, the top-level widget is `Scaffold`. You aren't going to work with `Scaffold` in this codelab, but it's a helpful widget and is found in the vast majority of real-world Flutter apps.
4. `Column` is one of the most basic layout widgets in Flutter. It takes any number of children and puts them in a column from top to bottom. By default, the column visually places its children at the top. You'll soon change this so that the column is centered.
5. You changed this `Text` widget in the first step.
6. This second `Text` widget takes `appState`, and accesses the only member of that class, `current` (which is a `WordPair`). `WordPair` provides several helpful getters, such as `asPascalCase` or `asSnakeCase`. Here, we use `asLowerCase` but you can change this now if you prefer one of the alternatives.
7. Notice how Flutter code makes heavy use of trailing commas. This particular comma doesn't need to be here, because `children` is the last (and also _only_) member of this particular `Column` parameter list. Yet it is generally a good idea to use trailing commas: they make adding more members trivial, and they also serve as a hint for Dart's auto-formatter to put a newline there. For more information, see [Code formatting](https://docs.flutter.dev/development/tools/formatting).

## Services and Patterns

[ServicesandPatterns](ServicesandPatterns.md)
## Widgets

[FlutterWidgets](FlutterWidgets.md)

## Programming Tricks and Knowledge
### Flutter

[FlutterCoding](FlutterCoding.md)
### Dart
[DartCoding](DartCoding.md)
### Animations

[FlutterAnimations](FlutterAnimations.md)