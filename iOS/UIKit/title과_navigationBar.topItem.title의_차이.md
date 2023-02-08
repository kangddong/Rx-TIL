### 2023.02.08
## UIViewController의 title 과 navigationBar.topItem.title의 차이

1. UINavigationController는 UIViewController를 서브 클래싱 하고 있습니다

```swift
  @available(iOS 2.0, *)
  @MainActor open class UINavigationController : UIViewController {
  ...
  }
```

2. self.title Jump to Definition 해보시면 UIViewController 멤버 변수인걸 확인 가능합니다.

```swift
  @available(iOS 2.0, *)
  @MainActor open class UIViewController : UIResponder, NSCoding, UIAppearanceContainer, UITraitEnvironment, UIContentContainer, UIFocusEnvironment {
  ...
  open var title: String?
  ...
  }
```
3. vc 가 유효한 네비게이션 아이템 혹은 탭 바 아이템을 가지고 있다면 할당하여 업데이트 해줌 
<img width="951" alt="image" src="https://user-images.githubusercontent.com/50406861/217453400-84881d9d-9ae4-4690-8e50-abff5f999767.png">

[출처: Apple Developer](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621364-title)

4. extension에서도 self.title 했으면 되는거 아닌가 ?
* UIViewController와 UINavigationController에 각각 print를 통해 self가 런타임에 어디를 가리키고 있는지 확인 
```swift
  class AViewController: UIViewController {
    override func viewDidLoad() {
      super.viewDidLoad()
      
      self.title = "A ViewController"
      print("self on A ViewController = \(self)")
      navigationController?.setTitle("A ViewController")
    }
  }
```


```swift
  extension UINavigationCotroller {
    func setTitle(_ title: String) {
      super.viewDidLoad()
      
      self.navigationBar.topItem.title = "UINavigationController"
      print("self on UINaviController = \(self)")
    }
  }
```
