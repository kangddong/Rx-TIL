```swift
UIApplication.shared.windows.first(where: { $0.isKeyWindow })
```
iOS 13에서 큰 변화는 AppDelegate 이외에 SceneDelegate가 추가된 것이라고 생각이 된다.
기존의 rootviewcontroller를 찾는 코드는 AppDelegate의 window를 통해서 찾았는데


``'windows' was deprecated in iOS 15.0: Use UIWindowScene.windows on a relevant window scene instead``

이제는 UIWindowScene.windows 를 통해서 찾아야한다.


```swift
guard let windowScene = UIApplication.shared.connectedScenes.first as? UIWindowScene,
           let delegate = windowScene.delegate as? SceneDelegate else { return nil }
guard let rootViewController = delegate.window?.rootViewController else { return nil }
```
 대안은 이렇다