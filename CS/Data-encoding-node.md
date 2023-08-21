

[KeyedDecodingContainer 정리](CS/KeyedDecodingContainer)


Type에 따라 오버로딩이 많이 되어있지만
메소드 원형 종류로 정리해봤다


```swift
func decode(
	_ type: Int16.Type,
	forKey key: KeyedDecodingContainer<K>.Key
) throws -> Int16
```

```swift
func decodeIfPresent(
	_ type: Int16.Type,
	forKey key: KeyedDecodingContainer<K>.Key
) throws -> Int16
```

```swift
func decodeNil(
	forKey key: KeyedDecodingContainer<K>.Key
) throws -> Bool
```