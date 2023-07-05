

메소드를 사용해서 map 하는 로직을 알게되어서 사용을 해보았다.

```swift

// occur retain cycle
rePasswordTextField.rx.text
	.orEmpty
	.filter { $0.count > 0 }
	.map(isSameNewPassword
	.bind(to: inValidPasswordNotiLabel.rx.isHidden)
	.disposed(by: bag)


// not occur retain cycle
rePasswordTextField.rx.text
	.orEmpty
	.filter { $0.count > 0 }
	.map{ [weak self] in self!.isSameNewPassword($0) }
	.bind(to: inValidPasswordNotiLabel.rx.isHidden)
	.disposed(by: bag)
```

여기서 궁금증은
map은 non escaping closure 라서 순환참조가 발생하지않을 줄 알았는데 발생한 점이다.


```swift
class ViewController: UIViewController {
    let bag: DisposeBag = DisposeBag()

    button.rx.tap
        .bind { self.label.rx.isHidden }
        .disposed(by: bag)
}

// 클로저 내부에서 weak self 사용하기
class ViewController: UIViewController {
    let bag: DisposeBag = DisposeBag()

    button.rx.tap
        .bind { [weak self] in
	        self?.label.rx.isHidden
	    }
        .disposed(by: bag)
}

// Declarative style 선언형으로 사용하기
class ViewController: UIViewController {
    let bag: DisposeBag = DisposeBag()

    button.rx.tap
        .bind(to: label.rx.isHidden)
        .disposed(by: bag)
}

```