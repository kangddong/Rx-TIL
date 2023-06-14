정수 해시 값을 생성하기 위해 `Hasher` 로 해시될 수 있는 유형입니다 .

```swift
protocol Hashable : Equatable
```

# Overview

<details><summary> 공식문서 번역 보기 </summary>
<p>

`Hashable` 프로토콜을 준수하는 어떤 타입이든 `Set`나 `dictionary key`로 사용할 수 있습니다. 
표준 라이브러리의 많은 타입이 `Hashable`을 준수합니다. `String`, `Int`, `floating-point` 및 `Boolean value`, 심지어 기본적으로 `Sets`도 해시 가능합니다. 
일부 다른 타입, 예를 들어 옵셔널, 배열 및 ranges는 타입 인수가 동일한 경우 자동으로 해시 가능해집니다.

사용자 정의 타입도 해시 가능합니다. `associated values`이 없는 `enumeration`을 정의하면 자동으로 `Hashable` 준수를 얻을 수 있으며, 모든 사용자 정의 타입에 대해 `hash(into:)` 메서드를 구현하여 `Hashable` 준수를 추가할 수 있습니다. 저장된 속성이 모두 `Hashable`인 구조체와 모든 `associated values`을 가진 `enum type`의 경우, 컴파일러는 자동으로 `hash(into:)` 구현을 제공할 수 있습니다.

값을 `Hashing`한다는 것은 `hash` 함수에 해당하는 `Hasher` 타입으로 핵심 구성 요소를 공급하는 것을 의미합니다. 핵심 구성 요소는 `Equatable`  타입의  구현에 기여하는 요소입니다. 
동일한 값을 가진 두 인스턴스는 `hash(into:)`에서 `Hasher`에 동일한 값을 동일한 순서로 공급해야합니다.

# Conforming to the Hashable Protocol  

To customize your type’s `Hashable` conformance, to adopt `Hashable` in a type that doesn’t meet the criteria listed above, or to extend an existing type to conform to `Hashable`, implement the `hash(into:)` method in your custom type.

집합 또는 사전의 키 타입으로 사용자 정의 타입을 사용하려면 타입에 `Hashable` 준수를 추가하세요. `Hashable` 프로토콜은 `Equatable` 프로토콜을 상속하므로 `Equatable`의 요구 사항도 충족해야 합니다.

사용자 정의 타입이 `Hashable`을 준수하고, 타입의 원래 선언에서 `Hashable` 준수를 선언하며 해당 타입이 다음 기준을 충족하는 경우, 컴파일러는 자동으로 `Hashable` 및 요구 사항을 `synthesizes`합니다.

- `struct`의 경우 모든 저장 프로퍼티가 `Hashable`을 준수해야 합니다. 
- `enum`의 경우 모든 연관 값을 `Hashable`을 준수해야 합니다. (연관 값이 없는 enum의 경우 선언 없이도 `Hashable` 준수가 됩니다.)

사용자 정의 타입의 Hashable 준수 사용자 정의하거나 위에 나열된 기준을 충족하지 않는 타입에 `Hashable을` 적용하거나 기존 타입을 확장하여 `Hashable`을 준수하도록 구현하려면 사용자 정의 타입의 `hash(into:)` 메서드를 구현하세요.

hash(into:) 구현에서는 제공된 Hasher 인스턴스에서 타입의 핵심 구성 요소를 사용하여 combine(_:)을 호출하세요. Hashable 및 Equatable 프로토콜의 의미적 요구 사항을 충족하는지 확인하기 위해 타입의 Equatable 준수도 맞춤 설정하는 것이 좋습니다.

예를 들어, 버튼 그리드에서 위치를 설명하는 GridPoint 타입을 고려해 보겠습니다. 여기 GridPoint 타입의 초기 선언이 있습니다:

``` swift
/// A point in an x-y coordinate system.
struct GridPoint {
    var x: Int
    var y: Int
}
```

You’d like to create a set of the grid points where a user has already tapped. Because the `GridPoint` type is not hashable yet, it can’t be used in a set. To add `Hashable` conformance, provide an `==` operator function and implement the `hash(into:)` method.

