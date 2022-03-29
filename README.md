



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
#### String
String names start with a prefix that identifies the section they belong to. We use `**<HOW>_<DESCRIPTION>**` for strings naming. `<HOW>` to indicate reason of the string will be used & `description` give any extra information.
| Description | Usage |Prefix | Example |
|--|--| --|--|
| "Trade" | Title, SubTitle , Message, Description |`label_` | `<string name="label_trade">Trade</string>`
| "Trade" | Button, Action, Menu |`action_` | `<string name="action_trade">Trade</string>`
| "Enter password" | Hint |`hint_` | `<string name="hint_password">Enter password</string>`
| "Password invalid" | Error |`error_` | `<string name="error_password_invalid">Password invalid. Please try again.</string>`

#### Drawable

`<WHAT>_<WHERE>`
For `feature/xxxx`
| Asset Type | Prefix | Example |
|--|--| --|
| Background | `bg_` | `bg_profile.xml`, `bg_button_trade.xml`

`<WHAT>_<DESCRIPTION_1>_<DESCRIPTION_2>_<DESCRIPTION_999>_<SIZE>`
For `share/design` 

| Asset Type | Prefix | Example |
|--|--| --|
| Background, Shape | `bg_` | `bg_white_circle.xml` , `bg_white_circle_stroke_red.xml` , `bg_white_stroke_2_red.xml`,`bg_white_corner_5_stroke_2_red.xml`, `bg_gradient_red_green_yellow.xml`
| Selector| `selector_`| `selector_button_login.xml`
| Ripple | `ripple_`| `ripple_button_login.xml`
| Divider | `divider_`| `divider_green.xml` ,`divider_dash_green.xml` 


Naming conventions for icons (taken from [Android iconography guidelines](http://developer.android.com/design/style/iconography.html)):
Add in `/share/design`
|Asset Type| Prefix | Example |
|--|--|--|
| Icons | `ic_`  | `ic_home.png` |
|Menu icons|`ic_menu_`|`ic_menu_notification.png`|

If you need to change icon color use `android:tint=`

#### Layout
Layouts are relatively simple, as there usually are only a few layouts per screen.
`<WHAT>_<WHERE>.xml`
 
| Component | Class Name | Layout Name | Usage |
|--|--| --|--|
| Activity | `ProfileActivity` | `activity_profile.xml` | content view for activity
| Fragment| `ProfileFragment`| `fragment_profile.xml` | view for a fragment
| Dialog| `ErrorDialog`| `dialog_error.xml` | view for dialog, dialog fragment
| BottomSheet | `FilterBottomSheetDialog`|`bottomsheet_filter.xml`| view for a Bottomsheet dialog fragment
|Widget or CustomView| `ProfileView` | `view_profile.xml` | inflated by a custom view
|Layout | - | `layout_login.xml` | layout reused using the include tag
|Item| - | `item_article.xml` | layout used in list/recycler/gridview

#### Variable 
| Description | suffix | Example | Note |
|--|--| --|--|
| User list, Users | `List` | `userList`
|For data class if object `{}`| `Data` | `UserData` | set `var` & nullable field & initial by null `var contentID: String? = null,`

#### Constant

```
//For Public Constant, Type, Create `annotation class`
@Retention(AnnotationRetention.SOURCE)  
annotation class PinStatus {  
    companion object {  
        const val RESET = "RESET"  
  const val SET = "SET"  
  const val NORMAL = "NORMAL"  
  }  
}
```

```
//For Private Constant, Create constant

private const val DISPLAY_TYPE = "DISPLAY_TYPE" // <-- on top class name
class XXXXX {
...
}
``` 
```
//For Actions Constant create `object`
object Demo {  
    const val ACTION = "action.demo.open"  
}
```

## Plugins

 ### [JSON To Kotlin Class ​(JsonToKotlinClass)](https://plugins.jetbrains.com/plugin/9960-json-to-kotlin-class-jsontokotlinclass-)

Plugin for Kotlin to convert Json String into Kotlin data class code quickly.

Fast use it with short cut key ALT + K on Windows or Option + K on Mac

<img width="819" alt="Screen Shot 2564-10-21 at 17 43 52" src="https://user-images.githubusercontent.com/91863302/138262441-47648798-f14d-46a9-a339-101576c0fdcf.png">
---

