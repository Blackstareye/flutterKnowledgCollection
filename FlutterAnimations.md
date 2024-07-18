---
title: Animations
tags: flutter animation
aliases: 
created at: 2024-07-18
---

# Animations

 there are 

  * build in animation widgets (implicit classes)
	  * e.g. `AnimatedContainer`
  * Animated Crossfade
	  * build animation between child a and b
  * Hero Animation
	  * zoom in to smooth the transition from one page to another using unique `tags`
  * TweenAnimationBuilder
  * Explicit Animations (need a controller)
	  * Transitions
		  * Fadetransition
		  * Sizetransition 
	  * uses only curve and Controller
	  * General Animation
		  * uses Animation Controller for Flow Control and syncing
		  * uses Animations e.g. Tweens for inbetween value interpolation
		  * uses notifications for state change and general value listener
		  * can also use
			  * Animation Widget for Code Modularization
			  * or Animation Builder if the Animation is part of the tree

Use `..repeat()` on animation controller for loop

Tween.evaluate --> if there is not an animation object but the value is needed (used also for synced animations)
Tween.animate(controller) -> get an animation object which spits out the value

Use Inplicit Animations for simple inbetween state 1 to state 2 things.
Use Transitions before you think you need explicit animation with builder.


## Tween Animation

```dart
  Widget build(BuildContext context) {
    return TweenAnimationBuilder(
      duration: const Duration(milliseconds: 500),
      tween: Tween<double>(begin: 0, end: 1),
      builder: (context, value, child) {
        return Opacity(
          opacity: value,
          child: Padding(
            padding: EdgeInsets.only(top: value* 20),
            child: child
          ),
        );
      },
      child: Text(
        text,
        style: TextStyle(fontSize: 36, color: Colors.white, fontWeight: FontWeight.bold),
      ),
    );
  }
```

## Animation Widget  and Animation Builder
The `AnimatedWidget` base class allows you to separate out the core widget code from the animation code. `AnimatedWidget` doesn't need to maintain a `State` object to hold the animation.

```dart
class AnimatedLogo extends AnimatedWidget {
  const AnimatedLogo({super.key, required Animation<double> animation})
      : super(listenable: animation);

  @override
  Widget build(BuildContext context) {
    final animation = listenable as Animation<double>;
    return Center(
      child: Container(
        margin: const EdgeInsets.symmetric(vertical: 10),
        height: animation.value,
        width: animation.value,
        child: const FlutterLogo(),
      ),
    );
  }
}
```

Use `AnimatedBuilder` to describe an animation as part of a build method for another widget. If you simply want to define a widget with a reusable animation, use an `AnimatedWidget`, as shown in the [Simplifying with AnimatedWidget](https://docs.flutter.dev/ui/animations/tutorial#simplifying-with-animatedwidget) section.

Like `AnimatedWidget`, `AnimatedBuilder` automatically listens to notifications from the `Animation` object, and marks the widget tree dirty as necessary, so you don't need to call `addListener()`.

With `AnimationBuilder`


Child paramater: give it down when it doesnt need to be build / animated again.
Else make a const  parameter (build at compilertime).

Use more AnimationWidget , its the modularized way of AnimationBuilder
```dart
import 'package:flutter/material.dart';

void main() => runApp(const LogoApp());

// #docregion logo-widget
class LogoWidget extends StatelessWidget {
  const LogoWidget({super.key});

  // Leave out the height and width so it fills the animating parent.
  @override
  Widget build(BuildContext context) {
    return Container(
      margin: const EdgeInsets.symmetric(vertical: 10),
      child: const FlutterLogo(),
    );
  }
}
// #enddocregion logo-widget

// #docregion grow-transition
class GrowTransition extends StatelessWidget {
  const GrowTransition(
      {required this.child, required this.animation, super.key});

  final Widget child;
  final Animation<double> animation;

  @override
  Widget build(BuildContext context) {
    return Center(
      child: AnimatedBuilder(
        animation: animation,
        builder: (context, child) {
          return SizedBox(
            height: animation.value,
            width: animation.value,
            child: child,
          );
        },
        child: child,
      ),
    );
  }
}
// #enddocregion grow-transition

class LogoApp extends StatefulWidget {
  const LogoApp({super.key});

  @override
  State<LogoApp> createState() => _LogoAppState();
}

// #docregion print-state
class _LogoAppState extends State<LogoApp> with SingleTickerProviderStateMixin {
  late Animation<double> animation;
  late AnimationController controller;

  @override
  void initState() {
    super.initState();
    controller =
        AnimationController(duration: const Duration(seconds: 2), vsync: this);
    animation = Tween<double>(begin: 0, end: 300).animate(controller);
    controller.forward();
  }
  // #enddocregion print-state

  @override
  Widget build(BuildContext context) {
    return GrowTransition(
      animation: animation,
      child: const LogoWidget(),
    );
  }

  @override
  void dispose() {
    controller.dispose();
    super.dispose();
  }
  // #docregion print-state
}
// #enddocregion print-state
```


More easier with https://pub.dev/packages/flutter_animate

##  2D Sprite animations

use flame https://medium.com/flutter-community/sprite-sheet-animations-in-flutter-1b693630bfb3