``` swift
extension GridPoint: Hashable {
    static func == (lhs: GridPoint, rhs: GridPoint) -> Bool {
        return lhs.x == rhs.x && lhs.y == rhs.y
    }


    func hash(into hasher: inout Hasher) {
        hasher.combine(x)
        hasher.combine(y)
    }
}
```

The `hash(into:)` method in this example feeds the grid point’s `x` and `y` properties into the provided hasher. These properties are the same ones used to test for equality in the `==` operator function.

Now that `GridPoint` conforms to the `Hashable` protocol, you can create a set of previously tapped grid points.

``` swift
var tappedPoints: Set = [GridPoint(x: 2, y: 3), GridPoint(x: 4, y: 1)]
let nextTap = GridPoint(x: 0, y: 1)
if tappedPoints.contains(nextTap) {
    print("Already tapped at (\(nextTap.x), \(nextTap.y)).")
} else {
    tappedPoints.insert(nextTap)
    print("New tap detected at (\(nextTap.x), \(nextTap.y)).")
}
// Prints "New tap detected at (0, 1).")
```

</p>
</details>



# Example

```swift
struct ScoreInfo: Codable, Hashable {
    /// 평가 항목 시퀀스
    let scoreItemNo: Int
    /// 평점
    let score: Float

    init(scoreItemNo: Int, score: Float) {

        self.scoreItemNo = scoreItemNo
        self.score = score

    }

    func hash(into hasher: inout Hasher) {

        hasher.combine(scoreItemNo)
    }
```
<details><summary> lhs와 rhs의 의미에 대해 궁금한 사람 눌러주세요 </summary>
우선 수학 방정식(equation), 비방정식(inequation), 부등식(inequality) 에서 사용되는 용어이며
lhs(left-hand side), rhs(right-hand-side)이다.
 
`func ==` 는 메소드의 명이 == , 즉 상등(equality)을 뜻하기에 
한국어로 익숙한 좌변(lhs)과 우변(rhs)으로 말할 수 있다.

좌변은 다른 변수값을 지정하여 저장할 변수(기존에 있던 변수)를,
우변은 다른 변수에 저장될 변수값에 해당하는 변수(upsert되는 변수)이다

</details>
    
```swift

    static func == (lhs: ScoreInfo, rhs: ScoreInfo) -> Bool {
		// lhs, rhs 비교시 scoreItemNo 같으면 같은 Hash라고 생각해서 중복 허용안함
        return lhs.scoreItemNo == rhs.scoreItemNo

    }
}

var info: Set<ScoreInfo> = []
let scoreInfo1 = ScoreInfo(scoreItemNo: 0, scroe: 3.0)
let scoreInfo2 = ScoreInfo(scoreItemNo: 0, scroe: 3.0)
let scoreInfo3 = ScoreInfo(scoreItemNo: 0, scroe: 4.0)

info.insert(scoreInfo1) // [scoreInfo1]
info.insert(scoreInfo2) // [scoreInfo1]
info.insert(scoreInfo3) // [scoreInfo1]

scoreItemNo는 유지하고, score의 변동사항만 바꾸고싶다면

info.update(scoreInfo1) // [scoreInfo1]
info.update(scoreInfo2) // [scoreInfo1]
info.update(scoreInfo3) // [scoreInfo1, scoreInfo3]
```



참고
https://dawoum.ddns.net/wiki/Sides_of_an_equation
[Apple Document Hashable](https://developer.apple.com/documentation/swift/hashable/hash(into:)-v52)
[Apple Document Equatable](https://developer.apple.com/documentation/swift/equatable)
[위키](https://en.wikipedia.org/wiki/Sides_of_an_equation)
https://alohalimi.tistory.com/entry/SWIFT-%EC%97%B0%EC%82%B0%EC%9E%90%EC%97%90%EC%84%9C-%EC%95%8C%EC%95%84%EB%91%AC%EC%95%BC-%ED%95%A0%EA%B2%83Operator