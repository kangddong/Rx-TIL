
이 샘플 코드 프로젝트는 Xcode에서 StoreKit 테스트를 사용하므로 App Store Connect에서 설정을 완료하지 않고도 샘플 앱을 빌드하고 실행할 수 있습니다. 이 프로젝트는 Products.storekit 파일에서 StoreKit 테스트 서버용 인앱 제품을 정의합니다. 이 프로젝트는 이모티콘 문자에 매핑되는 제품 식별자를 포함하는 리소스 파일로 Products.plist를 포함합니다.

기본적으로, Xcode의 StoreKit 테스트는 비활성화 상태입니다. Products.storekit 구성 파일을 선택하고 Xcode에서 StoreKit 테스트를 활성화하려면 다음 단계를 따르세요:

계획을 클릭하여 계획 메뉴를 열고 계획 편집을 선택하세요.

계획 편집기에서 실행 작업을 선택하세요.

작업 설정에서 옵션을 클릭하세요.

StoreKit 구성 옵션의 경우, Products.storekit 구성 파일을 선택하십시오.

앱이 스토어를 초기화하면, 시스템은 Products.plist를 읽고 제품 식별자를 사용하여 StoreKit 테스트 서버에서 제품을 요청합니다.



출처
[StorKit API 사용하여 앱에 스토어 구현하기](https://developer.apple.com/documentation/storekit/in-app_purchase/implementing_a_store_in_your_app_using_the_storekit_api)