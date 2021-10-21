


# Avantis Android Guidelines

## Overview

* Architecture
* Code style
* Plugins

----

## Architecture
We using Architecture Component + UseCase by working through an end-to-end use case.

<img width="819" alt="Screen Shot 2564-10-21 at 16 52 39" src="https://user-images.githubusercontent.com/91863302/138255324-4d8df2d1-eeb6-4309-84eb-88e67fbdac5f.png">

### View Layer
* Activity
* Fragment

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

## Plugins

 ### [JSON To Kotlin Class ​(JsonToKotlinClass)](https://plugins.jetbrains.com/plugin/9960-json-to-kotlin-class-jsontokotlinclass-)

Plugin for Kotlin to convert Json String into Kotlin data class code quickly.

Fast use it with short cut key ALT + K on Windows or Option + K on Mac

<img width="819" alt="Screen Shot 2564-10-21 at 17 43 52" src="https://user-images.githubusercontent.com/91863302/138262441-47648798-f14d-46a9-a339-101576c0fdcf.png">
---

