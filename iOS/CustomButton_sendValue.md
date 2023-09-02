
```swift
@objc
func buttonTouched(_ sender: UIButton) {
	let mult = Double(sender.tag)
	let oldValue = self.value
	
	self.value += mult * stepValue
	
	if oldValue != value {
		sendActions(for: .editingDidBegin)
		sendActions(for: .valueChanged)
		sendActions(for: .editingDidEnd)
	}
}
```