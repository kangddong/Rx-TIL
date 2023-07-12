

# viewDidLoad
# viewWillAppear
# viewDidAppear
# viewWillDisAppear
# viewDidDisAppear


오토 레이아웃 없이 스토리보드를 사용하는 경우 관찰하는 동작은 스토리보드 내에서 뷰가 배치되고 크기가 조정되는 방식과 관련이 있을 수 있습니다.

`viewDidLoad` 메서드에서 뷰 컨트롤러의 뷰 계층 구조가 스토리보드에서 로드되었지만 추가 레이아웃 조정이나 화면에 맞게 크기 조정되지 않았을 수 있습니다. 따라서 `viewDidLoad`에서 검색하는 프레임 값은 스토리보드에 설정된 초기 치수를 반영할 수 있습니다.

`viewDidAppear` 메서드에서 뷰 컨트롤러의 뷰가 화면에 완전히 표시되고 뷰가 화면에 맞도록 필요한 모든 레이아웃 조정이 완료되었습니다. 이 시점에서 얻은 프레임 값은 화면에 표시되는 뷰의 실제 치수를 반영해야 합니다.

`viewDidLoad`와 `viewDidAppear` 사이의 `frame.width`에 차이가 있는 경우 `viewDidLoad` 이후에 보기의 레이아웃이 조정되고 있기 때문일 수 있습니다. 기기 방향 변경, 상태 표시줄 업데이트 또는 영향을 미치는 기타 요인 때문일 수 있습니다. 뷰의 크기.



```
filter: viewDidLoad

filter: visiblePwButton.frame.origin: (328.0, 10.0)
filter: m_edit_change_password.frame.width: 354.0
filter: visiblePwButton.frame.width: 20.0
filter: m_edit_change_password.frame.height: 40.0
filter: visiblePwButton.frame.height: 20.0

filter: viewWillAppear

filter: visiblePwButton.frame.origin: (329.0, 10.0)
filter: m_edit_change_password.frame.width: 354.0
filter: visiblePwButton.frame.width: 20.0
filter: m_edit_change_password.frame.height: 40.0
filter: visiblePwButton.frame.height: 20.0

filter: viewWillLayoutSubviews

filter: visiblePwButton.frame.origin: (329.0, 10.0)
filter: m_edit_change_password.frame.width: 354.0
filter: visiblePwButton.frame.width: 20.0
filter: m_edit_change_password.frame.height: 40.0
filter: visiblePwButton.frame.height: 20.0

filter: viewDidLayoutSubviews

filter: visiblePwButton.frame.origin: (329.0, 10.0)
filter: m_edit_change_password.frame.width: 394.0
filter: visiblePwButton.frame.width: 20.0
filter: m_edit_change_password.frame.height: 40.0
filter: visiblePwButton.frame.height: 20.0

filter: viewWillLayoutSubviews

filter: visiblePwButton.frame.origin: (329.0, 10.0)
filter: m_edit_change_password.frame.width: 394.0
filter: visiblePwButton.frame.width: 20.0
filter: m_edit_change_password.frame.height: 40.0
filter: visiblePwButton.frame.height: 20.0
filter: viewDidLayoutSubviews
filter: visiblePwButton.frame.origin: (329.0, 10.0)
filter: m_edit_change_password.frame.width: 394.0
filter: visiblePwButton.frame.width: 20.0
filter: m_edit_change_password.frame.height: 40.0
filter: visiblePwButton.frame.height: 20.0

filter: viewDidAppear

filter: visiblePwButton.frame.origin: (329.0, 10.0)
filter: m_edit_change_password.frame.width: 394.0
filter: visiblePwButton.frame.width: 20.0
filter: m_edit_change_password.frame.height: 40.0
filter: visiblePwButton.frame.height: 20.0
```