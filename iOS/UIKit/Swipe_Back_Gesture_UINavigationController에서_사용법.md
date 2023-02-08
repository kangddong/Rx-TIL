### 2023.01.04
## Swipe Back Gesture


Swipe Back Gesture
  
기존 앱에서는 push, pop 같은 수평을 이동하는 구조에서 Swipe를 통해 뒤로 돌아갈 수 있었다.
  
그런데 간혹 내가 만든 화면에서는 스와이프로 이동이 되지않는 경우가 많았고, 해결하고 싶었다.
  
```swift
  // UINavigationController 기본 네비게이션 헤더 영역을 사용할 때
  self.navigationController?.interactivePopGestureRecognizer?.delegate = self
   
  // UINavigationController 커스텀 네비게이션 헤더 영역을 사용할 때
  self.navigationController?.interactivePopGestureRecognizer?.delegate = nil   
```
