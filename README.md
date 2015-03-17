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


**Interface:** Declares how an object can be used.

**.h file** (header) is the public API of a class (interface). viewable methods and properties of the class

**.m file** (implementation)

\*Classnames should have a 3 letter prefix to avoid duplicates.

**For Example:**

```objc
XYZPerson.h
@interface XYZPerson:NSObject
@property NSString *name;
@end

XYZPerson.m
#import “XYZPerson.h”
@interface XYZPerson()
	//here go private file declarations. 
@end
@implementation  XYZPerson
-(void) sayHello{}
@end
```

##Categories: 
Categories extend the functionality of a class to it and its subclasses.

**For Example:**  Declaring an interface for the original object, with the new name in parentheses

```objc
@interface ObjectiveCStuff (ObjectiveCStuff_ExtensionThroughCategory)
- (NSString *)extraMethod; //this method will now be available to all ObjectiveCStuff  and ObjectiveCStuff child instances.
@end
```
```objc
@implementation ObjectiveCStuff(ObjectiveCStuff_ExtensionThroughCategory)
- (NSString *)extraMethod { return @”hi”;}
@end
```

##Properties: 
Hold an object’s values and control access. 

* Property attributes indicate whether it is readonly.
* All properties start with a value of 0 (or nil in pointers)
* Initializing them in the header is called lazy instantiation.
* In swift, properties must be initialized at the creation of object. 

* Properties declared in the header file are public
                 declared in the implantation are private.
                 
**Standard declaration**  By default, properties  are strong and atomic.
`@property NSString *firstName;`

**Weak reference** Variables you only need as long as someone is also pointing to it. 

* Means a relation in which the object does not own. 
* The object is deleted if there are no other strong references to it.
```objc @property (weak) id delegate; ```

**Strong reference** Keep the object until all strong pointers are disconnected. 
* They own the object and it won't be deleted until the owner is deleted.

**Copy**: Hold on to the value of the object at the point in time when I am assigning it to my property.

* Otherwise, a mutable string could be assigned to an immutable string property, because mutablestring is a child class

```objc @property (copy)NSString *Name2; ```

**Retain** Hold on to the object 
* We don't care what its internal values currently are or will be in the future.

**Nonatomic** Not thread safe. 
* Property attribute specifies synthesized accessors simply to set or return a value directly.
* No guarantees about what happens if that same value is accessed simultaneously from different threads.
* It’s faster to access a nonatomic property than an atomic one

```objc @property(nonatomic) NSString *Name; ```
\*Multithreading should not be many threads to an object. It should be model in one, view in other thread and controller in other, talking to each other.

**Synthesize**

```objc @synthesize firstName = ivar_firstName; ``` Makes the \_firstname backing var of the firstName property to be called ivar_firstName.

```objc @synthesize firstName = _firstName; ``` *used only when you declare the properties getters AND setters explicitly, for the firstName property. 

**For Example:** Property, defining own getters and setters.

```objc
@property NSString *name; //on interface
@synthesize name = _name;  //on header, lets the compiler know the varname
```

**Setter method** 

```objc
- (void) setName:(NSString *)n {
_name = [n uppercaseString];
}
```

**Getter method**

```objc
- (NSString*) name {
return _name;
}
```


**Readonly** Doesn’t have a setter.

```objc @property (readonly) NSDate *dateOfBirth; ```

* A property can be declared as readonly in the header and in the implementation, so it has an internal setter.

**Specifying getter name** usually done in booleans.

```objc
@property(nonatomic, getter=isTaken) BOOL *taken;
```

##Variables
**Values and collections** are Cocoa objects
Objective C supports C primitive types

**Int** should be used in loops
```objc int someInteger=0; ```

**NSString** Class used for strings of characters

```objc
NSString *someString = @"Hello, World!";
NSNumber *myBOOL = @YES;
NSNumber *myFloat = @3.14f;
NSNumber *myInt = @42;
NSNumber *myInt2 = @(84 / 2);
```

**NSNumber** is an object, it is slow.  It can wrap different types of numbers

**NSInteger** use this one always. its a platform adaptive type of scalar, especially when passing between functions

**NSUInteger** NSInteger that is only positive.

**Collections**

```objc
NSArray
	   @[@"♠︎",@"♣︎",@"♥︎",@"♦︎"];
```

**NSSet**

**NSDictionary** immutable collection of objects looked by key (hash table) that holds objects strongly

```objc
@{key:value, key2:value}
NSDictionary *colors =@{ @“green”:[UIColor greenColor]}
```

***Methods***
```objc
something=colors[@“green”]
(id)objectForKey:(id)key
```
* key is an object and must implement has: and isEqual: NSStrings are good because they hash based on their chars
//dont rely on NSObject's has and isEqual methods

**looping**

```objc
for id key in dictionary{
dictioanary[key].doSomething
 }
```

**PropertyList** Collection of collections

* ”Property list” it is a phrase not an object. 
* Holds NSArray NSDict, NSNum, NSStr, NSDate, NSdata
* NSarray is PL if its members are PLS => like array of strings.
* NSDict if both keys+values are PLS.
* SDK has methods that operate on propertylist 
  * Example: writeToFile can be sent to an array or dict that contains property list objects.

* A **local variable** is allocated on the **stack**
* **Objects** are allocated on the heap.
* An object often needs to stay alive longer than the original variable that was created to keep track of it, so an object’s memory is allocated and deallocated dynamically.
* Variables declared at the top of the file are instance vars, like properties, without accessors.

**Initializing**  

```objc
NSObject *newObject = [[NSObject alloc] init];
```

*alloc saves memory for the object and sets memory spaces to zero
*init makes sure all values are initialized properly.

**Factory method** shorter way, used when no args are needed. 

```objc  
NSObject *newObject2 = [NSObject new];     
```
   
**Initialize with value**
```objc
NSNumber *magicNumber = [[NSNumber alloc] initWithInt:42];  //NSNumber is Immutable
NSNumber *magicNumber2 = [NSNumber numberWithInt:42]; //factory method. Same but in less code.
```
**IMPORTANT**
* On objective C, values are not changed.
```objc
NSString *c = @"a";
NSString *b =c;  // objects are copied, they don't point to the same object
c=@"B";  // a NEW string is assigned to b. The last value is not modified, it is discarded.
NSMutableString *e = @"a"; //Not discarded if object is mutable
e=@"d"; //original is modified.
```

                 
               