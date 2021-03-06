# ReSwift-Thunk

[![Build Status](https://img.shields.io/travis/ReSwift/ReSwift-Thunk/master.svg?style=flat-square)](https://travis-ci.org/ReSwift/ReSwift-Thunk) [![Code coverage status](https://img.shields.io/codecov/c/github/ReSwift/ReSwift-Thunk.svg?style=flat-square)](http://codecov.io/github/ReSwift/ReSwift-Thunk) [![CocoaPods Compatible](https://img.shields.io/cocoapods/v/ReSwift-Thunk.svg?style=flat-square)](https://cocoapods.org/pods/ReSwift-Thunk) [![Platform support](https://img.shields.io/badge/platform-ios%20%7C%20osx%20%7C%20tvos%20%7C%20watchos-lightgrey.svg?style=flat-square)](https://github.com/ReSwift/ReSwift-Thunk/blob/master/LICENSE.md) [![License MIT](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](https://github.com/ReSwift/ReSwift-Thunk/blob/master/LICENSE.md) [![Reviewed by Hound](https://img.shields.io/badge/Reviewed_by-Hound-8E64B0.svg?style=flat-square)](https://houndci.com)

**Supported Swift Versions:** Swift 4.1, Swift 4.2

When [ReSwift](https://github.com/ReSwift/ReSwift/) is a [Redux](https://github.com/reactjs/redux)-like implementation of the unidirectional data flow architecture in Swift, ReSwift-Thunk is like [redux-thunk](https://github.com/reduxjs/redux-thunk). 

## Why Use ReSwift-Thunk?

## Example

```swift
// First, you create the middleware, which needs to know the type of your `State`.
let thunksMiddleware: Middleware<MyState> = createThunksMiddleware()

// Note that it can perfectly live with other middleware in the chain.
let store = Store<MyState>(reducer: reducer, state: nil, middleware: [thunksMiddleware])

// A thunk represents an action that can perform side effects, access the current state of the store, and dispatch new actions, as if it were a ReSwift middleware.
let thunk = Thunk<MyState> { dispatch, getState in 
    if getState!.loading {
        return
    }
    dispatch(RequestStart())
    api.getSomething() { something in
        if something != nil {
            dispatch(RequestSuccess(something))
        } else {
            dispatch(RequestError())
        }
    }
}

// As the thunk type conforms to the `Action` protocol, you can dispatch it as usual, without having to implement an overload of the `dispatch` function inside the ReSwift library.
store.dispatch(thunk)

// Note that this action won't reach the reducers, instead, the thunks middleware will catch it and execute its body, producing the desired side effects.
```

## Installation

ReSwift-Thunk requires the [ReSwift](https://github.com/ReSwift/ReSwift/) base module.

### CocoaPods

You can install ReSwift-Thunk via CocoaPods by adding it to your `Podfile`:
```
use_frameworks!

source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '8.0'

pod 'ReSwift'
pod 'ReSwift-Thunk'
```

And run `pod install`.

### Carthage

You can install ReSwift-Thunk via [Carthage](https://github.com/Carthage/Carthage) by adding the following line to your `Cartfile`:

```
github "ReSwift/ReSwift-Thunk"
```

### Swift Package Manager

You can install ReSwift-Thunk via [Swift Package Manager](https://swift.org/package-manager/) by adding the following line to your `Package.swift`:

```swift
import PackageDescription

let package = Package(
    [...]
    dependencies: [
        .Package(url: "https://github.com/ReSwift/ReSwift-Thunk.git", majorVersion: XYZ)
    ]
)
```

## Checking out Source Code

After checking out the project run `pod install` to get the latest supported version of [SwiftLint](https://github.com/realm/SwiftLint), which we use to ensure a consistent style in the codebase.

## Contributing

You can find all the details on how to get started in the [Contributing Guide](/CONTRIBUTING.md).

## Credits

## License

ReSwift-Thunk Copyright (c) 2018 ReSwift Contributors. Distributed under the MIT License (MIT). See [LICENSE.md](/CONTRIBUTING.md).
