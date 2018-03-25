footer: @n8ebel #droidconbos
build-lists: true
slidenumbers: true


#[fit] fun() Talk

## Exploring Kotlin Functions

^ At this point, I think it's safe to say most everybody here has at least heard of Kotlin

^ If not, no worries.  I'm not going to make you raise your hand
^ However, I encourage you to check it out
^ And hopefully this will spark your curiosity
___

# [fit] Kotlin ♥️ Functions

^ 1st party citizens
^ functions aren't tied to a class
^ many useful functions in the stdlib

___

## Easy to Get Started

^ getting started with Kotlin functions is easy

- Can use the IDE conversion tool
- Can try online
- Easy to transfer existing knowledge

^ but much more to discover
___

## Flexible & Convenient

^ the features of Kotlin functions make them flexible and convenient

- Parameter & type flexibility
- Variations in scoping
- Variety of modifiers

^ we'l explore a variety of ways that these make our lives easier as developers

___

## Freedom to Reimagine

> The flexibility & functionality of functions allow us to break away from traditional java conventions and reimagine how we build our projects

___

# Takeaways

- Easy to get started
- Flexibility in how we write, modify and utilize functions
- Functions enable us to reimagine how we build projects

^ We're going to explore function's from their basics variants to more complex iterations

___

# [fit] Let's Have Some fun()

___

> From Methods to Functions

^ without further ado, let's kick off this dive into Kotlin functions by looking at some Java code 😀

___

# Hello Java Method

^ here we have the Java method that we probably all know
^ whether you love it or hate it is between you and java

```java
void helloFunctions() {
  System.out.println("Yay, Functions");
}
```
- return type
- name
- method body

^ we'll start here so we can build up our mental model of Kotlin functions with a common starting point

___

# java method converted to kotlin

^ if converted with Android Studio we might get something like this

```Kotlin
fun helloFunctions() {
  println("Yay, Functions")
}
```

^ not that different right?
^ but there are a few things to notice

- adds the `fun` keyword
- no explicit return type
- same name

^ great.  pretty straightforward. a little more conside version of the familiar java method

___

# Further Simplification

^ for this simple case, we can simplify this function even more

```kotlin
fun helloFunctions() = println("Yay, Functions")
```

^ can ommit the braces alltogether
^ this form is known as a single-expression function
^ we'll look a bit closer at how this works in a bit
___

# So What's Left?

^ functions dont seem that different.
^ maybe just a bit more concise

Seems pretty straightforward, what else is there to know?

___

# A Lot

^ thankfully or this would be an awkwardly short talk

___

> Let's Build On What We Know

^ let's build on our example to explore how you can interact with a function
___

# Parameter & Type Freedom

- Default parameters
- Named parameters
- Return types
    - when can we omit?
    - when can we infer?
- Generic functions

^ let's start by looking at paramter basics
___

# Parameters

^ if we couldn't have parameters, functions would be pretty boring
^ parameters are defined using <name> colon <type>

```Kotlin
fun helloFunctions(excitingThing:String) {
  println("Yay, " + excitingThing)
}

helloFunctions("functions")
// outputs "Yay, functions"
```

___

# Parameters

^ of course we can have multiple parameters as well
^ multiple parameters are separated by commas

```Kotlin
fun helloFunctions(exclamation:String, excitingThing:String) {
  println(exclamation + ", " + excitingThing)
}

helloFunctions("Yay", "functions")
// outputs "Yay, functions"
```

___

> Now It Gets Interesting

___

# Default Parameter Values

```Kotlin
fun helloFunctions(exclamation:String, excitingThing:String = "functions") {
  println(exclamation + ", " + excitingThing)
}

helloFunctions("Yay", "functions")
// outputs "Yay, functions"

helloFunctions("Yay")
// outputs "Yay, functions"
```
___

> Function parameters can have default values, which are used when a corresponding argument is omitted

___

# Default Parameter Values

- allows us the flexibility of overloads without the verbosity of writing them
- help document the function contract by indicating what "sensible defaults" might be

___

# Default Parameters & Java

Java doesn't have default parameter values

