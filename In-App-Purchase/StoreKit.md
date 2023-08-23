![[Pasted Graphic 17.png]]

인앱 구매 및 App Store와의 상호 작용을 지원

  

- 인앱구매 (In-App Purchase)

콘텐츠와 서비스에 대한 인앱 구매를 제공하고 홍보하세요.

- App transaction ()

App Store에서 서명한 거래로 고객의 앱 구매를 확인하세요.

- Ad network attribution

광고 기반 앱 설치를 검증하세요.

- Recommendations

third-party 콘텐츠에 대한 권장 사항을 제공하세요.

- Reviews

고객에게 App Store 리뷰와 평가를 요청하세요.

- Messages

앱에 App Store 메시지를 표시하세요.

  

StoreKit Framework 또한 고객의 Apple Music capabilities 를 확인할 수 있고, External Purchase, External Link Account, PaymentMethodBinding 을 위해 기능을 제공한다 

  

In-App Purchase를 볼거임

![[Pasted Graphic 18.png]]

Swift 기반 인터페이스를 사용하여 사용자에게 추가 콘텐츠와 서비스를 제공하십시오.

In-App Purchase API는 동시성과 같은 Swift 기능을 활용하여 인앱 구매 워크플로우를 단순화합니다. 
이 API를 사용하여 제품 정보를 로드하고, 상점에서 인앱 구매를 표시하고, 콘텐츠 및 구독에 대한 액세스를 관리하고, App Store에 서명한 거래 정보를 받으십시오. API는 비동기 작업 중에 Swift 동시성을 활용하여 대리 객체를 사용하는 대신 인라인으로 결과를 반환합니다.

In-App Purchase API는 다음을 제공합니다:

* JSON 웹 서명(JWS) 형식으로 App Store에 서명된 거래 정보.
* 클라이언트에서 쉽게 구문 분석할 수 있는 거래 및 구독 상태 정보.
* entitlements API, currentEntitlements는 고객을 위한 콘텐츠와 서비스를 잠금 해제하기 위한 자격 결정을 단순화합니다.

앱에서 스토어를 지원하려면, 다음 기능을 구현하세요:
* 앱이 실행되는 동안 최신 서비스와 콘텐츠를 제공하기 위해 거래 리스너, 업데이트를 사용하여 거래 상태 변경 사항을 들어보세요.
* `products(for:)`을 사용하여 App Store에서 앱에 표시할 제품을 요청하세요.
* 사용자가 `purchase(options:)`를 사용하여 App Store에서 인앱 제품을 구매할 수 있도록 합니다.
* 거래 기능 currentEntitlements를 사용하여 사용자의 인앱 구매를 반복하고 구매한 콘텐츠와 서비스의 잠금을 해제하세요.
* 선택적으로, API에서 받은 서명된 거래와 서명된 구독 상태 정보를 검증하십시오.

### 참고
[애플 공식문서 - StoreKit](https://developer.apple.com/documentation/storekit)
[애플 공식문서 - In-App Purchase](https://developer.apple.com/documentation/storekit/in-app_purchase/)
[StorKit API 사용하여 앱에 스토어 구현하기](In-App-Purchase/Implementing-In-App-Purchase.md)
[애플 공식문서 - StoreKit 연동](https://developer.apple.com/documentation/storekit/in-app_purchase/supporting_promoted_in-app_purchases_in_your_app)