1. **[유료 응용 프로그램 계약](In-App-Purchase/banking-tax-information.md)에 동의**
    
    앱 내 구입을 제공하려면 멤버십 계정 소유자가 App Store Connect의 “계약, 세금 및 금융거래” 섹션에서 [유료 응용 프로그램 계약에 동의](https://developer.apple.com/kr/help/app-store-connect/manage-agreements/sign-and-update-agreements)해야 합니다.
    [내 블로그에 정리](https://plcprogrammer-dy.tistory.com/118)
    
2. **앱 내 구입 디자인**
    
    앱 내 구입 경험이 앱의 다른 부분과 부합하는지 확인하고 제품을 효과적으로 선보이려면 [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/technologies/in-app-purchase) 및 [App Store 심사 지침](https://developer.apple.com/krwebsite-path)을 참고하십시오.
    
3. **App Store Connect에서 앱 내 구입 설정**
    
    [앱 내 구입을 생성](https://developer.apple.com/kr/help/app-store-connect/manage-consumable-and-non-consumable-in-app-purchases/create-in-app-purchases)하고 제품 이름, 설명, 가격 및 사용 가능 여부와 같은 메타데이터를 추가합니다. 또한 [앱 내 구입 키를 생성](https://developer.apple.com/kr/help/app-store-connect/configure-in-app-purchase-settings/generate-keys-for-in-app-purchases)하고 [세금 카테고리를 설정](https://developer.apple.com/kr/help/app-store-connect/configure-in-app-purchase-settings/set-a-tax-category-for-in-app-purchases)해야 합니다. 이를 통해 Apple이 고객 거래에 적용되는 적절한 세금을 계산할 수 있습니다. 
    
4. **StoreKit 구현**
    
    [Xcode](https://developer.apple.com/documentation/xcode/adding-capabilities-to-your-app)에서 앱에 `in-app purchase capabilities`을 추가하여 Xcode의 `bundle identifier` 및 `product identifiers`가 App Store Connect의 앱 및 앱 내 구입 `identifier`와 일치하는지 확인합니다.
    
5. **앱 내 구입 테스트**
    
    Apple은 “sandbox”라는 테스트 환경을 제공하고, 해당 환경에서 [테스트 계정](https://developer.apple.com/kr/help/app-store-connect/test-in-app-purchases-main/create-sandbox-apple-ids)을 사용하여 추가 비용 없이 [앱 내 구입을 테스트](https://developer.apple.com/documentation/storekit/in-app_purchase/testing_at_all_stages_of_development_with_xcode_and_the_sandbox)할 수 있습니다. 코드의 각 부분을 테스트하고 앱을 사용하여 앱 내 구입을 통한 코드가 올바르게 구현되었는지 확인합니다.
    
    [TestFlight](https://developer.apple.com/kr/help/app-store-connect/test-a-beta-version/overview-of-testflight) 또는 [Xcode](https://developer.apple.com/documentation/xcode/setting-up-storekit-testing-in-xcode)를 사용하여 앱 및 앱 내 구입의 추가적인 테스트를 진행할 수 있습니다.
    
6. **App Store Server 알림 사용**
    
    [App Store 서버 알림](https://developer.apple.com/documentation/appstoreservernotifications)은 거래 상태 및 앱 내 구입과 관련된 주요 이벤트(예를 들어, 환불, 구독 상태 변경 또는 “가족 공유” 액세스)의 업데이트를 실시간에 가깝게 제공합니다. 이러한 알림을 활용하려면 App Store Connect에서 [프로덕션 및 sandbox 서버 환경의 URL을 입력](https://developer.apple.com/kr/help/app-store-connect/configure-in-app-purchase-settings/enter-server-urls-for-app-store-server-notifications)해야 합니다.
    
7. **심사를 위해 앱 내 구입 제출**
    
    App Store에 앱 내 구입을 게시하기 전에 이를 [심사를 위해 제출](https://developer.apple.com/kr/help/app-store-connect/manage-submissions-to-app-review/submit-for-review)해야 합니다. 최초로 앱 내 구입을 제출하는 경우, 반드시 신규 버전의 앱을 제출해야 합니다. 제출하기 전에 [필수 정보](https://developer.apple.com/kr/help/app-store-connect/reference/required-localizable-and-editable-properties)가 누락되지 않았는지 확인하십시오. [앱 내 구입의 진행 상태](https://developer.apple.com/kr/help/app-store-connect/reference/in-app-purchase-statuses)를 모니터링하여 앱 내 구입을 사용할 수 있는지 또는 주의가 필요한지 여부를 파악하십시오.


### 참고
[Workflow for configuring in-app purchase-한국어판](https://developer.apple.com/kr/help/app-store-connect/configure-in-app-purchase-settings/overview-for-configuring-in-app-purchases/)