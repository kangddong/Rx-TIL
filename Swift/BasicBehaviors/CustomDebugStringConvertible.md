
A type with a customized textual representation suitable for debugging purposes.

```swift
protocol CustomDebugStringConvertible
```


Swift provides a default debugging textual representation for any type. That default representation is used by the `String(reflecting:)` initializer and the `debugPrint(_:)` function for types that don’t provide their own. To customize that representation, make your type conform to the `CustomDebugStringConvertible` protocol.

Because the `String(reflecting:)` initializer works for instances of _any_ type, returning an instance’s `debugDescription` if the value passed conforms to `CustomDebugStringConvertible`, accessing a type’s `debugDescription` property directly or using `CustomDebugStringConvertible` as a generic constraint is discouraged.

스위프트는 모든 유형에 대한 기본 디버깅 텍스트 표현을 제공합니다. 그 기본 표현은 String(reflecting:) 이니셜라이저와 debugPrint(_:) 함수에서 자체를 제공하지 않는 유형에 사용됩니다. 그 표현을 사용자 정의하려면, 당신의 유형이 CustomDebugStringConvertible 프로토콜을 준수하도록 하세요.

String(reflecting:) 이니셜라이저는 모든 유형의 인스턴스에서 작동하기 때문에, 전달된 값이 CustomDebugStringConvertible을 준수하는 경우 인스턴스의 debugDescription을 반환하고, 유형의 debugDescription 속성에 직접 액세스하거나 CustomDebugStringConvertible을 일반 제약 조건으로 사용하는 것은 권장되지 않습니다.

Calling the `dump(_:_:_:_:)` function and printing in the debugger uses both `String(reflecting:)` and `Mirror(reflecting:)` to collect information about an instance. If you implement `CustomDebugStringConvertible` conformance for your custom type, you may want to consider providing a custom mirror by implementing `CustomReflectable` conformance, as well.

디버거에서 덤프(_:_:_:_:_:) 함수를 호출하고 인쇄하는 것은 String(reflecting:)와 Mirror(reflecting:)를 모두 사용하여 인스턴스에 대한 정보를 수집합니다. 사용자 지정 유형에 대해 CustomDebugStringConvertible 적합성을 구현하는 경우, CustomReflectable 적합성을 구현하여 사용자 지정 미러를 제공하는 것을 고려할 수도 있습니다.
# Conforming to the CustomDebugStringConvertible Protocol

Add `CustomDebugStringConvertible` conformance to your custom types by defining a `debugDescription` property.

For example, this custom `Point` struct uses the default representation supplied by the standard library:

debugDescription 속성을 정의하여 사용자 지정 유형에 CustomDebugStringConvertible 적합성을 추가하십시오.

예를 들어, 이 사용자 지정 포인트 구조체는 표준 라이브러리에서 제공하는 기본 표현을 사용합니다.

``` swift
struct Point {
    let x: Int, y: Int
}


let p = Point(x: 21, y: 30)
print(String(reflecting: p))
// Prints "Point(x: 21, y: 30)"
```

After adding `CustomDebugStringConvertible` conformance by implementing the `debugDescription` property, `Point` provides its own custom debugging representation.

debugDescription 속성을 구현하여 CustomDebugStringConvertible 적합성을 추가한 후, Point는 자체 사용자 지정 디버깅 표현을 제공합니다.

``` swift
extension Point: CustomDebugStringConvertible {
    var debugDescription: String {
        return "(\(x), \(y))"
    }
}


print(String(reflecting: p))
// Prints "(21, 30)"
```


## 출처

[애플 공식 문서](https://developer.apple.com/documentation/swift/customdebugstringconvertible)