---
title: What nobody will tell you about JSON
description: Edited transcription of "What nobody will tell you about JSON", a talk I gave for App Builders Zürich.
---
This is an edited transcription of [a talk](http://www.meetup.com/App-Builders-Zurich/events/231739951) I did for [App Builders Zürich](http://www.meetup.com/App-Builders-Zurich/) on July 2016. I have arranged the content in a different way and omitted some parts to make the written version more coherent. The slides are also [available in PDF]({{ site.url }}/files/what_nobody_will_tell_you_about_json.pdf).

<!--more-->

---

## Motivation
Back in February, the mobile team at [FIFA TMS](https://www.fifatms.com) had to develop a new feature for [GPX](https://www.fifatms.com/gpx/). The application was written in Objective-C at that time, but this new feature was pretty much isolated from the rest of the code. The only shared components were an HTTP client to fetch data from back-end, an style guide and some small helpers. We decided to implement it in Swift, because we would not need to [mix and match](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/BuildingCocoaApps/MixandMatch.html) both languages too much.

One of the decisions that we had to make was how to parse back-end responses. We didn’t want to reinvent the wheel, so we started looking at existing solutions. That led us to discover some interesting facts about third-party libraries in Swift, in particular for parsing JSON.

At the time of this writing, these are the number of GitHub repositories mentioning JSON and decoding/parsing, without including forks:

* [Objective-C](https://github.com/search?utf8=✓&q=JSON+parsing+OR+decoding+fork%3Afalse+language%3AObjective-C&type=Repositories): 1611 results.
* [Swift](https://github.com/search?utf8=✓&q=JSON+parsing+OR+decoding+fork%3Afalse+language%3ASwift&type=Repositories): 1038 results.

If you do the math, it means that for every three Objective-C libraries there are almost two Swift libraries. That seems to mimic a similar trend in the Apple ecosystem in general, as [pointed out by Orta Therox](https://twitter.com/orta/status/748139249074053120):

> *Looks like in the last month for every 4 Obj-C libraries, there are 3 Swift libraries.*

There might be several reasons for this trend but since I'm not a data analyst I'm not going to go into details. I'll just leave the numbers here to pick your curiosity.

What I would like to do is share a journey that I went through while looking for a library to parse JSON in GPX. This will serve as an excuse for sharing a few tips about sustainable development, specifically about how to deal with third-party libraries. It won’t be cutting-edge, but I also think that it would be a good idea to [stay away from the hype](https://medium.freecodecamp.com/being-a-developer-after-40-3c5dd112210c) and revise how we are solving problems in Swift with a bit of perspective.

Before we continue, let me clarify the terminology we will use:

* **Deserialising** (or *decoding*) is the operation that transforms binary data into a data structure that represents a JSON text (e.g `[String: AnyObject]` in Swift).
* **Parsing** is the operation that fetches values from that data structure (e.g. querying a dictionary).


## JSON demystified
Let's start with a brief summary on what is JSON and how we’ve been using it on Apple platforms.

### When, why and how JSON was born
JSON was popularised by [Douglas Crockford](http://crockford.com) in 2001 as a format to transmit data between programs. It was developed as a subset of the JavaScript-based syntax defined in the standard [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm). Intended to be a replacement for the complexity of XML, it quickly gained adoption because of its simplicity. You can [listen to the story](https://www.youtube.com/watch?v=kc8BAR7SHJI) by the man himself.

So despite what a lot of people think, there is actually a JSON standard:

* [RFC 4627](https://tools.ietf.org/html/rfc4627), written by Douglas Crockford on 2006. He basically formalised the syntax that was originally published in [json.org](http://json.org) in 2002.
* [ECMA-404](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf), released on 2013. The standard was officially defined, consolidating the syntax for producing JSON text.
* [RFC 7158](https://tools.ietf.org/html/rfc7158) and [RFC 7159](https://tools.ietf.org/html/rfc7159), released on 2013 and 2014 respectively. It clarified and proposed a set of best practices to avoid interoperability problems.

The syntax specification is the same in all documents. The only difference is that the RFCs go a little bit further by including operational aspects, like the reserved MIME type (`application/json`) or the preferred text encoding (UTF-8).

### Looking for alternatives?
Are there any alternatives to JSON for transmitting data? The answer to this question is a bit tricky. There are alternatives indeed, but one of the keys for the success of JSON has been its simplicity. With that in mind we could:

* Go back to [XML](https://en.wikipedia.org/wiki/XML), but I guess that’s not really an option.
* Use [YAML](http://yaml.org), but it also its own issues.
* Use [MessagePack](https://en.wikipedia.org/wiki/MessagePack), which is closely related to JSON and somewhat more performant.
* Go for [FlatBuffers](https://google.github.io/flatbuffers/index.html), which is a whole different concept.

These are only some well-known examples, there are plenty of options out there. Some of them might be more performant, but most of them don't have native support in either Objective-C or Swift. Thus, the complexity they add to the code doesn't make them worthy. MessagePack is maybe the only format that I would really consider as a replacement, because the syntax is roughly the same but the performance is a little bit better.


## Which tools does Apple give us?
So having defined the basics of what is JSON, let’s see now the main tool that Apple gives us to work with it: [NSJSONSerialization](https://developer.apple.com/library/ios/documentation/Foundation/Reference/NSJSONSerialization_Class/index.html#//apple_ref/occ/cl/NSJSONSerialization).

`NSJSONSerialization` was introduced in 2011 with iOS 5 and has been the *de facto* class to serialise and deserialise JSON objects. The public interface is minimal, with two main methods:

* `JSONObjectWithData(_:options:)`, to deserialise `NSData` into `AnyObject`.
* `dataWithJSONObject(_:options:)`, to serialise `AnyObject` into `NSData`.

It’s worth noting that Apple has only made one [revision in 2014](https://developer.apple.com/library/ios/documentation/Foundation/Reference/NSJSONSerialization_Class/RevisionHistory.html#//apple_ref/doc/uid/TP40010946-CH99-SW1), just to clarify the behaviour of the error reporting.

The documentation also states an important limitation regarding the latest JSON standard:

> *The top level object is either an `NSArray` or an `NSDictionary`.*

This is an interesting one, because the standard actually allows any JSON value as a top-level root object. And there is also an important advice:

> *Other rules may apply. Calling `isValidJSONObject:` or attempting a conversion are the definitive ways to tell if a given object can be converted to JSON data.*

I couldn't find which "other rules" they refer to ¯\\_(ツ)\_/¯. So on the event of unexpected behaviour we have to use `isValidJSONObject:` to debug.

This lack of support of the latest standard is probably the fundamental reason that justifies writing an alternative JSON serialiser. Although, to be honest, I have rarely found myself receiving a JSON object where the top-level object was not a dictionary or an array.


## What's wrong with parsing JSON?
By reading the standard we can see that JSON is a fairly simple format. What’s wrong with it then? Why do we have such proliferation of libraries for Swift, attempting to provide the definitive way of doing something that simple? Bear with me and let’s propose a few hypothesis on that.

### 1. Limited support in Swift
The first reason could be the limited support that Swift offers. If you think about it, parsing JSON in Objective-C is easier thanks to reflection and Key Value Coding. [Mantle](https://github.com/Mantle/Mantle) and [OSReflectionKit](https://github.com/iAOS/OSReflectionKit) are two good examples of it.

Swift on the other hand has limited support for reflection. There are some protocols like [CustomReflectable](https://developer.apple.com/library/ios/documentation/Swift/Reference/Swift_CustomReflectable_Protocol/index.html) and the [Mirror](https://developer.apple.com/library/ios/documentation/Swift/Reference/Swift_Mirror_Structure/index.html#//apple_ref/swift/struct/s:Vs6Mirror) type. But still, it doesn’t have the dynamism of Objective-C.

However, the problem here might be that we’re trying to solve a problem using the same approach, when we have fundamentally different languages.

### 2. NSJSONSerialization is not fully compliant
The second reason could be the limitations of NSJSONSerialization. Maybe because we are not happy with its performance, maybe because the Objective-C API doesn’t play well with Swift or maybe because we want full support of the latest RFC.

### 3. Learning experience
The third reason could be to use it as a learning exercise. Fair enough, it’s indeed an interesting exercise and a good way to explore the language. But again, that doesn’t justify the release of so many libraries.

### 4. Bragging
Which brings us to the last reason: bragging! Swift is a new language and it’s so cool to show the latest thing that we did with it.


## Evaluating libraries
Going back to the beginning of the post, let's actually go through all the libraries for parsing JSON that we tried.

### 1. Freddy
The first library we tried was [Freddy](https://github.com/bignerdranch/Freddy), from the guys at [Big Nerd Ranch](https://www.bignerdranch.com). Here is an example on how to parse data:

```swift
import Freddy

let data = getSomeData() // returns NSData
do {
  let json = try JSON(data: data)
  let success = try json.bool("success")
  // do something with `success`
} catch {
  // do something with the error
}
```

The first thing to note here is that `json` is initialised with an `NSData` object. Freddy implements its own deserialiser, so we can skip `NSJSONSerialization` altogether. While they claim that is faster, one disadvantage is that we cannot use the default serialisers of some famous HTTP clients (e.g. [Alamofire](https://github.com/Alamofire/Alamofire/blob/2501fc92eaf2d4e6d0b316d8fb5bb2eb41311f86/Source/ResponseSerialization.swift#L290)). So this library looked great, but in return we had to extend our HTTP client to replace `NSJSONSerialization` with something else.

Populating models with a JSON object is possible with a protocol. This approach is really common in many libraries out there:

```swift
struct Person {
  let name: String
  let age: Int
}

extension Person: JSONDecodable {
  init(json value: JSON) throws {
    name = try value.string("name")
    age = try value.int("age")
  }
}
```

Note that we have to use a specific method for every data type. I think this is redundant, because there's no much difference with `value["name"] as? String`. On the other hand, having all the error handling internally comes in handy.

### 2. Argo
Then we tried [Argo](https://github.com/thoughtbot/Argo), from [Thoughtbot](https://thoughtbot.com). This library uses currying heavily, so we actually have to import two libraries: Argo and [Curry](https://github.com/thoughtbot/Curry). Here is an example on how to parse data:

```swift
import Argo
import Curry

struct Person {
  let name: String
  let age: Int
}

extension Person: Decodable {
  static func decode(j: JSON) -> Decoded<User> {
    return curry(User.init)
      <^> j <| "name"
      <*> j <| "age"
    }
}

let json: AnyObject? = try? NSJSONSerialization.JSONObjectWithData(data, options: [])

if let j: AnyObject = json {
  let person: Person? = decode(j)
}
```

Just take a moment to see all the things that take part in this convoluted solution:

1. Generics.
2. Three custom operators.
3. Currying.
4. Three additional types (`Decodable`, `JSON` and `Decoded`).

However the authors state in the documentation the following:

> *We feel that these patterns greatly reduce the pain felt in trying to use JSON with Swift*.

With all due respect, my answer to that is this quote from a [Nick O’Neill's talk](https://realm.io/news/slug-nick-oneill-native-swift-patterns/):

> *Not every piece of clever code is a great pattern.*

### 3. ObjectMapper
Let's continue with [ObjectMapper](https://github.com/Hearst-DD/ObjectMapper), by [Hearst](http://www.hearst.com). Here is an example on how to parse data:

```swift
import ObjectMapper

struct Person {
  var name: String
  var age: Int
}

extension Person: Mappable {
  init?(_ map: Map) {}

  mutating func mapping(map: Map) {
    name <- map["name"]
    age  <- map["age"]
  }
}
```

This library also uses custom operators, but at least they're more intuitive and easier to read; they almost look like assignment operators.

But the biggest disadvantage is that it forces us to use mutable properties on a model. That's because they decided to implement parsing as an operation that occurs after initialising an object.

This approach works really well if we are dealing with Core Data objects, which are inherently mutable. But for the rest of cases, the safety net of the Swift compiler is just out of the window.

### 4. SwiftyJSON
The next candidate is [SwiftyJSON](https://github.com/SwiftyJSON/SwiftyJSON). Here is an example on how to parse data with it:

```swift
import SwiftyJSON

struct Person {
  let name: String
  let age: Int
}

extension Person {
  init?(json: [String: AnyObject]) {
    guard let name = json["name"].string else {
      return nil
    }

    guard let age = json["age"].int else {
      return nil
    }

    self.name = name
    self.age = age
  }
}
```

SwiftyJSON starts to look like a decent solution. To begin with, we don't need any custom types. We can just pass a plain dictionary, as returned by `NSJSONSerialization`. And we are not forced to use a given initialiser from a protocol. We have complete freedom to populate our objects however we want.

But this library still has one issue, the same as Freddy: we have to be explicit with the type of the objects we are trying to fetch. It seems to me that we could use some type inference here. Moreover, error handling might become really verbose as shown in this particular example.

### 5. Unbox
So finally, the last library we tried: [Unbox](https://github.com/JohnSundell/Unbox), by [John Sundell](). I have to admit that this one is my favourite by far, kudos to John for this fantastic tool. This is how you can parse JSON with Unbox:

```swift
import Unbox

struct Person {
  let name: String
  let age: Int
}

extension Person: Unboxable {
  init(unboxer: Unboxer) {
    name = unboxer.unbox("name")
    age = unboxer.unbox("age")
  }
}

let person: Person = try Unbox(dictionary)
```

With Unbox we can keep our objects immutable, we make use of type inference to avoid being explicit with the data types and we can use plain dictionaries as well. You can see how better is this library just by comparing the amount of code needed, yet remaining simple and easy to read.

But there's still one small drawback: we have to depend on the `Unbox` function, the `Unboxable` protocol and the `Unboxer` type. And we wanted to keep our interfaces free from foreign types.

### 6. Our own parser
So after trying all these libraries we became really frustrated. None of them offered us exactly what we were looking for.

But then I came across an [article by Soroush Khanlou](http://khanlou.com/2016/04/decoding-json/) where he also described his struggles with JSON decoding. He mentions three key things that we wanted:

* Avoiding explicit types by using type inference.
* Handling the existence/absence of keys by wrapping the native `Dictionary` type (it doesn’t throw errors when keys are missing).
* Keeping error handling simple by using a `do` statement as opposed to using `guard`, which tends to be verbose when you have lots of values to fetch.

So inspired by Soroush's post we went ahead and implemented our own JSON parser. Here's what parsing JSON looks like with our solution:

```swift
struct Person {
  let name: String
  let age: Int
}

extension Person: Deserializable {
  init?(response: [String: AnyObject]) {
    let parser = JSONParser(response)

    do {
      name = try parser.fetch("name")
      age = try parser.fetch("age")
    } catch {
      return nil
    }
  }
}
```

We finally came up with a combination of all the things that we liked from all the solutions we tried, while discarding the things we didn’t like:

1. Keeping our properties immutable.
2. Avoiding being explicit with the property types, thanks to generics and type inference.
3. Avoiding (ab)using any custom operators. We decided to [favour clarity over brevity](https://swift.org/documentation/api-design-guidelines/#fundamentals).
3. Using the native `Dictionary` type, but wrapped into an object that handles all the error conditions.
4. Keeping error handling locally by using a `do` statement. From a higher level perspective we only wanted to know if the object could be created or not. Hence, the failable initialiser.

I’m not going to show all the code here, but let’s take the main function as an example. The rest of the functions call this one in one way or another.

```swift
struct JSONParser {

  private let dictionary: [String: AnyObject]?

  init(_ dictionary: [String: AnyObject]) {
    self.dictionary = dictionary
  }

  func fetch<T>(key: String) throws -> T {
    guard let object = dictionary?[key] else  {
      throw ParseError.KeyNotFound(key)
    }

    guard let value = object as? T else {
      throw ParseError.TypeMismatch(key: key, expected: T.self, found: object.dynamicType)
    }

    return value
  }

}
```

As you can see, fetching a value is as simple as:

1. Checking that the key exists.
2. Checking that the value matches the expected type.
3. Returning the value.


## Lessons to learn
This journey was a little bit painful, but a good exercise overall. So like I said at the beginning, parsing JSON is just an excuse that I wanted to use to share with you some principles or tips about sustainable development.

### Reasons to avoid a third-party JSON library
While adding a third-party library might sound like the most logical thing to do (it did for us), there are a few things to keep in mind.

#### 1. Make sure your problem is not somewhere else
We saw that `NSJSONSerialization` is limiting and does not fulfil the standard completely. But in our case it covered all our needs. We as developers are tempted sometimes to try anything that is more performant or faster. But is it really worth the complexity added? In my experience, if an iOS application is suffering from performance problems, the answer is often somewhere else, not while parsing JSON.

#### 2. Strive for simple solutions to simple problems.
We have learnt that a deeper knowledge of the language gave us new possibilities. Our JSON parser is really simple. With less than 200 hundred lines we covered all of our cases, including error handling and providing default values in case of errors.

We could’ve given up and patch our code base to make it work with one of the libraries we tried. But we kept looking and learning until we found the simplest possible solution. My advise here would be to think it twice before adding third-party code to solve a simple problem, because probably [YAGNI](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it).

#### 3. Stay as close as possible to an evolving platform
Swift is evolving fast and things break often. And with [Swift 3](http://oleb.net/blog/2016/06/swift-3/) this is going to be really painful. So it’s really convenient to keep our interfaces simple and independent from external components.

Let me give you an example. A lot of people relying in [PromiseKit](https://github.com/mxcl/PromiseKit) could not release apps after upgrading Xcode from 7.3 to 7.3.1 due to a [bug in the compiler](https://bugs.swift.org/browse/SR-1427). But Xcode 7.3.1 also fixed some other compiler issues. Developers in this situation had to decide whether to keep using 7.3 and wait on Apple or PromiseKit to fix the issue or patch PromiseKit themselves.

Can we afford to wait on framework maintainers to keep the pace of Swift changes? Sometimes we can, sometimes we cannot. That’s why we discarded libraries that forced us to use additional types and prefer to use the native types. Staying close to the platform is the best way to avoid future headaches until Swift 3 proves to be stable enough. Dave Thomas [put it best](https://youtu.be/a-BOSpxYJ9M?t=23m15s) this way:

> When faced with two or more alternatives that deliver roughly the same value, take the path that makes future change easier.

### Reasons for using a third-party JSON library
Now, I don’t want to discourage anyone from using third-party libraries at all. I am particularly conservative when it comes to that, but that’s my personal choice as a developer. There are also good reasons and appropriate scenarios where using a library totally makes sense.

#### 1. Constraints or prototyping
If there are serious resource constraints or we are just simply building a prototype, an existing solution will do the job.

But I want to emphasise here the word *"serious"*. Sometimes we fool ourselves into thinking that we don’t have enough time and we want to rush into code. And one month later we found that we have to review that design again because we jumped too fast into a solution. But if the constraints are real and unavoidable, go for it.

#### 2. Sometimes Apple doesn’t just work
If for any reason we wanted to have full support of the standard, then our only choice would’ve been to use Freddy. And writing a deserialiser is a way more complex task compared with writing a simple parser. So in that case, using an external component would've been the right choice.

#### 3. Objective-C
Objective-C is very dynamic in nature and that might lead to a lot of errors. In my experience it's easier to get something wrong in Objective-C compared to Swift.

But the Objectice-C compiler is also way more stable than Swift and some of the libraries out there have been already tested in many battles. We can benefit from these years of experience, stability and testing, instead of writing our own solutions. That's why I always use Mantle when I have to parse JSON in Objective-C.


## Conclusion
I hope that with these insights I have contributed to shed some light on the issues of parsing JSON (e.g. over-engineering) and encourage you to think twice before adding complexity to your code.
