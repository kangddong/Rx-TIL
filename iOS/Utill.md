**if** ( [[[UIDevice currentDevice] systemVersion] floatValue] > 6.9)

```swift
// commonExtension
extension NSObject {
	var className: String {
		return String(describing: type(of: self))
	}
}
```