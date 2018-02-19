slidenumbers: true
build-lists: true
footer: © @n8ebel, [Udacity Engineering](https://engineering.udacity.com/) 2018
slidenumbers: true


# [fit] Adopting Kotlin

_A case study in team buy-in and adoption_

——

![left, 200%](/Users/nate/Pictures/kotlin_logos/logo.png)

## What Is Kotlin?

- a programming language developed by JetBrains
- targets the JVM
- is 100% compatible with Java for Android development

—

[.build-lists: false]
## Where Is It Used?

- Android
- JVM
- Browser
- Backend
- iOS

^ a lot of support going into making Kotlin available as widely as possible

—

# [fit] Adoption at Udacity

—

## Production Today

![right](/Users/nate/Downloads/udacity_logo_white.jpg)

Have been using in production for over a year

Today, Kotlin is our primary development language for Android

—

## Why Invest In Kotlin?

- Our adoption process
- How are we using Kotlin today
- Tips for incorporating Kotlin into your project

—

# Why Kotlin?

—

[.autoscale:true]
> Kotlin provides a more enjoyable developer experience by allowing us to express our features & ideas using safer, more concise code. This, in turn, enables us to build a better product for our users

^ each member of our team would have a unique answer, but they’d all probably sound something like this

—

## Key Benefits

- Improved crash rate
- Reduction in lines of code written
- Decreased time spent in code review
- Renewed excitement around experimentation and innovation

—

## Ultimately, our goal is to provide our users with the best learning experience possible.

—-

# [fit] We believe Kotlin helps us do that.

—

# [fit] How Did We Start?

—

## Recognition of Pain Points

We started to notice patterns in our code reviews
<br>

- “we need to be consistent in our handling of `null`”
- “this code could be shortened using a more functional approach”

^ We didn’t just set out to use the “latest & greatest”
^ Our adoption was a pragmatic one

—

## Recognition of Pain Points

Having experimented with Kotlin outside Udacity, we knew the language could help with some of these issues

—

## Kotlin, Meet the Team

![right, 100%](/Users/nate/Downloads/512px-Android_robot.svg.png)

- built a small new feature
- create both a Java & Kotlin PR

<br>

- demonstrated that Kotlin could be easily integrated

^ the Kotlin version wasn’t merged, but it showed that we didn’t have to lose time by using the language
^ it also showed our existing tooling and build process didn’t have to be impacted

—

## Jumping Off Point

- Set out to migrate our Settings screen
<br>
- During testing, we looked closely for 2 things

<br>

- Stability issues?
- Impacts to development process?  

^ Settings was fairly small and isolated at the time

—

## Jumping Off Point

1. Usability issues: what impact did Kotlin have on crashes/bugs?
2. Development process: did Kotlin cause CI issues, slow down our build, or slow down feature development?

^ Any increase in bugs?
^ Any issues with build/ CI/ etc?

—

## Ship It

![left, 100%](https://cdn-images-1.medium.com/max/1280/1*U8STxSl0AHVzzcjx4majdA.png)

As expected, no significant issues found

Released to production

—

## Slow Down

At this point, we slowed down a bit. 

We loved using Kotlin, but recognized the potential risks of going all-in on an unofficially supported language. 

We continued to add/convert some tests to Kotlin, but no new feature code was using it

—

# [fit] **Game Changer**

—

## Google I/O

![left, 175%](/Users/nate/Downloads/android-and-kotlin.png)

The Google I/O announcement of official support for Kotlin was the push we needed

We decided immediately that we wanted to go all-in on Kotlin

—

## Team Buy In

Met with our PM and expressed our desire/plan to adopt Kotlin. 

We were met with a healthy dose of pragmatism.

—

## “What’s the value prop?”

- Is the language stable/safe to be using now?
- Will it slow down development?
- Are there tangible benefits?

^ having already answered these questions, we were able to easily his concerns

—

# [fit] Migration Plan

—

## Migration Plan

1. All new dev work in Kotlin
2. If anything larger than a small bug fix must be done to a class, consider migrating the class to Kotlin
3. Start migrating existing code

—

## Migration Plan

Planned to tackle the low hanging fruit first (utilities, helpers, isolated classes) 

Work towards migrating enough code that the majority of our daily development would be in Kotlin

—

## Migration Process

- Started by using the Java to Kotlin conversion tool within Android Studio

- Then made manual adjustments to the converted code

—-

## Migration Process

Some of the adjustments we made to converted code:

- Avoiding the use of !! operator
- When possible, convert helper methods to top-level functions
- Avoid companion object where possible
- Reorganize the generated code
- Expressing code in a more Kotlin idiomatic way

—

## Handling `null`

In many places we focused on leveraging statements such as 

```kotlin
object?.let {...}
``` 

instead of 

```java
if(object != null) { ... }
```

^ One of the largest (and most valuable) migration task was handling or `null`

—-

## `stdlib`

Tried to leverage the great collections stdlib that Kotlin provides. 

Allowed us to replace large blocks of code with a few lines of concise functional code

—

## Shorter, safer code

```kotlin
val recentQueries:List<String?>? = listOf()
val recentsToDisplay = recentQueries
        ?.filterNotNull()
        ?.filter{ it.isNotBlank() }
        ?.take(5)
        ?: listOf()
```

—

# [fit] Where Are We Today?

—

## Flagship App

Our flagship codebase continues to be migrated to Kotlin

- ~40% Kotlin today
- All new dev work is done in Kotlin

—

## New Codebase

Additional code base that is 100% Kotlin

- Allowed us to fully explore the language
- Have began using several language features extensively

—

## New Codebase

Began leveraging more interesting aspects of the language

- data classes
- sealed classes
- named arguments & default parameter values
- higher order functions 

—

# [fit] Tips for Incorporating Kotlin

—

## Tips for Incorporating Kotlin

- If new to the language, start with the conversion tool
- Don’t be afraid to further modify the converted code

—

## Tips for Incorporating Kotlin

Start with tests
- can help work out build issues
- explore basic syntax
- great for understanding interop story

Features
- writing feature code will give a more comprehensive picture of how it can affect your code

—

## Tips for Incorporating Kotlin

Don’t go wild trying to write “idiomatic” Kotlin. 
- As you progress with the language, it’s likely your opinion of whats readable vs what’s possible will evolve

—

> “Just because you can doesn’t mean you should”

—

## Tips for Incorporating Kotlin

- As you migrate existing code, re-visit previously converted code from time to time. You may find that newly discovered conventions/patterns could be applied.
- Don’t forget to thoroughly test any interop layers between Java and Kotlin. Nullability issues can crop up during runtime when dealing with nullable platform types.

—

> “Explore, experiment, migrate, refactor”

—

## How Can Kotlin Improve Your Product?

take advantage of this period of exploration while learning the language

—

## How Can Kotlin Improve Your Product?

Question existing patterns/conventions for writing Android apps and ask yourself if/how Kotlin might enable you to write alternative solutions

—

## How Can Kotlin Improve Your Product?

- can your code be refactored to avoid null properties?
- can you replace helper classes/methods with top-level functions?
- can you avoid handling null properties by using a delegate?
- could a logical path be expressed using functional concepts to reduce a class’s state?

—

# [fit] Moving Forward

—

## Confident Moving Forward

We feel great about our investment into Kotlin

- Google continues to poor resources into Kotlin
- Samples now defaulting to Kotlin
- New ktx library for Android
- Increased interest from users will accelerate improvements

—

## More From Udacity

**Free Course**
- [Kotlin for Android Developers](https://www.udacity.com/course/kotlin-for-android-developers--ud888)

**Engineering Blog Posts***
- [Adopting Kotlin](https://engineering.udacity.com/adopting-kotlin-c12f10fd85d1)
- [Learning Kotlin by Mistake](https://engineering.udacity.com/learning-kotlin-by-mistake-b99304b7d724)
- [Modeling ViewModel States Using Kotlin’s Sealed Classes](https://engineering.udacity.com/modeling-viewmodel-states-using-kotlins-sealed-classes-a5d415ed87a7)
