
가이드 문서를 통해서 flexbox를 구성하고 레이아웃하는 것을 보았다.
하지만 내가 FlexLayout를 사용하려고자 했던 이유는 동적인 UI를 구성하기 위함이었기 때문에
추가와 삭제 방법을 알 필요가 있었다.
```swift

confirmButton.rx
	.tap
	.asDriver()
	.drive(onNext: { (_) in
		print("confirmButton")
		print("called isSelected: \(self.confirmButton.isSelected)")
		if self.confirmButton.isSelected {
			self.testMenuView.flex.size(0)
			self.contentsView.flex.layout()
			self.contentsView.contentSize = self.rootFlexContainer.frame.size
			} else {
				self.rootFlexContainer.flex.addItem(self.testMenuView)
					.size(100)
					.backgroundColor(.cyan)
				self.contentsView.flex.layout()
				self.contentsView.contentSize = self.rootFlexContainer.frame.size
			}
		self.confirmButton.isSelected.toggle()
	})
	.disposed(by: bag)
```

`RxCocoa`를 사용한 코드이며,
`isSelected` 값으로 사이즈를 조절하면서 조절해보았다

deleted 하는 메소드는 아직 발견하지못했고, height를 nil로 날려버리면 될거같다