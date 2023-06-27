
```swift
/**
Pin all edges on its superview's corresponding edges (top, bottom, left, right). Similar to calling`view.top(insets).bottom(insets).left(insets).right(insets)`
*/

@discardableResult

public func all(_ insets: PEdgeInsets) -> PinLayout {

    top(insets.top, { "all(\(insets)) top coordinate" })
    bottom(insets.bottom, { "all(\(insets)) bottom coordinate" })
    left(insets.left, { "all(\(insets)) left coordinate" })
    right(insets.right, { "all(\(insets)) right coordinate" })
    
    return self
}
```

`bottom`, `left`, `right`는 `top`과 똑같은 구조이다.

```swift
@discardableResult

internal func top(_ value: CGFloat, _ context: Context) -> PinLayout {
    
    setTop(value, context)
    return self
}
```


```swift
internal func setTop(_ value: CGFloat, _ context: Context) {

	if let _vCenter = _vCenter {
		warnConflict(context, ["Vertical Center": _vCenter])

    } else if let _top = _top, _top != value {
        warnPropertyAlreadySet("top", propertyValue: _top, context)
    } else {
        _top = value
    }
}
```