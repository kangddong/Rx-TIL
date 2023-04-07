
# NSLocalizedString

```swift
func NSLocalizedString(
		_ key: String,
		tableName: String? = nil,
		bundle: Bundle = Bundle.main,
		value: String = "",
		comment: String
) -> String
```

## **Parameter**

### **key**

지정된 테이블에서 key로 사용 될 String

### tableName

`tableName`은 `NSLocalizedString` 함수의 옵셔널한 매개변수 중 하나이며, 로컬라이즈된 문자열을 저장하는 데 사용되는 파일을 지정합니다. 이 때, 파일이름은 `tableName`에 지정한 값 뒤에 `.strings` 확장자를 붙여서 만들어집니다.

일반적으로, 로컬라이즈된 문자열은 `Localizable.strings` 파일에 저장되며, 이 파일은 앱 번들 내에 위치합니다. 따라서, `tableName` 매개변수를 지정하지 않을 경우, 이 파일의 테이블이 기본값으로 사용됩니다.

만약 앱 내에서 특정한 목적을 가진 로컬라이즈 파일을 사용한다면, `tableName` 매개변수를 이에 맞게 지정할 수 있습니다. 이렇게 하면, 해당 파일 내에 특정한 키-값 쌍만을 사용할 수 있어서, 앱 전체의 로컬라이즈 파일에 비해 더욱 가볍고 간결한 문자열 파일을 만들어 사용할 수 있습니다.

### bundle

테이블의 문자열 파일이 포함된 번들. 메인 번들은 지정되지 않은 경우 사용됩니다.

### value

개발 로케일을 위한 현지화된 문자열. 다른 로케일즈의 경우, 테이블에서 키를 찾을 수 없는 경우 이 값을 반환하십시오.

### comment

주의사항

String Interpolation(문자열 보간법) 피하기

```swift
NSLocalizedString(
		"dominant-color-caption",
    value: "The dominant color is \\(dominantColor).",
    comment: "Image caption identifying the color that stands-out the most."
)

/* Image caption identifying the color that stands-out the most. */
"dominant-color-caption" = "The dominant color is (dominantColor).";
```

Instead, to dynamically insert values within localized strings, set `value` to a format string, and use `localizedStringWithFormat(_:_:)` to insert those values.

```swift
let format = NSLocalizedString(
		"dominant-color-caption",
    value: "The dominant color is %@.",
    comment: "Image caption identifying the color that stands-out the most."
)
let localizedString = String.localizedStringWithFormat(format, favoriteColor)
```

```swift
/* Image caption identifying the color that stands-out the most. */"dominant-color-copation" = "The dominant color is %@.";
```

For information about inserting plural nouns and units into localized strings, see [Localizing strings that contain plurals](https://developer.apple.com/documentation/xcode/localizing-strings-that-contain-plurals).


[레퍼런스](https://developer.apple.com/documentation/foundation/1418095-nslocalizedstring)[https://developer.apple.com/documentation/foundation/1418095-nslocalizedstring](https://developer.apple.com/documentation/foundation/1418095-nslocalizedstring)
