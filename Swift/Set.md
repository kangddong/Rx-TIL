

## Set 집합 관련 메소드

- intersection - 교집합

```swift
func intersection(_ other: Set<Element>) -> Set<Element>

let employees: Set = ["Alicia", "Bethany", "Chris", "Diana", "Eric"]
let neighbors: Set = ["Bethany", "Eric", "Forlani", "Greta"]
let bothNeighborsAndEmployees = employees.intersection(neighbors)
print(bothNeighborsAndEmployees)
// Prints "["Bethany", "Eric"]"
```

- union - 합집합

```swift
func union<S>(_ other: S) -> Set<Element> where Element == S.Element, S : Sequence

let attendees: Set = ["Alicia", "Bethany", "Diana"]
let visitors = ["Marcia", "Nathaniel"]
let attendeesAndVisitors = attendees.union(visitors)
print(attendeesAndVisitors)
// Prints "["Diana", "Nathaniel", "Bethany", "Alicia", "Marcia"]"

// Set에 이미 다른 요소에 있는 하나 이상의 요소가 포함되어 있다면, 기존 멤버는 유지됩니다.
// 다른 것에 동등한 요소의 여러 인스턴스가 포함되어 있다면, 첫 번째 인스턴스만 보관됩니다.
let initialIndices = Set(0..<5)
let expandedIndices = initialIndices.union([2, 3, 6, 6, 7, 7])
print(expandedIndices)
// Prints "[2, 4, 6, 7, 0, 1, 3]"
```

- subtracting - 차집합

```swift
func subtracting(_ other: Set<Element>) -> Set<Element>

var employees: Set = ["Alicia", "Bethany", "Chris", "Diana", "Eric"]
let neighbors = ["Bethany", "Eric", "Forlani", "Greta"]
employees.subtract(neighbors)
print(employees)
// Prints "["Chris", "Diana", "Alicia"]"
```

## 참고

[애플 공식문서 - intersection(\__:)](https://developer.apple.com/documentation/swift/set/intersection(_:)-1zh8f)
[애플 공식문서 - union(\__:)](https://developer.apple.com/documentation/swift/set/union(_:))
[애플 공식문서 - subtract( :)](https://developer.apple.com/documentation/swift/set/subtract(_:)-8gc48)