- must specific all parameter values when calling from Java
- can use `@JvmOverloads` to generate overloads for each parameter
- generated overloads will used the specified default values

___

# Named Arguments

Improve readability of function invocations
How do we know which value is correct?

^ examine the source/documentation?

<br>

```Kotlin
helloFunctions("functions", "functions")
```

___

# Named Arguments

Much easier to understand with named arguments
<br>

```Kotlin
helloFunctions(exclamation = "yay!", excitingThing = "functions")
```

___

# Named Arguments

^ looking at our example, notice the names of the parameters

Modify order of passed parameters by using named arguments

```Kotlin
fun helloFunctions(exclamation:String, excitingThing:String = "functions") {
  println(exclamation + ", " + excitingThing)
}
```

```Kotlin
helloFunctions("Hooray", "functions")
helloFunctions("Hooray")
helloFunctions(excitingThing = "functions", exclamation = "Hooray")
// all output "Hooray, functions"
```
^ notice we've reversed the order in which these are passed
^ by providing the name, the correct behavior is achieved

^ This allows for a reduced number of overloads compared to other languages:

___

# Named Arguments

There are limitations to how named & positioned arguments are used
- once an argument name is specificed, all subsequent arguments must be named as well

___

# Named Arguments

^ this example works fine

```Kotlin
helloFunctions("hooray", "Droidcon Boston")
helloFunctions("hooray", excitingThing = "Droidcon Boston")
// both output "hooray, Droidcon Boston"
```

^ this example fails to compile

```Kotlin
helloFunctions(excitingThing = "Droidcon Boston", "hooray")
// error: Mixing named and positioned arguments not allowed
```
___

# Variable Number of Arguments

^ like in Java

We can define a parameter to accept a variable number of arguments `T`
- use the `vararg` keyword
- the `vararg` param is then treated as an array of type T
- default value must now be an array
___

# Variable Number of Arguments

^ imagine we want to print multiple exciting things
^ can mark the 2nd param with `vararg` to accept multiple inputs

```Kotlin
fun helloFunctions(exclamation:String, vararg excitingThings:String) {
  for(excitingThing in excitingThings) {
    println(exclamation + ", " + excitingThing)
  }
}

helloFunctions("yay!", "Droidcon Boston", "Kotlin", "Android")
// outputs:
// yay!, Droidcon Boston
// yay!, Kotlin
// yay!, Android
```
^ excitingThings is treated as an array or strings, so it can be iterated over

___

# Variable Number of Arguments

Typically, a `vararg` parameter will be the last one

Can be used in any order if:
- other parameters are called using named argument syntax
- last parameter is a function passed outside the parentheses

___

# Variable Number of Arguments

This works great

```Kotlin
helloFunctions("yay!", "Droidcon Boston", "Kotlin", "Android")
helloFunctions("Droidcon Boston", "Kotlin", "Android", exlamation = "yay!")

// both output:
// yay!, Droidcon Boston
// yay!, Kotlin
// yay!, Android
```

___

# Variable Number of Arguments

This works

^ but because no named arguments are used, the first item becomes the exclamation

```Kotlin
helloFunctions("Droidcon Boston",  "Kotlin", "Android")
// output:
// "Droidcon Boston, Kotlin"
// "Droidcon Boston, Android"

```

___

# Variable Number of Arguments

This won't compile

```Kotlin
helloFunctions("Droidcon Boston", exlamation = "yay!", "Kotlin", "Android")
// error: "no matching function"
```

^ can't find a match because of the missing of argument types

___


# Variable Number of Arguments

Use "spread" operator to pass an existing array of values

```Kotlin
val thingsToBeExcitedAbout = arrayOf("Droidcon Boston", "Kotlin", "Android")
helloFunctions("yay!", *thingsToBeExcitedAbout)

// output:
// yay!, Droidcon Boston
// yay!, Kotlin
// yay!, Android
```

---

# Variable Number of Arguments

"Spreading" can be used alone, or with other passed varargs as well

```Kotlin
helloFunctions("yay!", "coffee", *thingsToBeExcitedAbout)
helloFunctions("yay!", *thingsToBeExcitedAbout, "coffee")
```
- input array to the vararg parameter is handled in order

