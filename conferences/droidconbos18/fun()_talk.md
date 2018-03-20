footer: @n8ebel
build-lists: true
slidenumbers: true

# outline

intro
key takeaways

transition

parameter & type freedom

transition

scoping freedom

transition

___

#[fit] fun() Talk

## Exploring Kotlin Functions

^ At this point, I think it's safe to say most everybody here has at least heard of Kotlin

^ If not, I encourage you to check it out
^ And hopefully this will spark your curiosity
___

# [fit] Kotlin ♥️ Functions

___

# Kotlin ♥️ Functions
## Many great features
- Both member functions and top-level functions
- Functions that take other functions as arguments
- Terrific stdlib filled with useful functions

___

# 3 Key Takeaways

- Easy to get started
- Many ways to write, modify and utilize functions
- Functions enable us to reimagine how we build projects

___

## Easy to get started, but much more to discover

^ getting started with Kotlin functions is easy
^ we'll see how quickly you can convert a java method to a kotlin function and you'll be off and running

^ but there is so much more to learn and discover about functions in Kotlin
___

## Functions can be written, modified, and used in a variety of ways

- parameter freedom
- multiple types
- variations in scoping
- variety of modifiers

___

## Functions provide freedom to reimagine how we build for Android

> the flexibility & functionality of functions allow us to break away from traditional java convention and reimagine how we build our projects

___

> We're going to explore function's from their basics variants to more complex iterations

___

# [fit] Let's Have Some fun()

___

> From methods to Functions

^ without further ado, let's kick off this dive into Kotlin functions by looking at some Java code 😀

___

# simple java method
```java
void helloFunctions() {
  System.out.println("Yay, Functions");
}
```
- return type
- name
- method body

^ here we have the Java method that we probably all know
^ whether you love it or hate it is between you and java

^ we'll start here though so we can build up our mental model of Kotlin functions with a common starting point

___

# java method converted to kotlin
```Kotlin
fun helloFunctions() {
  println("Yay, Functions")
}
```

^ not that different right?

- adds the fun keyword
- same name
- no explicit return type

___

# Kotlin can be even more concise

```kotlin
fun helloFunctions() = println("Yay, Functions")
```

^ for this simple case, we can simplify this function even more
^ can ommit the braces alltogether
^ this form is known as a single-expression function
___

# So What's The Big Deal?

seems pretty straightforward, what else is there to know?

___

# [fit] A Lot

___

# Building On What We Know

^ let's build on our example to explore how you can interact with a function
___

# Parameter & Type Freedom

- default
- named
- return types
    - when can omit?
    - when can infer?
- templated
- higher order

___

# Parameters

```Kotlin
fun helloFunctions(excitingThing:String) {
  println("Yay, " + excitingThing)
}

helloFunctions("functions")
```

^ parameters are defined using <name> colon <type>

___

# Parameters

```Kotlin
fun helloFunctions(exclamation:String, excitingThing:String) {
  println(exclamation + ", " + excitingThing)
}

helloFunctions("Yay", "functions")
```

^ multiple parameters are separated by commas

___

> Now It Gets Interesting

___

# Default Arguments

```Kotlin
fun helloFunctions(exclamation:String, excitingThing:String = "functions") {
  println(exclamation + ", " + excitingThing)
}

helloFunctions("Yay", "functions")
helloFunctions("Yay")
```

- allows us the flexibility of overloads without the verbosity of writing them

^ Function parameters can have default values, which are used when a corresponding argument is omitted.

___

# Named Arguments

```Kotlin
helloFunctions(
  excitingThing = "functions",
  exclamation = "Horray"
)

helloFunctions("Hooray")

helloFunctions("hooray", excitingThing = "Droidcon Boston")
```
^ notice we've reversed the order in which these are passed
^ by providing the name, the correct behavior is achieved

^ This allows for a reduced number of overloads compared to other languages:

___

# Variable number of arguments

we can define a parameter to accept a variable number of arguments T

^ like in Java

use the `vararg` keyword

the `vararg` param is then treated as an array of type T
___

# Variable number of arguments

```Kotlin
fun helloFunctions(exclamation:String, vararg excitingThings:String) {
  for(excitingThing in excitingThings) {
    println(exclamation + ", " + excitingThing)
  }
}

helloFunctions("yay!", "Droidcon Boston", "Kotlin", "Android")
```
___

# Variable number of arguments

typically, a `vararg` parameter will be the last one

can use anywhere if
- other parameters are called using named argument syntax
- last parameter is a function passed outside the parentheses

```Kotlin
helloFunctions("Droidcon Boston", "Kotlin", "Android", exlamation="yay!")
```
___


# Variable number of arguments spreading

Use `spread` operator to pass an existing array of values

```Kotlin
val thingsToBeExcitedAbout = arrayOf("Droidcon Boston", "Kotlin", "Android")
helloFunctions("yay!", *thingsToBeExcitedAbout)
helloFunctions("yay!", "coffee", *thingsToBeExcitedAbout)
```

