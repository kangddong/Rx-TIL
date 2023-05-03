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


```swift
private lazy var _contentsView: UIHostingController<some View> = {
	let model = MyModel.shared
    let hostingController = UIHostingController(
	    rootView: BlockAppSelectionView()
		    .environmentObject(model)
	)
	return hostingController

}()

/* not add some View
Property definition has inferred type 'UIHostingController<some View>',
involving the 'some' return type of another declaration
*/

static let _contentsView2: UIHostingController = UIHostingController(
        rootView: BlockAppSelectionView()
            .environmentObject(MyModel.shared)
 )

private let _contentsView3: UIHostingController = UIHostingController(
        rootView: BlockAppSelectionView()
    )

private func getContentsView() -> UIHostingController<some View> {

	let model = MyModel.shared
    let hostingController = UIHostingController(
            rootView: BlockAppSelectionView()
                .environmentObject(model)
    )
    return hostingController
}
```