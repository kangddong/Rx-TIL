
```swift
public enum UIModalPresentationStyle : Int, @unchecked Sendable {

    case fullScreen = 0

    @available(iOS 3.2, *)
    case pageSheet = 1

    @available(iOS 3.2, *)
    case formSheet = 2

    @available(iOS 3.2, *)
    case currentContext = 3

    @available(iOS 7.0, *)
    case custom = 4

    @available(iOS 8.0, *)
    case overFullScreen = 5

    @available(iOS 8.0, *)
    case overCurrentContext = 6

    @available(iOS 8.0, *)
    case popover = 7

    @available(iOS 7.0, *)
    case none = -1

    @available(iOS 13.0, *)
    case automatic = -2

}
```


# over 가 붙으면 어떤 점이 달라질까 ?
