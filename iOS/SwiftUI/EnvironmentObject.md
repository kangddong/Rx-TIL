# EnvironmentObject

잘못 사용하면 나오는에러

```
fatal error: No ObservableObject of type <EnvironmentObject> found. A View.environmentObject(_:) for MyModel may be missing as an ancestor of this view.

```

UIKit 베이스에서 사용할 때 사용법

```swift
struct ExampleView: View {
	@EnvironmentObject var model: Model
	
	var body: some View {
		// 중략...	}
}
```


```swift
let hostingController = UIHostingController(
	rootView: ExampleView()
		.environmentObject(model)
)
hostingController.sizingOptions = .preferredContentSize // available iOS16
hostingController.modalPresentationStyle = .popover

self.present(hostingController, animated: true)
```