

```swift
optional func textView(
	_ textView: `UITextView`,
	shouldChangeTextIn range: `NSRange`,
	replacementText text: `String`
) -> `Bool`
```

`UITextView` 의 `delegate`을 위임받으면 사용할 수 있는 메소드이다
Text view에서 지정한 텍스트를 바꿀 수 있는 메소드이다.

### textView
변화가 포함된 textView이다.

### range
현재 선택 범위이다
`range`의 `length`가 0인 경우 현재 삽입점을 반영한다.
사용자가 삭제 키를 누르면 `range`의 `length`는 1이고 
빈 문자열 개체가 단일 문자를 대체한다.

### text
추가 될 텍스트이다.

### return Value



```swift

func textView(_ textView: UITextView, shouldChangeTextIn range: NSRange, replacementText text: String) -> Bool {
																					let limit = 50

	guard
		let str = textView.text,
              str.count < limit
		else {
			// 입력시 1 지울시 0
			if text.count == 0 {
				return true
			} else {
				return false
				}
	}

	print("str.count, text.count, range.length")

        print(str.count, text.count, range.length)

	let newLength = str.count + text.count - range.length
	return newLength <= limit
}
```