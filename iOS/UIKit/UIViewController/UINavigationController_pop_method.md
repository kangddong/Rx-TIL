
- `UINavigationController`는 `UIViewController`를 `Stack`으로 관리를 한다.

# popViewController(animated:)
Pops the top view controller from the navigation stack and updates the display.

- `Stack`의 상위 `view controller`를 제거하고 `stack` 새로운 상단의 활성화 된 `view controller`로 만든다.
- `Stack`의 마지막 item을 pop 할 수 없습니다.
# popToViewController(__:animated:)
특정 view controller가 네비게이션 Stack의 상단이 될 때까지 pop 하고 디스플레이를 업데이트

```swift
func popToViewController(
	_ viewController: UIViewController,
	animated: Bool
) -> [UIViewController]?
```

viewController
스택의 맨 위에 있고 싶은 `viewController`. `viewController`는 현재 내비게이션 `Stack`에 있어야 합니다.


# popToRootViewController(animated:)
Root view controller를 제외한 Stack의 모든 view controller를 `pop`하고 디스플레이를 업데이트
