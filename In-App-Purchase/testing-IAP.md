
Apple은 “sandbox”라는 테스트 환경을 제공하고, 해당 환경에서 [테스트 계정](https://developer.apple.com/kr/help/app-store-connect/test-in-app-purchases-main/create-sandbox-apple-ids)을 사용하여 추가 비용 없이 [앱 내 구입을 테스트](https://developer.apple.com/documentation/storekit/in-app_purchase/testing_at_all_stages_of_development_with_xcode_and_the_sandbox)할 수 있습니다.


# Sandbox Apple ID 생성

신규 Sandbox 테스터를 생성하려면 다음 정보를 제공하십시오:

- 이름
- 성
- 이메일 주소
    
    Apple ID로 사용한 적이 없거나 iTunes 또는 App Store 콘텐츠 구입에 사용한 적이 없는 이메일 주소를 사용하십시오. 모든 Sandbox 테스터에게 전용 이메일 주소를 생성하는 것을 고려해야 합니다.
    
    
    
- 암호
    
    표준 Apple ID와 마찬가지로 Sandbox Apple ID에는 강력한 암호가 필요합니다. 암호를 입력할 때 암호가 요구 사항을 충족하지 않는 경우 권장 사항이 표시됩니다.


[App store Connect - Sandbox 테스트 생성](https://appstoreconnect.apple.com/access/users/sandbox)으로 이동 계정 생성



## 앱 내 구입 테스트

Sandbox는 App Store의 인프라를 사용하지만 실제 결제는 처리하지 않습니다. 대신, 결제가 성공적으로 처리된 것과 같이 거래내역이 반송됩니다.
* 앱 심사의 승인 필요 없음

## App Store 국가 및 지역

테스트 계정의 지역을 175개의 App Store 지역 중 하나에 연계할 수 있습니다. 
이를 통해 새로운 테스터를 생성하지 않고도 동일한 sandbox Apple ID를 사용하여 다양한 지역의 App Store에서 테스트를 진행할 수 있습니다.

이메일 서비스 공급자가 더하기 기호(+)가 있는 이메일 하위 주소 지정을 지원하는 경우 샌드박스 테스터에 샌드박스 관련 주소의 하위 주소를 사용할 수 있습니다. 예를 들어 기본 샌드박스 이메일이 `billjames2@icloud.com`인 경우, `billjames2+UK@icloud.com`, `billjames2+US@icloud.com`, `billjames2+JP@icloud.com`을 추가 테스터의 이메일 주소로 사용할 수 있습니다. 하위 주소로 보내는 모든 메시지는 기본 주소로도 전달됩니다.

국가 및 지역의 변경을 완료하고 기기에서 sandbox Apple ID로 다시 한번 로그인을 진행하면 변경이 완료됩니다.

[앱 내 구입 테스트](https://developer.apple.com/kr/help/app-store-connect/test-in-app-purchases-main/test-in-app-purchases)