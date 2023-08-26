
# UITabBarController

```swift
@MainActor
class UITabBarController: UIViewController
```



## Life cycle

viewcontroller의 Life Cycle과 특별하게 차이나지않는다.
* 최초 viewcontroller가 load 가 될 때,
* viewcontroller가 전환 될 때

UITabBarController에 A, B ViewController가 embed 되었다고 가정

### 최초 viewcontroller 로드 시 
``` swift
UITabBarController viewDidLoad()

A ViewController viewDidLoad()
A ViewController viewWillAppear(_:)

UITabBarController viewWillAppear(_:)

A ViewController viewDidAppear(_:)
UITabBarController viewDidAppear(_:)
```

최초 B ViewController 로드  시

``` swift
B ViewController viewDidLoad()
B ViewController viewWillAppear(_:)
A ViewController viewWillDisappear(_:)

tabBarController(_:didSelect:)

A ViewController viewDidDisappear(_:)
B ViewControllerswift viewDidAppear(_:)
```


각 viewcontroller 전환 시 A -> B

``` swift
B ViewControllerswift viewWillAppear(_:)
A ViewController viewWillDisappear(_:)

tabBarController(_:didSelect:)

A ViewController.swift viewDidDisappear(_:)
B ViewController viewDidAppear(_:)
```