^ in first call here coffee will be first, and in the 2nd call it will be last

___

# Return Types

What is the return type?

```Kotlin
fun helloFunctions(exclamation:String, excitingThing:String="functions") {
  println(exclamation + ", " + excitingThing)
}
```
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

Functions with block body require explicit return type & call for non-Unit functions

```Kotlin
fun helloFunctions(exclamation:String, excitingThing:String="functions") : String {
  return exclamation + ", " + excitingThing
}
```
___

# Return A Non-Unit Type

Can infer return type for single-expression functions

```Kotlin
fun helloFunctions(exclamation:String, excitingThing:String="functions")
    = exclamation + ", " + excitingThing
```
___

# Generic Functions

Like classes, functions may have generic type parameters

^ many of the stdlib functions for collections are generic

```Kotlin
public inline fun <T> Iterable<T>.filter(predicate: (T) -> Boolean): List<T> {
    return filterTo(ArrayList<T>(), predicate)
}

public fun <T> Iterable<T>.toHashSet(): HashSet<T> {
    return toCollection(HashSet<T>(mapCapacity(collectionSizeOrDefault(12))))
}

listOf(2,4,6,8).filter{ ... }
setOf(2,4,6).toHashSet()
```

___

> concise
> convenient
> flexible

___

# What Next?

___

> Let's explore some variations on how you can create and use functions

___

# Variations In Scope

- Top-level
- Member functions
- Local
- CompanionObject
- Extension functions

___

# Top-Level functions

- Not tied to a class
- Defined within a Kotlin file
- Belong to their declared file's package
- Import to use within other packages

^ enable interesting changes in how we build our apps

___

# Top-Level Function Patterns
- Replace stateless classes filled with static methods
- Swap your "Util" or "Helper" classes with functions

^ great for functionality that is widely used
^ ex: threading helpers, loggers
^ possibly even fewer classes/objects to be dependent on

___

# Top-Level Function Considerations

- Not truly removing classes
- Generated as a public static method on a class using a special convention
- <function's file name>Kt.java

___

# Top-Level Function Considerations

__Inside Logging.kt__
<br>

```Kotlin
package logging

fun log(error:Throwable) {...}
```
___

# Top-Level Function Considerations

__Call from Kotlin__
<br>

```Kotlin
log(Throwable("oops"))
```

___

# Top-Level Function Considerations

__Generated Code__
<br>

```Java
public class LoggingKt {
  public static void log(Throwable error) {...}
}
```
___

# Top-Level Function Considerations

__Call from Java__
<br>

```Java
LoggingKt.log(new Throwable("oops"))
```

^ notice the name of the generated class

___

# Top-Level Function Considerations

Can override the generated class/file name

- Add `@file:JvmName(<desired class name>)` to function's file
- Must be before the declared package

___

# Top-Level Function Considerations

__Inside Logging.kt__
<br>

```Kotlin
@file:JvmName("LoggingFunctions")
package logging

fun log(error:Throwable) {...}
```

___

# Top-Level Function Considerations

__Call from Java__
<br>

```Java
LoggingFunctions.log(new Throwable("oops"))
```
___

# Top-Level Function Summary

- Function declared in a file outside of any class
- Can replace stateless helper/util classes
- Can override generated class name to improve Java interop

___

# Member Functions

- Function on a class or object
- Like a Java method
- Have access to private members of the class or object

___

# Member Functions

```Kotlin
class Speaker() {
    fun giveTalk() { ... }
}

// create instance of class Speaker and call giveTalk()
Speaker().giveTalk()
```

___

# Member Function Considerations

- Default arguments can't be changed in overridden methods
- If overriding a method, you must omit the default values

___

# Local Functions

Functions inside of functions

- Create a function that is scoped to another function
- Useful if your function is only ever called from another function

___

# Local Functions

Why would you want this?

- clean code
- avoids code duplication
- avoid deep chains of function calls

___

# Local Functions

- declare like any other function, just within a function
- have access to all params and variables of the enclosing function

___

# Local Functions

