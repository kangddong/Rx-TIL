# UIHostingController


UIKit View 계층에 SwiftUI view를 통합하고 싶을 때 `UIHostingController` 를 사용
사용할 때,   view controller에 root view 하고 싶은 SwiftUI view 를 지정할 수 있다.
나중에 rootView 프로퍼티를 통해서 바꿀 수 있다.

사용 예시

```swift

let hostingController = UIHostingController(rootView: ExampleView())

hostingController.sizingOptions = .preferredContentSize
hostingController.modalPresentationStyle = .popover
self.present(hostingController, animated: true)
```

