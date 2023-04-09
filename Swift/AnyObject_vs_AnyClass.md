
# AnyObject vs AnyClass

AnyObject와 AnyClass는 모양새가 비슷하여 유독 헷갈리는 내용이다

그렇기에 각각의 특징을 알아보고 차이점에 대해서 작성해볼려고한다

# AnyObject
모든 클래스가 암시적으로 준수하는 프로토콜.

입력되지 않은 객체의 유연성이 필요하거나 입력되지 않은 결과를 반환하는 브리지된 Objective-C 메서드와 속성을 사용할 때 AnyObject를 사용합니다. AnyObject는 모든 클래스, 클래스 유형 또는 클래스 전용 프로토콜의 인스턴스의 구체적인 유형으로 사용할 수 있습니다.
예를 들어:
```swift
class FloatRef {
	let value: Float
	init(_ value: Float) {
		self.value = value
	}
}

let x = FloatRef(2.3)
let y: AnyObject = x
let z: AnyObject = FloatRef.self
```

AnyObject는 Objective-C 클래스에 연결되는 유형의 인스턴스의 구체적인 유형으로도 사용될 수 있습니다. String 및 Int와 같은 Objective-C 대응에 대한 Swift 브리지의 많은 값 유형.
```swift
let s: AnyObject = "This is a bridged string." as NSString
print(s is NSString)
// Prints "true"

let v: AnyObject = 100 as NSNumber
print(type(of: v))
// Prints "__NSCFNumber"
```

AnyObject 프로토콜의 유연한 동작은 Objective-C의 ID 유형과 유사하다. 이러한 이유로, 가져온 Objective-C 유형은 AnyObject를 속성, 메서드 매개 변수 및 반환 값의 유형으로 자주 사용합니다.

AnyObject의 구체적인 유형을 가진 객체는 특정 동적 유형을 유지하며 유형 캐스트 연산자 중 하나를 사용하여 해당 유형으로 캐스팅할 수 있습니다(as, as? 또는 as!).

이 예제는 조건부 다운캐스트 연산자를 사용합니다 (as?) 위에서 선언된 s 상수를 스위프트의 문자열 유형의 인스턴스로 조건부로 캐스팅합니다.

AnyObject 인스턴스에 특정 유형이 있다는 사전 지식이 있다면, 무조건 다운캐스트 연산자를 사용할 수 있습니다(as!). 잘못된 캐스트를 수행하면 런타임 오류가 발생합니다.

캐스팅은 스위치 진술의 맥락에서 항상 안전하다.

AnyObject를 구체적인 유형으로 사용할 때, 모든 @objc 메서드와 속성, 즉 Objective-C에서 가져오거나 @objc 속성으로 표시된 메서드와 속성을 사용할 수 있습니다. Swift는 컴파일 타임에 이러한 메서드와 속성이 AnyObject 인스턴스의 기본 유형에서 실제로 사용할 수 있다는 것을 보장할 수 없기 때문에, 이러한 @objc 기호는 각각 암시적으로 래핑되지 않은 선택적 메서드와 속성으로 사용할 수 있습니다.

이 예제는 getIntegerValue()라는 @objc 메서드를 사용하여 IntegerRef 유형을 정의합니다.

이 예에서, obj는 AnyObject의 정적 유형과 IntegerRef의 동적 유형을 가지고 있다. 선택적 체인을 사용하여 obj에서 @objc 메소드 getIntegerValue()를 안전하게 호출할 수 있습니다. Obj의 동적 유형을 확신한다면, getIntegerValue()를 직접 호출할 수 있습니다.

Obj의 동적 유형이 getIntegerValue() 메서드를 구현하지 않으면, 시스템은 certainValue를 초기화할 때 런타임 오류를 반환합니다.

또는, obj.getIntegerValue()가 존재하는지 테스트해야 하는 경우, 메소드를 호출하기 전에 선택적 바인딩을 사용하세요.

# AnyClass
모든 클래스 유형이 암시적으로 준수하는 프로토콜.

AnyClass 프로토콜을 모든 클래스의 인스턴스의 구체적인 유형으로 사용할 수 있습니다. 그렇게 할 때, 알려진 모든 @objc 클래스 메서드와 속성은 각각 암시적으로 래핑되지 않은 선택적 메서드와 속성으로 사용할 수 있습니다. 예를 들어:

```swift
class IntegerRef {
	@objc class func getDefaultValue() -> Int {
		return 42
	}
}

func getDefaultValue(_ c: AnyClass) -> Int? {
	return c.getDefaultValue?()
}
```

`getDefaultValue(_:)` 함수는 선택적 체인을 사용하여 c에서 암시적으로 래핑되지 않은 클래스 메서드를 안전하게 호출합니다. 다른 클래스 유형으로 함수를 호출하는 것은 `getDefaultValue()` 클래스 메소드가 조건부로만 사용할 수 있는 방법을 보여줍니다.

```swift
print(getDefaultValue(IntegerRef.self))
// Prints "Optional(42)"

print(getDefaultValue(NSString.self))
// Prints "nil"
```
