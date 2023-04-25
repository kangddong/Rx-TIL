
# ObservableObject

## 원형
```swift
protocol ObservableObject: AnyObject
```
`AnyObject` 타입이기에 `class` 에서만 채택이 가능하다.

## Example

``` swift
class Contact: ObservableObject {
	@Published var name: String
	@Published var age: Int
	
	init(name: String, age: Int) {
		self.name = name self.age = age
	}
	
	func haveBirthday() -> Int {
		age += 1
		return age
	 }
}

let john = Contact(name: "John Appleseed", age: 24)
cancellable = john.objectWillChange
	.sink { _ in
		print("\(john.age) will change")
}
print(john.haveBirthday())
// Prints "24 will change"
// Prints "25"
```

기본적으로 ObservableObject 는  `@Published` 표시 된 프로퍼티의 변화를  `objectWillChange`  에서  방출해준다.