
# In-App-Purchase

Offer extra content and features — including digital goods, subscriptions, and premium content — directly within your app through in‑app purchases on all Apple platforms. You can even promote and offer in-app purchases directly on the App Store.

모든 Apple 플랫폼의 인앱 구매를 통해 앱 내에서 직접 디지털 상품, 구독 및 프리미엄 콘텐츠를 포함한 추가 콘텐츠와 기능을 제공합니다.
App Store에서 직접 인앱 구매를 홍보하고 제공할 수도 있습니다.

- Overview
- Configuring
- Testing
- Marketing
- Providing Support

## Overview

In-app purchases provide a consistent and safe experience facilitated by our world-class commerce and payment system

인앱 구매는 세계적 수준의 상거래 및 결제 시스템에 의해 촉진되는 일관되고 안전한 경험을 제공하여 사람들이 시간이 지남에 따라 구매와 구독을 쉽게 관리할 수 있도록 합니다.

인앱 구매를 통해, 사람들이 할 수 있는 것:

- 거의 200개의 결제 방법(Apple Pay, 신용 카드 또는 직불 카드, 매장 신용 카드, 지역별 방법 등 모두 파일에 안전하게 저장됨)을 지원하는 Apple ID와 연결된 결제 방법을 사용하여 44개의 통화로 빠르게 결제하세요.
- 앱이 지원하는 모든 장치에서 구매한 콘텐츠에 액세스하고, 새 장치에서 구매를 복원하세요.
- 문제 신고를 사용하여 구매한 콘텐츠에 대한 도움을 받거나 환불을 요청하세요.
- 가족 공유를 통해 자격 구매를 공유하세요.
- Apple 기기에서 구매 내역을 확인하세요.
- 모든 구독을 한 곳에서 관리하세요.


## In-App-Purchase Type

There are four types of in-app purchases and you can offer multiple types within your app.
앱 내 구매에는 네 가지 유형이 있으며 앱 내에서 여러 유형을 제공할 수 있습니다.

#### Consumable (소모성 항목)

소모성 앱 내 구입은 한 번 사용하면 소모되며 다시 구입할 수 있습니다. 소모성 앱 내 구입은 [부분 유료화 비즈니스 모델](https://developer.apple.com/kr/app-store/business-models/)을 사용하는 앱 및 [게임](https://developer.apple.com/kr/app-store/freemium-games/)에서 자주 사용됩니다.

#### Non-Consumable (비소모성 항목)

프리미엄 기능과 같이 한 번 구입하면 만료되지 않는 비소모성 항목을 제공해 보십시오. 비소모성 항목의 예로는 사진 앱의 추가 필터, 일러스트레이션 앱의 추가 브러시 또는 게임의 꾸미기용 아이템이 있습니다. 비소모성 앱 내 구입 항목을 가족 공유로 제공할 수 있습니다.

#### Auto-renewable subscriptions (자동 갱신 구독)

앱의 콘텐츠, 서비스 또는 프리미엄 기능에 대한 **지속적인 이용 권한을 제공**하십시오.
요금은 사용자가 **구독을 해지할 때까지 반복해서 청구**됩니다.
자동 갱신 구독은 가족 공유가 가능합니다.

#### Non-renewing subscriptions (비갱신형 구독)

한정된 기간 동안 서비스 또는 콘텐츠에 대한 이용 권한을 제공해 보십시오.
이런 유형의 구독은 **자동으로 갱신되지 않기 때문에** 이용 권한을 유지하려면 사용자는 **기존의 구독이 종료된 후** 새로운 구독을 구입해야 합니다.

## Configuring in-app purchases

앱 내 구입을 생성하고 앱에서 제공하기에 앞서 유료 응용 프로그램 계약에 서명하고 App Store Connect에서 [세금 및 금융거래 정보](https://developer.apple.com/kr/help/app-store-connect/provide-tax-information/tax-forms-overview/)를 설정해 보십시오.

#### Set up in App Store Connect

제품명, 설명, 가격 및 사용 가능 여부와 같은 세부 사항을 추가하여 App Store Connect에서 앱 내 구입을 구성해 보십시오. 또한 현지화 버전을 추가하여 앱이 제공되는 지역의 언어로 사용자의 구입을 원활하게 지원할 수 있습니다.

#### Use StoreKit

Xcode 에서 앱에 앱 내 구입 기능을 추가한 후 `StoreKit`을 사용하여 안전하고 보안이 유지되는 구입 경험을 위한 앱 내 구입을 지원해 보십시오. `StoreKit` 프레임워크 및 앱 내 구입 API는 제품 정보 검색, 결제 처리, 제품 배송 등 구입에 관한 작업을 처음부터 끝까지 처리합니다.

[Go to StoreKit](In-App-Purchase/StoreKit.md)


#### Determine transaction status

App Store 서버 알림을 사용하면 환불 또는 구독 상태의 변경이나 가족 공유 이용과 같은 앱 내 구입과 관련된 거래 상태 및 중요 이벤트에 대한 근 실시간 업데이트를 제공할 수 있습니다. 이 정보를 이용하여 거래 기록을 업데이트하고 앱에서 맞춤형 경험을 제공할 수 있습니다. 예를 들어, 사용자가 자동 갱신을 끈 경우 구독자의 재구독을 유도할 수 있는 프로모션 특가를 표시할 수 있습니다. App Store 서버 알림을 활성화하려면 App Store Connect에서 개발자의 서버로 연결되는 [URL을 제공](https://developer.apple.com/kr/help/app-store-connect/configure-in-app-purchase-settings/enter-server-urls-for-app-store-server-notifications/)합니다.

App Store Server API를 사용하여 제품 Entitlement(권한) 및 거래 업데이트 정보를 확인할 수 있습니다. 앱 외부에서 이루어진 상태 변경을 포함한 앱 내 구입 거래 내역 및 최신 상태를 확인할 수 있습니다.


간략하게 정리를 해보자 !

1. 세금 및 금융거래 정보를 설정
2. App Store Connect 설정 추가
3. StoreKit 연동


### 키워드
인앱 구매 - in-app purchases(IAP)
디지털 상품 - digital goods
구독 - subscriptions


### 참고
[애플 디벨로퍼 - 인앱구매](https://developer.apple.com/in-app-purchase/)
