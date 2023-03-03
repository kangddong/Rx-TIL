### 2023.03.03

### 참고자료
[UINavigationBar에 대한 공식 문서](https://developer.apple.com/documentation/uikit/uinavigationbar#overview)
[Navigation Bar Cutomize Guide 문서](https://developer.apple.com/documentation/uikit/uinavigationcontroller/customizing_your_app_s_navigation_bar)


아래 코드와 같이 navigationBar의 backgroundColor를 변경하면 원치않는 결과를 얻을 때가 있다.

```swift
navigationController?.navigationBar.backgroundColor = UIColor.red
```



```swift
let appearance = UINavigationBarAppearance()
appearance.configureWithOpaqueBackground()
appearance.backgroundColor = UIColor(red: 0.24, green: 0.33, blue: 0.67, alpha: 1.0)
navigationController.navigationBar.standardAppearance = appearance
// standard는 스크롤을 하고 있는 도중의 색상을 의미
navigationController.navigationBar.scrollEdgeAppearance = appearance
// scroll edge는 스크롤을 하기 전 색상을 의미
```
