
Storyboard vs Programmatically
취향차이라고 보통 말들 하신다.
결국 내가 속한 조직의 기존 방식에 따르는 경우가 많을 것 같다.

눈물을 머금고 쓴다고 생각했을 때, 쓰더라도 ! 잘 써보고싶었다.

```swift

// Crash !!
let storyboard = self.storyboard?.instantiateViewController(withIdentifier: "MainViewContrroller")

```

위에 코드는 `MainViewController` 대신 r이 하나 더 들어간 `MainViewContrroller` 때문에 Crash가 일어난다.
이런 실수를 발견했을 때 항상 스트레스가 쌓여만 갔다.
그리고 매번 같은 방식으로 VC를 호출하기에 Generic하게 만든 메소드가 있으면 멋들어질 것 같았다 !

이런 니즈가 나만 있지않았을꺼라는 생각에 바로 검색을 했고 검색 결과를 이해하고 적용을 해보았다

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
present(vc, animated: true)
```