- can be alone, or with other passed varargs as well
___

# Return Types

```Kotlin
fun helloFunctions(exclamation:String, excitingThing:String="functions") {
  println(exclamation + ", " + excitingThing)
}
```

^ you might have noticed that no return type is specified

___

> If a function does not return any useful value, its return type is Unit

___

# Return Types

These are equivalent

```Kotlin
fun helloFunctions(exclamation:String, excitingThing:String="functions") : Unit {
  println(exclamation + ", " + excitingThing)
}

fun helloFunctions(exclamation:String, excitingThing:String="functions") {
  println(exclamation + ", " + excitingThing)
}
```
___

# Return A Non-Unit Type

function with block body require explicit return type & call for non-Unit functions

```Kotlin
fun helloFunctions(exclamation:String, excitingThing:String="functions") : String {
  return exclamation + ", " + excitingThing
}
```
___

# Return A Non-Unit Type

can infer return type for single-expression functions

```Kotlin
fun helloFunctions(exclamation:String, excitingThing:String="functions")
    = exclamation + ", " + excitingThing
```
___

# Generic Functions

Like classes, functions may have generic type parameters

```Kotlin
fun <T> log(item: T) {
    // ...
}

log(Foo())
log(Goo())
```

___

> concise
> convenient
> flexible

___

# What Next?

___

# [fit] Variations On A Theme

> Let's explore some variations on how you can create and use functions

___

# Variations In Scope

- top-level
- methods
- local
- CompanionObject
- extension functions

___

# Top-Level functions
- available everywhere
- not tied to a class
- enabling interesting patterns

___

# Top-Level Function Patterns
- replace need for globablly available methods or instances
- ex: logger

- basic building block of dsls

___

# Top-Level Function Considerations

- generated as static? (** need to check this**)
- available from Java using special convention

___

# Methods

- function on a class or object
- **default arguments can't be changed in overridden methods**

___

# Local Functions

- can create a function that is scoped to another function
- similar to javascript?
- useful if your function is only ever called from another function

___

# Local Function Considerations

- local function vs private method?
- performant?

___

# Functions on a CompanionObject

- how do these differ?

___

# Functions on a CompanionObject Considerations

- ???

___

# [fit] Special Cases

___

# [Special Cases]

- `infix`
- `inline`
- `extension`
- higher-order
- lambdas
- anonymous

___

# infix

___

# Extension Functions

- people love and know these
- extend existing class
- can cleanup apis, simplify or remove helpers
- again can be leveraged for dsls

___

# Extension Function Considerations
- how are these generated under the hood?
- how are these called from Java?

___

# Higher-Order Functions

inception time

functions that take other functions are parameters

- allow very interesting Patterns
- can cleanup setup/teardown patterns such as shared prefs
- very helpful in dsls

___

# Higher-Order Functions

- show example of usage
- dont use lambda yet

___

# Higher-Order Functions

- if the last parameter is a function, can ommit the parentheses and
lambda syntactic sugar

threading syntax
receiver functions in stdlib

there is a convention that if the last parameter to a function is a function, and you're passing a lambda expression as the corresponding argument, you can specify it outside of parentheses

___

# lambdas

> "A lambda expression or an anonymous function is a "function literal", i.e. a function that is not declared, but passed immediately as an expression"

___

# anonymous functions

- how are they different from a lambda
- how do we use them (pass them to another function) ??
- how are types inferred?

___

# function literals w/ receiver

___

# Higher-Order Function Performance

> "Using higher-order functions imposes certain runtime penalties"

# inline

- helps solve higher-order function performance hits
- how?

___

## inline

- mark with inline keyword
- does that then make all the fuction params inlined?
- can use `noinline` for args if needed

___

## inline: returns

- non-local returns
- crossline

## inline: restrictions

- there are some restrictions..

___

# Android Reimagined

These features enabled us to rethink how we build our apps

___

# Android Reimagined

### Avoiding `if`

`foo?.let{}`
`when(foo){
  true ->
  false ->
  }`

___

# Android Reimagined

## Safer Strategies

`fun doTheThingSafely(theThing:() -> Unit){
    try {
      theThing()
    } catch(error:Throwable) {
      // handle error
    }
}`

___

# Android Reimagined

## Upgrade Our Apis

can use extensions, default params, etc to cleanup common apis

- shared prefs
- ktx
- anko

___

# Android Reimagined

## Fewer Helpers to Pass Around

Can utilized top-level functions for globally vailable actions such as logging

Remove direct dependencies that must be shared
Allow's for configuration
Impacts testing

___

# Android Reimagined
## Building a DSL

???  dsl for parsing things from the Contentful sdk ???
___

# Summary

functions let us do yada yada yada

___

# [fit] Thanks

## @n8ebel
