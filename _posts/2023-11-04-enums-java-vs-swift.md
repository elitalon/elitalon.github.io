---
title: "Enums: Java vs Swift"
description: A comparison of the capabilities of enumerations in Java and Swift.
---
I had always thought that Java [enumerations](https://en.wikipedia.org/wiki/Enumerated_type) were a rather simple data type, as they are designed in C for example. But I discovered recently, as part of doing some backend work, that they're actually much more versatile.

<!--more-->

Enumerations in Java are implemented through the [Enum base class](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/lang/Enum.html), from which all enumerations inherit. They come with a special syntax (e.g. using the `enum` keyword instead of `class` to declare them) and a somewhat restricted behaviour. But precisely because they _are_ a class, they also offer most of their functionality.

I thought it would be an interesting exercise to compare their capabilities with [enumerations in Swift](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations) because Swift is currently the language I use the most and its enumeration type is also powerful.

Throughout this post I will be using the [SE 18 Edition](https://docs.oracle.com/javase/specs/jls/se18/html/index.html) of the Java Language Specification (JLS) and [version 5.9](https://github.com/apple/swift-book/tree/swift-5.9-fcs) of the [Swift Programming Language](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/aboutthelanguagereference/). And it wouldn't be fair if I didn't thank [Joshua Bloch](https://twitter.com/joshbloch) for his invaluable explanations in [Effective Java](https://www.pearson.com/en-us/subject-catalog/p/effective-java/P200000000138/9780134685991).

## Creating enumerations
The purpose of enumerations is to create a group of related values that we can access from the rest of a program using a name.

One important feature to remember is that in Java these values are constant. Once they're defined, they don't change nor can be destroyed. You can think of them as [singleton](https://en.wikipedia.org/wiki/Singleton_pattern) instances of a class.

This is also true in Swift for the most part. But as we will see later, enumerations can also hold additional values that are set at call site.

### Enumerations as plain constants
The simplest way of creating enumerations is by defining constants. The two snippets below define `Season` with four constant values (a.k.a. cases) that we can access by their name.

```java
// Java
enum Season {
    SPRING,
    SUMMER,
    AUTUMN,
    WINTER;
}

var summer = Season.SUMMER;
```

```swift
// Swift
enum Season {
    case spring
    case summer
    case autum
    case winter
}

let summer = Season.summer
```

This trivial example is enough to discover how much functionality they provide out of the box.

In the case of Java, `Season` is effectively a subclass of [Enum](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/lang/Enum.html). This means we have methods like `name()`, `ordinal()` or `valueOf()` at our disposal and, by extension, we also get all the functionality of [Object](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/lang/Object.html).

In comparison it may seem like enumerations in Swift are more limited because they don't inherit from any parent class nor implement any interface. But in the absence of a superclass like Java's [Object](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/lang/Object.html), a Swift `enum` comes with an equivalent built-in implementation of interfaces like [CustomStringConvertible](https://developer.apple.com/documentation/swift/customstringconvertible), [Hashable](https://developer.apple.com/documentation/swift/hashable) or [Codable](https://developer.apple.com/documentation/swift/codable).

### Storing additional values
A more advanced way of creating enumerations is by storing additional values alongside each constant.

The snippet below demonstrates a first approach in Java. In this case we define `Size` with three constants, each one storing an additional `String` value:

```java
// Java
enum Size {
    SMALL("S"),
    MEDIUM("M"),
    LARGE("L");

    private final String label;

    Size(String label) {
        this.label = label;
    }
}

var smallSize = Size.SMALL;
```

This works by declaring an instance field (`label`) and writing a constructor that stores the value in it. We can actually declare as many fields as we need and of any type, although each constant must share the same declaration (remember that constants are "instances" of the same `Enum` subclass):

```java
// Java
enum Size {
    SMALL("S", 1, false),
    MEDIUM("M", 3, false),
    LARGE("L", 5, true);

    private final String label;

    private final double weight;

    private final boolean requiresCheck;

    Size(String label, double weight, boolean requiresCheck) {
        this.label = label;
        this.weight = weight;
        this.requiresCheck = requiresCheck;
    }
}

var smallSize = Size.SMALL;
```

While these fields could be changed later if we also wrote custom setters, the convention in the Java community seems to have them declared as `final` and thus also constant.

The same approach is more limited in Swift. We can only define exactly one value per constant, known as the [raw value](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations/#Raw-Values), and restricted to types adopting the [RawRepresentable](https://developer.apple.com/documentation/swift/rawrepresentable) interface. Moreover, they remain constant once they're set:


```swift
// Swift
enum Size: String {
    case small = "S"
    case medium = "M"
    case large = "L"
}

let smallSize = Size.small
```

To compensate for that Swift offers a second approach where we can declare a variable number of [associated values](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations/#Associated-Values) of any type:

```swift
// Swift
enum ReadState {
    case pending
    case inProgress(page: Int)
    case finished(rating: Double)
}

let statesByBookTitle: [String: ReadState] = [
    "The Lord of The Rings": .finished(rating: 4.5),
    "Drums of Autumn": .finished(rating: 3),
    "The Pillars of The Earth": .inProgress(page: 682),
    "Effective Java": .inProgress(page: 12),
    "Design for Real Life": .pending
]
```

The example above shows an important difference with Java: associated values are attached to enumeration _cases_, not to the enumeration itself. There's no need to declare instance properties and different values can be attached to the same case every time they're used[^1].

A similar effect, although not as powerful, can be achieved in Java by implementing additional constructors that set default values to one or more fields:

```java
// Java
enum VideoFormat {
    MATROSKA("mkv"),
    QUICKTIME("mov", List.of("qt"));

    private final String mainExtension;

    private final List<String> altExtensions;

    VideoFormat(String mainExtension) {
        this(mainExtension, List.of());
    }

    VideoFormat(String mainExtension, List<String> altExtensions) {
        this.mainExtension = mainExtension;
        this.altExtensions = altExtensions;
    }
}
```

## Switching over values
A typical application of enumerations is to use them in [switch statements](https://en.wikipedia.org/wiki/Switch_statement). They work similarly in both languages, syntactical differences aside:

```java
// Java
boolean isWarm(Season season) {
    return switch (season) {
        case SPRING -> true;
        case SUMMER -> true;
        case AUTUMN -> false;
        case WINTER -> false;
    };
}
```

```swift
// Swift
func isWarm(season: Season) -> Bool {
    switch season {
    case .spring:
        true
    case .summer:
        true
    case .autum:
        false
    case .winter:
        false
    }
}
```

Swift allows [more advanced comparisons](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Switch), but that's more a feature of `switch` rather than enumerations. The only aspect where Swift differs slightly from Java is when handling associated values:

```swift
// Swift
struct Book {

    enum ReadState {
        case pending
        case inProgress(page: Int)
        case finished(rating: Double)
    }

    let numberOfPages: Int

    let readState: ReadState

    func progress(book: Book) -> Double {
        switch readState {
        case .pending:
            0
        case .inProgress(let page):
            page / numberOfPages
        case .finished:
            100
        }
    }

}
```

Note how accessing associated values of a given case (like `.finished` in the example above) is completely optional.

## Iterating over values
Sometimes it's useful to have a collection of all constants in an enumeration.

In Java this is straightforward because all values are known at compile time and the `Enum` class provides a [values()](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/lang/Enum.html#valueOf(java.lang.Class,java.lang.String)) static method returning them:

```java
// Java
enum Season {
    SPRING,
    SUMMER,
    AUTUMN,
    WINTER;
}

for (var season: Season.values()) {
    System.out.println(season);
}
```

In Swift the same can be achieved by adopting the [CaseIterable](https://developer.apple.com/documentation/swift/caseiterable) interface, which provides an equivalent `allCases` property:

```swift
// Swift
enum Season: CaseIterable {
    case spring
    case summer
    case autum
    case winter
}

for season in Season.allCases {
    print(season)
}
```

The difference is that, while in many cases the Swift compiler is also able to generate the implementation of `allCases` for us, there are some exceptions.

For example, if we wanted to use associated values we would need to implement `allCases` ourselves, which is often impractical:

```swift
// Swift
enum ReadState: CaseIterable {
    case pending
    case inProgress(page: Int)
    case finished(rating: Double)

    // Naive implementation using hardcoded limits
    static var allCases: [Self] {
        let inProgressCases = stride(from: 0, through: 2000, by: 1)
            .map(Self.inProgress)
        let finishedCases = stride(from: 0.0, through: 5.0, by: 0.25)
            .map(Self.finished)
        return [.pending] + inProgressCases + finishedCases
    }
}
```

## Extending enumerations behaviour
We can extend the behaviour of enumerations in several ways.

One already shown in previous sections is by implementing interfaces. Java's `Enum` base class implements [Comparable](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/lang/Comparable.html) among others. And we saw how adopting the `CaseIterable` interface in Swift allows us to generate all values of an enumeration.

Another obvious way is by writing our own instance methods:

```java
// Java
enum CreditCardType {
    SILVER(0.0025),
    GOLD(0.005),
    PLATINUM(0.0075);

    private final double cashbackRate;

    CreditCardType(double cashbackRate) {
        this.cashbackRate = cashbackRate;
    }

    double cashback(double amount) {
        return amount * cashbackRate;
    }
}

var card = CreditCardType.PLATINUM;

var formatter = new DecimalFormat("O###,###.0000");
System.out.println(formatter.format(card.cashback(15))); // 0.1125
```

```swift
// Swift
enum CreditCardType: Decimal {
    case silver = 0.0025
    case gold = 0.005
    case platinum = 0.0075

    func cashback(for amount: Decimal) -> Decimal {
        amount * rawValue
    }
}

let card = CreditCardType.platinum
print(card.cashback(for: 15)) // 0.1125
```

Note how in both examples above we get the same behaviour regardless of the underlying enumeration constant: `amount` is multiplied by the corresponding `cashbackRate`. But what if we wanted a different behaviour for each case?

In Swift there's no other way but switching over `self`:

```swift
// Swift
enum CompassDirection {
    case north
    case east
    case south
    case west

    var reversed: Self {
        switch self {
        case .north:
            .south
        case .east:
            .west
        case .south:
            .north
        case .west:
            .east
        }
    }
}
```

We can do the same in Java, but switching over `this` is often regarded as a code smell[^2]:

```java
// Java
enum CompassDirection {
    NORTH,
    EAST,
    SOUTH,
    WEST;

    // This is OK, but we can do better
    CompassDirection reversed() {
        return switch (this) {
            case NORTH -> SOUTH;
            case EAST -> WEST;
            case SOUTH -> NORTH;
            case WEST -> EAST;
        };
    }
}
```

Instead, we can leverage the fact that `Enum` is a class and declare the behaviour we need as an `abstract` method:

```java
// Java
enum CompassDirection {
    NORTH {
        @Override
        CompassDirection reversed() {
            return SOUTH;
        }
    },
    EAST {
        @Override
        CompassDirection reversed() {
            return WEST;
        }
    },
    SOUTH {
        @Override
        CompassDirection reversed() {
            return NORTH;
        }
    },
    WEST {
        @Override
        CompassDirection reversed() {
            return EAST;
        }
    };

    abstract CompassDirection reversed();
}
```

This is actually quite clever. Using an abstract method forces us to provide an implementation for each constant because the compiler complains otherwise. And the overall implementation it's arguably easier to understand because each behaviour is closer to the constant it applies, rather than several lines below in the `enum` body.

## Conclusion
We have only scratched the surface of what's possible with enumerations in Java and Swift. Although both offer the same basic functionality, some language design decisions have resulted in different, more advanced capabilities.

In Swift, the most notable is perhaps [associated values](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations/#Associated-Values), which can be of a variable number and from heterogeneous types.

In the case of Java, I was pleasantly surprised by the ability to associate different behaviours with each constant by having abstract methods instead of switching over `this`.

I hope you've found this small comparison of such an essential type useful. I have left out things like [recursive enumerations](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations#Recursive-Enumerations), in hope that you can discover them and continue exploring on your own.

[^1]: Swift's `enum` is in this way quite similar to a [tagged union](https://en.wikipedia.org/wiki/Tagged_union).
[^2]: This seems a widespread view in Object-Oriented Programming and has been catalogued by Martin Fowler as a code smell in ["Refactoring: Improving the Design of Existing Code"](https://martinfowler.com/books/refactoring.html).
