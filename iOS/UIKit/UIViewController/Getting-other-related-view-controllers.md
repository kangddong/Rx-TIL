


# **presentationController**

```swift
var presentationViewController: UIPresentationController? { get }
```

현재 view controller를 관리하는 presentation controller.

view controller가 presentation controller에 의해 관리되는 경우, 이 속성은 해당 객체를 포함합니다.
view controller가 presentation controller에 의해 관리되지 않는 경우 이 속성은 nil입니다.
아직 현재 view controller를 present하지 않았다면, 이 속성에 액세스하면 modalPresentationStyle 속성의 현재 값을 기반으로 presentation controller가 생성됩니다.
presentation controller에 접근하기 전에 항상 그 속성의 값을 설정하세요.

# **presentedViewController**

```swift
var presentedViewController: UIViewController? { get }
```
The view controller that is presented by this view controller, or one of its ancestors in the view controller hierarchy.

이 뷰 컨트롤러에 의해 presented 된 뷰 컨트롤러 또는 뷰 컨트롤러 계층 구조의 조상 중 하나.

`present(:animated:completion:)` 메서드를 사용하여 view controller를 모달(명시적 또는 암시적으로) `present`할 때, 메서드를 호출한 view controller는 이 속성을 제시한 view controller로 설정합니다.
현재 view controller가 다른 view controller를 **모달로 표시하지 않았다면**, 이 속성의 값은 `nil`입니다.


NavigationController.rootViewControoler = A ViewController
**A ViewController -> push -> B ViewController** -> present -> C ViewController
After presented C ViewController

```swift
po navigationController.presentationViewController
▿ Optional<UIPresentationController>
  - some : <_UIPageSheetPresentationController>

po navigationController.presentedViewController
▿ Optional<UIViewController>
  ▿ some : <TestApp.CViewController: 0x10a82b600>
  
po navigationController.presentingViewController
nil
```
# **presentingViewController**

이 뷰 컨트롤러를 제시한 뷰 컨트롤러.

`present(:animated:completion:)` 메서드를 사용하여 view controller를 모달(명시적 또는 암시적으로) 제시할 때, 제시된 view controller는 이 속성을 제시한 view controller로 설정합니다. 뷰 컨트롤러가 모달 방식으로 제시되지 않았지만 조상 중 하나가 있었다면, 이 속성에는 조상을 제시한 view controller가 포함되어 있습니다. 현재 view controller나 그 조상이 모달 방식으로 제시되지 않았다면, 이 속성의 값은 `nil`이다.


주의사항은 present를 호출하더라도, overFullScreen과 같이 modally 하지않은 경우에는 원하는 값을 못 볼수 있다. present != modally 기억하자
[애플 공식문서 - presentedViewController](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621407-presentedviewcontroller)
[애플 공식문서 - presentingViewController](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621430-presentingviewcontroller)