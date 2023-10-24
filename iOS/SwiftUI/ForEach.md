
```swift
init(
	 _ data: Data,
	 id: KeyPath<Data.Element, ID>,
	 @ViewBuilder content: @escaping (Data.Element) -> Content
)
```


`Data`가 `RandomAccessCollection`을 준수하고, `ID`가 `Hashable`을 준수하고, `content`가 `View`를 준수할 때 사용할 수 있습니다.


## 참고

[애플 공식문서 - init](https://developer.apple.com/documentation/swiftui/foreach/init(_:id:content:)-82hm4)