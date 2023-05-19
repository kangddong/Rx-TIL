
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