#The iOS Development Quick Reference Guide

This is a quick reference guide to iOS developers. Consider it as an extended cheatsheet or a small, more understantable documentation. The purpose of this guide is to be a **simple**, improved by everyone with the best concepts, practices and code.

This guide is **not** completed yet. Do not like something? improve it. 

For styling, we use the [NYTimes Objective-C Style Guide](https://github.com/NYTimes/objective-c-style-guide)


## Introduction

Here are some of the docs used to create this guide. 

## Table of Contents

* [Something ](#stu-ff)


#Objective-C
Objective C: a direct superset of C

* **blocks:** code that is passed as an object. When something happens, you can run that code. Categories: Extend existing classes. 
* **Protocols:** defines messaging contracts. Any class can  chose to implement int. 
You have to implement the methods specified in the protocol. 
* **Exceptions:** Programming errors. All other errors including runtime are NSErrors. 
* **Constants:** 
```objc #define PI 3.14 ```
```objc static const float PI=3.14```
* **closures:**  code in a variable
* **lazy var:** created when first used, In the getter. 
* **Singleton:** Special kind of object that exists only once in an app
* **Static Var:** exists only once in our app
* **@lazy:** Instance is created when the object is first called


##Classes 
Classes are blueprints for objects, that are its instances. 

* An app is a network of objects. 
* Classes inherit from other classes

**For example:**  

```objc
@interface ObjectiveCStuff : NSObject
    
    //ObjectiveCStuff inherits basic attributes and methods from NSObject
    
@end
```

* If ObjectiveCStuff implements a method already defined in NSObject, it overrides it.

* Calling overriden methods on ObjectiveCStuffChild 
```objc[self sayHello];```

* Calling parent methods
```objc[super sayHello];```

* Root classes defines the basic functionality. Such as NSObject.
* Keep inheritance in mind to know what an object can do.

**For Example:**

1. NSObject: Basic Framework
2. UIResponder: Responds to taps, shakes, user interactions
3. UIView: Displays on screen.
4. UIControl: Behavior of iOS controls.
5. UIButton