```Kotlin
fun parseAccount(response:AccountResponse) : Account {
  ...

  val hobbies = response.getField("hobbies").map{
    val key = it.getField("key")
    Hobby(key)
  }

  val favoriteFoods = response.getField("favorite_foods").map{
    val key = it.getField("key")
    Food(key)
  }
}
```

___

# Local Functions

```Kotlin
fun parseAccount(response:AccountResponse) : Account {
  fun parseKey(entity:ResponseEntity) = entity.getField("key")

  ...

  val hobbies = response.getField("hobbies").map{
    val key = parseKey(it)
    Hobby(key)
  }

  val favoriteFoods = response.getField("favorite_foods").map{
    val key = parseKey(it)
    Food(key)
  }
}
```

___

# Local Function Considerations

- local function or private method?
- is the logic going to be needed outside the current function?
- does the logic need to be tested in isolation?
- is the enclosing function still readable?

___

# Companion Objects

- no static method/functions in Kotlin
- recommended to use top-level functions instead
- but what if you need access to private members of an object?

___

# Companion Objects

- want to create a factory method?
- define a member function on a companion object to gain access to private members/constructors

___

# Companion Objects

```Kotlin
class Foo private constructor(val key:String)

// won't work
// can't access the private constructor
fun createFoo(key:String) : Foo {
    return Foo(key)
}
```

___

# Companion Objects

```Kotlin
class Goo private constructor(val key:String) {
    companion object {
        fun createGoo(key:String) : Goo {
            return Goo(key)
        }
    }
}

// can then call the factory method
Goo.createGoo("somekey")
```

___

# [fit] Special Cases

___

# Special Cases

- `infix`
- `extension`
- higher-order
- lambdas
- `inline`
- anonymous

___

# infix

- `infix` keyword enables usage of infix notation
- can omit the dot & parentheses for the function call

- ```Kotlin
"key" to "value"
```

^ the 'to' function used to return a Pair

___

# infix

- must be a member function or extension function

^ we will look at extension functions shortly

- must take a single, non-varargs, parameter with no default value

___

# infix

```Kotlin
class User{
    infix fun addNickname(name:String){...}
}

// call the function without dot or parentheses
val user = User()
user addNickname "shades"
```

___

# infix

- can provide a very clean, human-readable syntax
- core building block of custom DSLs

___

# Extension Functions

- extend the functionality of an existing class
- use as if it were a member of a class
- defined outside the class

___

# Extension Functions

- cleanup or extend classes & apis you don't control
- remove helper classes & simplify top-level functions
- can be leveraged for DSLs

___

# Extension Functions

```Kotlin
fun showToast(
  context: Context,
  msg:String,
  duration: Int = Toast.LENGTH_SHORT) {

  Toast.makeText(context, msg, duration).show()
}

showToast(context, "Toast!")
```
^ top-level function
^ requires a `Context` always be passed

___

# Extension Functions

```Kotlin
fun Context.showToast(
  msg: CharSequence,
  duration: Int = Toast.LENGTH_SHORT) {

  Toast.makeText(this, msg, duration).show()
}

context.showToast("Toast!")
```
^ extension function
^ `Context` is now the receiver and is called on the context
^ can be defined anywhere

___


# Extension Function Considerations
- how are these generated under the hood?
- how are these called from Java?

___

# Extension Function Considerations

- extension functions are static methods that accept the receiver object as it's first argument
- like with top-level functions the convention is to use <filename>Kt.<functionName>

- ```Java
ContextExtensionsKt.showToast(context, "Toast!");
```

___

# Higher-Order Functions

- functions that take, or return, other functions
- can be lambda or function reference
- many examples in the Kotlin standard library `apply`, `also`, `run`

___

# Higher-Order Functions

- allow very interesting Patterns
- can cleanup setup/teardown patterns such as shared prefs
- very helpful in dsls

___

# Higher-Order Functions

```Kotlin
val predicate = { number:Int -> number > 5 }
listOf(2,4,6,8).filter(predicate)
```

^ we pass the lambda val to the `filter` function on the list
___

# Higher-Order Functions

```Kotlin
fun filterTheList(value:Int) = value > 5
listOf(2,4,6,8).filter(::filterTheList)
```

