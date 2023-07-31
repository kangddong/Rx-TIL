
기존 RGB를 통한 init

```swift
init(red: CGFloat,
	 green: CGFloat,
	 blue: CGFloat,
	 alpha: CGFloat
)
```

기존에는 red, green, blue에 0.0 ~ 1.0 값을 넣어야했습니다.
보통 디자인에서는 0~255 사이의 값을 받기에 우린 `red: 204/255`와 같이 표현해주어야했습니다.

```swift
convenience init(red: CGFloat, green: CGFloat, blue: CGFloat) {
	assert(red >= 0 && red <= 255, "Invalid red component")
	assert(green >= 0 && green <= 255, "Invalid green component")
	assert(blue >= 0 && blue <= 255, "Invalid blue component")

	self.init(red: red / 255.0,
			  green: green / 255.0,
			  blue: blue / 255.0,
			  alpha: 1.0
	)
}
```