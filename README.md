<img src="https://raw.githubusercontent.com/teodorpatras/EasyTipView/master/assets/easytipview.png" alt="EasyTipView: fully customisable tooltip view written in Swift" style="width: 500px;"/>

[![Version](https://img.shields.io/cocoapods/v/EasyTipView.svg?style=flat)](http://cocoapods.org/pods/EasyTipView)
[![Carthage Compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![License](https://img.shields.io/cocoapods/l/EasyTipView.svg?style=flat)](http://cocoapods.org/pods/EasyTipView)
[![Platform](https://img.shields.io/cocoapods/p/EasyTipView.svg?style=flat)](http://cocoapods.org/pods/EasyTipView)
[![Build Status](https://travis-ci.org/teodorpatras/EasyTipView.svg)](https://travis-ci.org/teodorpatras/EasyTipView)

Description
--------------

```EasyTipView``` is a fully customisable tooltip view written in Swift that can be used as a call to action or informative tip.

## Features

- [x] Can be shown on top of or below any ``UIBarItem`` or ``UIView`` subclass.
- [x] Automatic orientation change adjustments.
- [x] Fully customisable appearance.
- [x] Fully customisable presentation and dismissal animations.

## Preview

<img src="https://raw.githubusercontent.com/teodorpatras/EasyTipView/master/assets/easytipview.gif" width="320">

Installation
--------------

### CocoaPods

[CocoaPods](http://cocoapods.org) is a dependency manager for Cocoa projects.

CocoaPods 0.36 adds supports for Swift and embedded frameworks. You can install it with the following command:

```bash
$ gem install cocoapods
```

To integrate EasyTipView into your Xcode project using CocoaPods, specify it in your `Podfile`:

```ruby
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '8.0'
use_frameworks!

pod 'EasyTipView', '~> 0.1.3'
```

Then, run the following command:

```bash
$ pod install
```

In case Xcode complains (<i>"Cannot load underlying module for EasyTipView"</i>) go to Product and choose Clean (or simply press <kbd>⇧</kbd><kbd>⌘</kbd><kbd>K</kbd>).


### Carthage

[Carthage](https://github.com/Carthage/Carthage) is a decentralized dependency manager that builds your dependencies and provides you with binary frameworks.

You can install Carthage with [Homebrew](http://brew.sh/) using the following command:

```bash
$ brew update
$ brew install carthage
```

To integrate `EasyTipView` into your Xcode project using Carthage, specify it in your `Cartfile`:

```ogdl
github "teodorpatras/EasyTipView"
```

Run `carthage update` to build the framework and drag the built `EasyTipView.framework` into your Xcode project.

### Manually

If you prefer not to use either of the aforementioned dependency managers, you can integrate EasyTipView into your project manually.

Supported OS & SDK Versions
-----------------------------

* Supported build target - iOS 8.0 (Xcode 7.x)

Usage
--------------

1) First you should customize the preferences:
```swift

var preferences = EasyTipView.Preferences()
preferences.drawing.font = UIFont(name: "Futura-Medium", size: 13)!
preferences.drawing.foregroundColor = UIColor.whiteColor()
preferences.drawing.backgroundColor = UIColor(hue:0.46, saturation:0.99, brightness:0.6, alpha:1)
preferences.drawing.arrowPosition = EasyTipView.ArrowPosition.Top

/*
 * Optionally you can make these preferences global for all future EasyTipViews
 */
EasyTipView.globalPreferences = preferences

```

2) Secondly call the ``show(animated: forView: withinSuperview: text: preferences: delegate:)`` method:
```swift
EasyTipView.show(forView: self.buttonB,
withinSuperview: self.navigationController?.view,
text: "Tip view inside the navigation controller's view. Tap to dismiss!",
preferences: preferences,
delegate: self)
```

**Note that if you set the** ```EasyTipView.globalPreferences```**, you can ommit the** ```preferences``` **parameter in all calls. Additionally, you can also ommit the** ``withinSuperview`` **parameter and the** ``EasyTipView`` **will be shown within the main application window**.

*Alternatively, if you want to dismiss the ``EasyTipView`` programmatically later on, you can use one of the instance methods:*

```swift

let tipView = EasyTipView(text: "Some text", preferences: preferences)
tipView.show(forView: someView, withinSuperview: someSuperview)

// later on you can dismiss it
tipView.dismiss()
```

Customising the presentation or dismissal animations
--------------

The default animations for showing or dismissing are scale up and down. If you want to change the default behaviour, you need to change the attributes of the ``animating`` property within the preferences. An example could be:

```swift
preferences.animating.dismissTransform = CGAffineTransformMakeTranslation(0, -15)
preferences.animating.showInitialTransform = CGAffineTransformMakeTranslation(0, -15)
preferences.animating.showInitialAlpha = 0
preferences.animating.showDuration = 1.5
preferences.animating.dismissDuration = 1.5
```

This produces the following animations:
<br><br><img src="https://raw.githubusercontent.com/teodorpatras/EasyTipView/master/assets/animation.gif" width="200">

For more animations, checkout the example project.
*Once you configured the animations, a good idea would be to __make these preferences public__, for all future instances of `EasyTipView` by assigning it to ```EasyTipView.globalPreferences```.*

Custom types
--------------

```swift

public protocol EasyTipViewDelegate : class {
    func easyTipViewDidDismiss(tipView : EasyTipView)
}

```
Custom protocol which defines one method to be called on the delegate after the ``EasyTipView`` has been dismissed.


```swift
public struct Preferences {
    public struct Drawing
    public struct Positioning
    public struct Animating
}
```
Custom structure which encapsulates all the customizable properties of the ``EasyTipView``. These preferences have been split into three structures:
* ```Drawing``` - encapsulates customisable properties specifying how ```EastTipView``` will be drawn on screen.
* ```Positioning``` - encapsulates customisable properties specifying where ```EasyTipView``` will be drawn within its own bounds.
* ```Animating``` - encapsulates customisable properties specifying how ```EasyTipView``` will animate on and off screen.


License
--------------

```EasyTipView``` is developed by [Teodor Patraş](https://www.teodorpatras.com) and is released under the MIT license. See the ```LICENSE``` file for details.

Logo was created using Bud Icons Launch graphic by [Budi Tanrim](http://buditanrim.co) from [FlatIcon](http://www.flaticon.com/) which is licensed under [Creative Commons BY 3.0](http://creativecommons.org/licenses/by/3.0/). Made with [Logo Maker](http://logomakr.com).

Contact
--------------

You can follow or drop me a line on [my Twitter account](https://twitter.com/teodorpatras). If you find any issues on the project, you can open a ticket. Pull requests are also welcome.