^ can also pass an existing function

___

# Higher-Order Functions

if the last parameter of a function is a function, you can omit the parentheses

- ```Kotlin
listOf(2,4,6,8).filter{ number -> number > 5 }
```

^ in this case, the type of the

___

# Higher-Order Functions

```Kotlin
fun getScoreCalculator(level:Level) {
    when (level) {
        Level.EASY -> { state:ScoreState -> state.score * 10 }
        Level.HARD -> { state:ScoreState -> state.score * 5 * state.accuracy }
    }
}
```

^ can return functions as well
^ could be used as a factory to return strategy functions

___

# Higher-Order Function Performance

> "Using higher-order functions imposes certain runtime penalties"

- extra class created when using lambda
- if lambda captures variables, extra object created on each call
- how to solve?

# inline

- helps solve higher-order function performance hits
- body of the inlined function is substituted for invocations of the function

___

## inline

^ example from Kotlin in Action

```Kotlin
inline fun <T> synchronized(lock: Lock, action: () -> T): T {
    lock.lock()
    try {
        return action()
    }
    finally {
        lock.unlock()
    }
}

val l = Lock()
synchronized(l) {...}
```

___

## inline

```Kotlin
fun foo(l:Lock) {
  println("before")
  synchronized(l) {
    println("action")
  }
  println("after")
}
```

___

## inline

With `inline` the generated code is equivalent to this

```Kotlin
fun goo(l:Lock) {
  println("before")
  lock.lock()
  try {
      println("action")
  }
  finally {
      lock.unlock()
  }
  println("after")
}
```

^ notice how the body of the synchronized function has been written within the body of foo

^ more to be learned regarding the intrices of `inline`

___

# Android Reimagined

> These features enabled us to rethink how we build our apps

___

# Avoiding `if`

```Kotlin
if(foo != null) { ...}

foo?.let{}
```

___

# Avoiding `if`

```Kotlin
if(game.level == EASY)  { }
else if (game.level == NORMAL) {}
else if (game.level == HARD) {}

when(game.level){
  EASY -> {}
  NORMAL -> {}
  HARD -> {}
}
```
___

# Android Reimagined

## Safer Strategies

```Kotlin
fun doTheThingSafely(theThing:() -> Unit) {
    try {
      theThing()
    } catch(error:Throwable) {
      // handle error
    }
}
```

___

# Android Reimagined

## Upgrade Our Apis

can use extensions, default params, etc to cleanup common apis

- now seeing community supported examples of this
- ktx: https://github.com/android/android-ktx
- anko: https://github.com/Kotlin/anko

___

# Android Reimagined

## Android KTX

^ from the android ktx github page

```Kotlin
sharedPreferences.edit()
    .putString("key", "without ktx")
    .putBoolean("isLessBoilerplate", false)
    .apply()

sharedPreferences.edit {
  putString("key", "with ktx")
  putBoolean("isLessBoilerplate", true)
}
```
^ notice we dont have to call edit() or apply() anymore


# Android Reimagined

## Fewer Helpers to Pass Around

Can utilize top-level functions for globally available actions such as logging

- remove direct dependencies that must be shared
- encourages configuration
- can have nice testing benefits

___

# Android Reimagined

## Fewer Helpers to Pass Around

```Kotlin
object CustomLogger {
  fun log(msg:String) {...}
}
```

- traditional syntax
- requires mocking when testing
- extra class & nesting

___

# Android Reimagined

## Fewer Helpers to Pass Around

```Kotlin
fun log(msg:String) {...}
```

- more fluent syntax
- doesn't require mocking when testing
- avoids extra class
- encourages configuration

___

# Android Reimagined
## Building a DSL

???  dsl for parsing things from the Contentful sdk ???
___

# In Closing

> Kotlin functions provide flexibility & freedom in how you build your apps

___

# In Closing

- Easy to get started
- Can build your understanding and usage of functions over time
- Enables you to rethink how you build your applications

___

# [fit] Thanks For Coming

___

# Let's Connect

```kotlin
with("n8ebel").apply{
  Twitter
  .com
  Medium
  Instagram
  Facebook
}
```
