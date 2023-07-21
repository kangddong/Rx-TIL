


```swift
enum StoryboardName : String {
    case Home
    case Profile
}

extension UIViewController {
    class func instantiateController<T>(forName storyboard : UIStoryboardName) -> T {

	let storyboard = UIStoryboard.init(name: storyboard.rawValue, bundle: nil)
    let identifier = String(describing: self)

    return storyboard.instantiateViewController(withIdentifier: identifier) as! T

    }
}

// for example

let vc: HomeViewController = HomeViewController.instantiateController(forName: .Home)
```