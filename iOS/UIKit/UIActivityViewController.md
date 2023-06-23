
# Overview

* pasteboard에 항목을 복사
* 소셜 미디어 사이트에 콘텐츠를 게시
* 이메일이나 SMS를 통해 항목을 보내는 것과 같은 몇 가지 표준 서비스
* 앱은 또한 사용자 지정 서비스를 정의할 수 있다.

당신의 앱은 이 뷰 컨트롤러를 configuring, presenting, and dismissing할 책임이 있습니다.
뷰 컨트롤러의 configuring은 뷰 컨트롤러가 작동해야 하는 데이터 객체를 지정하는 것을 포함한다.
(앱이 지원하는 사용자 지정 서비스 목록을 지정할 수도 있습니다.) 

뷰 컨트롤러를 presenting할 때, 현재 장치에 적합한 수단을 사용하여 그렇게 해야 합니다. 
iPad에서는 popover에서 뷰 컨트롤러를 표시해야 합니다. 
iPhone과 iPod touch에서, 모달로 제시해야 합니다.

# initializer

```swift
init(
	activityItems: [Any],
	applicationActivities: [`UIActivity`]?
)
```

### activityItems

activity을 수행할 데이터 객체의 배열. 
배열의 객체 유형은 가변적이며 애플리케이션이 관리하는 데이터에 따라 다릅니다. 예를 들어, 데이터는 현재 선택된 콘텐츠를 나타내는 하나 이상의 문자열 또는 이미지 객체로 구성될 수 있습니다.