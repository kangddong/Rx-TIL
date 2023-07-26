
```swift
final class SectionBackgroundDecorationView: UICollectionReusableView {

    override init(frame: CGRect) {
        super.init(frame: frame)

        self.backgroundColor = .white
        self.layer.cornerRadius = 10

    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")

    }

}

private func createLayout() -> UICollectionViewLayout {
	let layout = UICollectionViewCompositionalLayout { [weak self] sectionNumber, env -> NSCollectionLayoutSection? in

            /// section 번호마다 다른 Layout을 설정하기 위해 switch 문

            return self?.createSelectedLayout()
	}

	layout.register(SectionBackgroundDecorationView.self,
	 forDecorationViewOfKind: "background-element-kind")

	return layout
}
```
