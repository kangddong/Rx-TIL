# `layoutIfNeeded()`

레이아웃 업데이트가 보류 중인 경우, 서브뷰를 즉시 배치합니다.

이 방법을 사용하여 뷰가 레이아웃을 즉시 업데이트하도록 강제하십시오. 자동 레이아웃을 사용할 때, 레이아웃 엔진은 제약 조건의 변화를 충족시키기 위해 필요에 따라 뷰의 위치를 업데이트합니다. 메시지를 루트 뷰로 받는 뷰를 사용하여, 이 방법은 루트에서 시작하는 뷰 하위 트리를 배치합니다. 보류 중인 레이아웃 업데이트가 없는 경우, 이 방법은 레이아웃을 수정하거나 레이아웃 관련 콜백을 호출하지 않고 종료됩니다.


```swift
    private func _startAnimation(_ preview: BannerView) {

        self.topConstraint.constant = 0

        UIView.animate(withDuration: 1.0,
                       delay: 0.0,
                       options: [.curveEaseInOut]) {

            self.view.layoutIfNeeded()

        } completion: { _ in
            DispatchQueue.main.asyncAfter(deadline: .now() + 3, execute: {
                self._endAnimation(preview)
            })
        }
    }
```

이러한 로직이었는데

```swift
self.topConstraint.constant = 0
```
위에 코드의 animation 시도시 위에서 아래로 내려오지않고, 좌상단에서 날라온 문제가 있었고
preview를 addsubview 한 이후에 바로 애니메이션이 일어나다보니, 그런 문제가 생긴 것 같았다

```swift
addSubview(preview) // 1
view.layoutIfNeeded() // 2
startAnimation // 3
view.layoutIfNeeded() // 4
```

하지만 `layoutIfNeeded()` 를 너무 자주 호출하는 것은 아닐지 비용에 대한 걱정이 있다.
하지만 공식문서를 확인하니, 변경사항이 없는 부분은 계산하지 않고 종료되기 때문에, 걱정한만큼 높은 비용이 들지는 않는다고한다.