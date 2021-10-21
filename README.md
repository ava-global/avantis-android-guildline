

# Avantis Android Guidelines

## Overview

* Architecture
* Code style
* Plugins

----

## Architecture
We using Architecture Component + UseCase by working through an end-to-end use case.

<img width="819" alt="Screen Shot 2564-10-21 at 16 52 39" src="https://user-images.githubusercontent.com/91863302/138255324-4d8df2d1-eeb6-4309-84eb-88e67fbdac5f.png">

### Repository

<img width="980" alt="Screen Shot 2564-10-21 at 17 32 12" src="https://user-images.githubusercontent.com/91863302/138260930-26bbfb84-f7f4-4a0a-a581-55f93018cc29.png">

```
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

Ref : [android ViewBinding](https://developer.android.com/topic/libraries/view-binding)

---
