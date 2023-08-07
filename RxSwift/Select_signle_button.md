

기존 코드

reduce 내부에 API 호출이 있어서 
버튼의 갯수만큼 호출이 되었음

```swift
periodButtons.reduce(Disposables.create()) { disposable, button in
	let subscription = selectedButton.map { $0 == button }
		.bind(to: button.rx.isSelected)
	let identifierTags = selectedButton.map { $0.tag }
		.subscribe(onNext: { [weak self] tag in
			self?.requestPeriod(tag: tag)
		})
	return Disposables.create(disposable, subscription, identifierTags)
}
.disposed(by: bag)
```

reduce 외부에서 subscribe 하는 것으로 해결하였음

```swift
let periodButtons: [UIButton] = [weekButton, month1Button, month3Button, periodSettingButton].map { $0 }

let selectedButton = Observable.from(periodButtons.map({ button in
	button.rx.tap.map { button }
})).merge()

selectedButton
	.map { $0.tag }
	.subscribe(onNext: { [weak self] tag in
		self?.requestPeriod(tag: tag)
	})
	.disposed(by: bag)

periodButtons.reduce(Disposables.create()) { disposable, button in
	let subscription = selectedButton.map { $0 == button }
		.bind(to: button.rx.isSelected)

	return Disposables.create(disposable, subscription)
}
.disposed(by: bag)
```