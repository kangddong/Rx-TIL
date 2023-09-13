 
문자열에서 문자를 대치하고 싶을 때 

```swift
/// Returns a new string in which all occurrences of a target
/// string in a specified range of the string are replaced by
/// another given string.

func replacingOccurrences<Target, Replacement>(
	of target: Target,
	with replacement: Replacement,
	options: String.CompareOptions = [],
	range searchRange: Range<Self.Index>? = nil
) -> String where Target : StringProtocol, Replacement : StringProtocol

/// Returns a new string in which all occurrences of a target
/// string in the receiver are replaced by another given string.
func replacingOccurrences(
	of target: String,
	with replacement: String
) -> String
```

```swift
let newString = smapleString.replacingOccurrences(of: "<br>", with: "")
```


# initializer

`init(describing: TextOutputStreamable)`


```swift
let input = readLine()!.components(separatedBy: CharacterSet) -> [String]
```


주어진 세트의 문자로 나눈 수신기의 부분 문자열을 포함하는 배열을 반환합니다.
```swift
func components(separatedBy: CharacterSet) -> [String]
```

### CharacterSet
`CharacterSet`은 유니코드 호환 문자 집합을 나타냅니다. 
`Foundation` 유형은 `CharacterSet`을 사용하여 검색 작업을 위해 문자를 그룹화하여 검색 중에 특정 문자 세트를 찾을 수 있습니다.

이 유형은 "copy-on-write" 동작을 제공하며, Objective-C NSCharacterSet 클래스에 브릿지됩니다.

## String.Index 사용

`String`은 `Int` 타입으로는  `subscript` 로 접근할 수 없음 -> 왜 ?...
`String.Index`로 접근해야함

주어진 index으로부터 지정된 거리의 index를 반환
```swift
func index(
	_ i: String.Index,
	offsetBy distance: Int
) -> String.Index
```


인덱스 i로부터의 거리로 오프셋된 인덱스. 
distance가 양수인 경우, 이것은 `index(after:)`에 대한 거리 호출의 결과와 동일한 값입니다. distance가 음수라면, 이것은 `index(before:)`에 대한 `abs(distance)` 호출의 결과와 같은 값이다.

### String.SubSequence

```swift
let str = my_string[frontIdx] // Character Type
let str2 = my_string[...frontIdx] // String.SubSequence Type
```
