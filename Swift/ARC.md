
### 'weak' must not be applied to non-class-bound

순환참조 문제를 방지하기 위해서
보통 `delegate`와 같이 `delegate` 객체가 사라지면 ARC에서 자동으로 nil을 할당할 수 있도록 메모리 관리에 사용된다.
```swift
weak var delegate: SampleDelegate
```

```swift
protocol SampleDelegate: AnyObject {
	// AnyObject를 상속하지않으면 weak 키워드에 대한 에러가 발생한다.
}
```

`protocol`은 클래스, 구조체, 열거형에 사용이 되는데
어디에 사용이 될지 모르기에, reference count 관리를 위해 사용되는 `unowned`나 `weak` 키워드를 사용을 할 수 없다

`weak` 키워드를 사용했는데 그것이 구조체, 열겨형이면 ?!

`AnyObject`를 상속을 통하여, 클래스임을 의미하기에 `weak` 키워드가 사용 가능해진다 !