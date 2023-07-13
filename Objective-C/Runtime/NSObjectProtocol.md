
```swift
protocol NSObjectProtocol
```

모든 Objective-C 객체의 기본인 methods 그룹.
이 프로토콜은 NSObjectProtocol이라는 이름으로 Swift로 가져옵니다.

To conform to the `NSObjectProtocol`, a Swift class needs to explicitly declare its conformance by inheriting from the `NSObject` class or stating conformance to the protocol itself, like so:

`NSObjectProtocol`을 준수하려면 Swift 클래스는 `NSObject` 클래스를 상속하거나 프로토콜 자체에 대한 적합성을 명시적으로 선언해야 합니다

이 프로토콜을 준수하는 객체는 일급 객체로 간주될 수 있다. 

그러한 object는 그것에 대해 물어볼 수 있다:
* 클래스, 그리고 상속 계층 구조에서 클래스의 위치.
* 프로토콜 준수.
* 특정 메시지에 응답하는 능력.

Cocoa root class `NSObject`는 이 프로토콜을 채택하므로, NSObject에서 상속된 모든 객체는 이 프로토콜에 설명된 기능을 가지고 있습니다.