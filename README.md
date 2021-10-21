



# Avantis Android Guidelines

## Overview

* Architecture
* Code style
* Plugins

----
## Language
Android development using [Kotlin](https://developer.android.com/kotlin)

## Architecture
We using Architecture Component + UseCase by working through an end-to-end use case.

<img width="819" alt="Screen Shot 2564-10-21 at 16 52 39" src="https://user-images.githubusercontent.com/91863302/138255324-4d8df2d1-eeb6-4309-84eb-88e67fbdac5f.png">

### View Layer
* Activity
* Fragment
* ViewModel

### Domain Layer
* UseCase
* CoroutineUseCase

### Data Layer
* Model
* Repository
* Remote
* Local
* Service

#### Repository

<img width="980" alt="Screen Shot 2564-10-21 at 17 32 12" src="https://user-images.githubusercontent.com/91863302/138260930-26bbfb84-f7f4-4a0a-a581-55f93018cc29.png">

```
//NetworkBoundResource
val dbSource = loadFromDb()  
val shouldFetch = shouldFetch(dbSource)  
if (shouldFetch) {  
    fetchFromNetwork(dbSource)  
} else {  
    return ResultResponse.Success(dbSource)  
}
```

---
### Dependencies Injection
* [Koin](https://insert-koin.io/) 
A pragmatic and lightweight dependency injection framework for Kotlin developers

###  [Kotlin coroutines on Android](https://developer.android.com/kotlin/coroutines)
Coroutines is our recommended solution for asynchronous programming on Android. Noteworthy features include the following:

-   **Lightweight**: You can run many coroutines on a single thread due to support for  [_suspension_](https://kotlinlang.org/docs/reference/coroutines/basics.html), which doesn't block the thread where the coroutine is running. Suspending saves memory over blocking while supporting many concurrent operations.
-   **Fewer memory leaks**: Use  [_structured concurrency_](https://kotlinlang.org/docs/reference/coroutines/basics.html#structured-concurrency)  to run operations within a scope.
-   **Built-in cancellation support**:  [Cancellation](https://kotlinlang.org/docs/reference/coroutines/cancellation-and-timeouts.html)  is propagated automatically through the running coroutine hierarchy.
-   **Jetpack integration**: Many Jetpack libraries include  [extensions](https://developer.android.com/kotlin/ktx)  that provide full coroutines support. Some libraries also provide their own  [coroutine scope](https://developer.android.com/topic/libraries/architecture/coroutines)  that you can use for structured concurrency.
---
### View Binding
View binding  is a feature that allows you to more easily write code that interacts with views. Once view binding is enabled in a module, it generates a  _binding class_  for each XML layout file present in that module. An instance of a binding class contains direct references to all views that have an ID in the corresponding layout.

In most cases, view binding replaces  `findViewById`.
```
android {
  ... 
  buildFeatures {
   viewBinding true
  }  
}
```
Note : We not use data binding

Ref : [Android ViewBinding](https://developer.android.com/topic/libraries/view-binding)

---
## Code style

#### Resources 
Resources file names are written in **lowercase_underscore**.
![Screen Shot 2564-10-21 at 18 45 24](https://user-images.githubusercontent.com/91863302/138270711-f3c2c9e9-ffb0-4799-8b6b-5293e56ec21e.png)
Ref : [cheat sheet](https://jeroenmols.com/blog/2016/03/07/resourcenaming/)

##### Drawable


| Asset Type | Prefix | Example |
|--|--| --|
| Background | `bg_` | `bg_circle_white.xml`
| Selector| `selector_`| `selector_button_login.xml`
| Ripple | `ripple_`| `ripple_button_login.xml`
| Circke||


Naming conventions for icons (taken from [Android iconography guidelines](http://developer.android.com/design/style/iconography.html)):
|Asset Type| Prefix | Example |
|--|--|--|
| Icons | `ic_`  | `ic_home.png` |
|Menu icons|`ic_menu_`|`ic_menu_notification.png`|


##### Layout
Layouts are relatively simple, as there usually are only a few layouts per screen.
`<WHAT>_<WHERE>.xml`
 
| Component | Class Name | Layout Name |
|--|--| --|
| Activity | `ProfileActivity` | `activity_profile.xml`
| Fragment| `ProfileFragment`| `fragment_profile.xml`
| Dialog| `ErrorDialog`| `dialog_error.xml`
|Widget or CustomView| `ProfileView` | `view_profile.xml`
|Layout | - | `layout_login.xml`
|Item| - | `item_article.xml`

##### Strings


## Plugins

 ### [JSON To Kotlin Class ​(JsonToKotlinClass)](https://plugins.jetbrains.com/plugin/9960-json-to-kotlin-class-jsontokotlinclass-)

Plugin for Kotlin to convert Json String into Kotlin data class code quickly.

Fast use it with short cut key ALT + K on Windows or Option + K on Mac

<img width="819" alt="Screen Shot 2564-10-21 at 17 43 52" src="https://user-images.githubusercontent.com/91863302/138262441-47648798-f14d-46a9-a339-101576c0fdcf.png">
---

