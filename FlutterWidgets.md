---
title: Widgets
tags: flutter widgets
aliases: 
created at: 2024-07-18
---


# Flutter Widgets
##  FutureBuilder

add Async Methods to building steps (not invocation of actions)
https://api.flutter.dev/flutter/widgets/FutureBuilder-class.html


## ListviewBuilder

Determines `how` the list should be build.
* separated , has a separtion in between which can be also used with a `builder`

## Intrinsic Height

Adds more reasonable Height to a widget if the height goes to infinity

## Form Fields

Tutorial: https://www.youtube.com/watch?v=2QxzqkLzAG8&list=PL4cUxeGkcC9ighyCUUmoaxz9CZsUz4Iwf

Text Editing Controller:
 * Controller for on change stuff - has the text and can be accessed
You can use normal input fields if you don't need validation and save

Icons: https://fonts.google.com/icons
##  Stateful  vs Stateless Widgets

Widgets that are stateful can have variables.
They have a `setState()` method, which notifies all that there are changes.

set state also rebuilds the layout if there are changes (like in [nestedScaffoldExample](https://api.flutter.dev/flutter/material/Scaffold-class.html#troubleshooting)).


Example Class:

>[!info]
>The underscore (`_`) at the start of `_MyHomePageState` makes that class private and is enforced by the compiler. If you want to know more about privacy in Dart, and other topics, read the [Language Tour](https://dart.dev/language/libraries).



```dart nums {31-34, 6, 11}

//....

class MyHomePage extends StatefulWidget {
  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {

  var selectedIndex = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Row(
        children: [
          SafeArea(
            child: NavigationRail(
              extended: false, // if true, then label is seen
              destinations: [
                NavigationRailDestination(
                  icon: Icon(Icons.home),
                  label: Text('Home'),
                ),
                NavigationRailDestination(
                  icon: Icon(Icons.favorite),
                  label: Text('Favorites'),
                ),
              ],
              selectedIndex: selectedIndex,
              onDestinationSelected: (value) {
                setState(() {
                  selectedIndex = value;
                });
              },
            ),
          ),
          Expanded(
            child: Container(
              color: Theme.of(context).colorScheme.primaryContainer,
              child: GeneratorPage(),
            ),
          ),
        ],
      ),
    );
  }
}
```


setState() rebuilds and notifies all that a state change happened.
## Layout Builder 

`LayoutBuilder` lets you change your widget tree depending on how much available space you have.

## Safe Area

The `SafeArea` ensures that its child is not obscured by a hardware notch or a status bar. In this app, the widget wraps around `NavigationRail` to prevent the navigation buttons from being obscured by a mobile status bar, for example.

## Extended 

Expanded widgets are extremely useful in rows and columns—they let you express layouts where some children take only as much space as they need (`SafeArea`, in this case) and other widgets should take as much of the remaining room as possible (`Expanded`, in this case). One way to think about `Expanded` widgets is that they are "greedy". If you want to get a better feel of the role of this widget, try wrapping the `SafeArea` widget with another `Expanded`. The resulting layout looks something like this:

## Placeholder

`Placeholder`; a handy widget that draws a crossed rectangle wherever you place it, marking that part of the UI as unfinished.
## Scaffold

![](assets/Pasted%20image%2020240711142926.png)

The basic structure of an widget, with title, body , bottom and snackbar (optional)
Only **one** should be in the application [source](https://stackoverflow.com/questions/64618050/is-it-correct-to-have-nested-scaffold-in-flutter)
## Container

[`Container`](https://api.flutter.dev/flutter/widgets/Container-class.html) is a widget class that allows you to customize its child widget. Use a `Container` when you want to add padding, margins, borders, or background color, to name some of its capabilities.

## Expandable Floating Action Button (FAB)

https://docs.flutter.dev/cookbook/effects/expandable-fab

## Gesture Detector

Use for touch button stuff