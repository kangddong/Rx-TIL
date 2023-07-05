

# rx.text 사용할 때 주의해야하는 부분

text가 변할 때만 이벤트가 방출될 것으로 에상했지만, 실제로 사용해보니 그렇지않았습니다.
text가 사용 되는 `UITextField, UISearchBar, UITextView` 를 사용시에 영향이 갑니다.
*RxCocoa 6.5.0* 기준 입니다.

.text 프로퍼티 구현부를 봅시다.

```swift
extension Reactive where Base: UITextField {
    /// Reactive wrapper for `text` property.

    public var text: ControlProperty<String?> {
        value
    }

    /// Reactive wrapper for `text` property.

    public var value: ControlProperty<String?> {
        return base.rx.controlPropertyWithDefaultEvents(
            getter: { textField **in**
                textField.text
            },
            setter: { textField, value **in**
                // This check is important because setting text value always clears control state
                // including marked text selection which is important for proper input
                // when IME input method is used.
                if textField.text != value {
                    textField.text = value
                }
            }
        )
    }
}
```


text는 value를 wrapper 입니다.

 value 의 `controlPropertyWithDefaultEvents`  살펴보면 UIControl 까지 가게됩니다.
 ```swift
 UIControl.Event = [.allEditingEvents, .valueChanged] 
```
 이렇게 두개의 이벤트를 받고 있는 것을 볼 수 있습니다.

```swift
extension Reactive where Base: UIControl {
	/// This is a separate method to better communicate to public consumers that
    /// an `editingEvent` needs to fire for control property to be updated.
    internal func controlPropertyWithDefaultEvents<T>(
        editingEvents: UIControl.Event = [.allEditingEvents, .valueChanged],
        getter: @escaping (Base) -> T,
        setter: @escaping (Base, T) -> Void
        ) -> ControlProperty<T> {
        return controlProperty(
            editingEvents: editingEvents,
            getter: getter,
            setter: setter
        )
    }		  
}
```


아래와 같은 코드가 있을 때 위 코드가 속한 메소드 (예를 들면 bind 에서)가 호출될 때 event가 방출된다.


```swift
textField.rx
	.text
	.orEmpty
	.asDriver()
	.drive(onNext: { [weak self] str in
		// po textField.allControlEvents  -> rawValue: 0
	})
	.disposed(by: bag)
```

UIControl.Event 문서에는 rawValuew: 0에 대한 정보가 없다


![[Pasted image 20230704184423.png]]