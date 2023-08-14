
```swift
final class OnoffButton: UIButton {

    enum OnOffButtonType {
        case normal
        case disabled
    }

    private var normalBackgroundColor: UIColor?
    private var disabledBackgroundColor: UIColor?

    override var isEnabled: Bool {
        didSet {
            if isEnabled {
                if let normalColor = normalBackgroundColor {
                    backgroundColor = normalColor
                }
            } else {
                if let disabledColor = disabledBackgroundColor {
                    backgroundColor = disabledColor
                }
            }
        }
    }

    public func setBackgroundColor(
	    _ color: UIColor?,
		for state: OnOffButtonType
	) {
        switch state {
        case .normal:
            normalBackgroundColor = color
            backgroundColor = color
            
        case .disabled:
            disabledBackgroundColor = color
        }
    }
}
```