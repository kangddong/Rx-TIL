


기본 값을 지정하고 싶을 때

`protocol`에 함수를 정의할 때, 기본 값을 인자로 사용할 수 없다.
인자를 사용하게 되면 아래와 같은 에러가 나온다.
```swift


protocol Interface {
	func sample(item: Int = 0) // Default argument not permitted in a protocol method
}
```


프로토콜에서 기본 값을 지정하게 되면 아래와 같은 에러가 나온다.
```swift
protocol Interface {
	func sample(item: Int)
}

extension Interface {
	func sample(item: Int = 0) {
		sample(item = item)
	}
}
```