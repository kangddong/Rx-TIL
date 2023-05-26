

# ApplicationToken
응용프로그램의 표현

``` swift
typealias ApplicationToken = Token<Application>
```


>  개인 사용자 데이터에 액세스하지 않고 device 응용 프로그램을 제한하고 필터링하는 토큰입니다.
>  `FamilyActivitySelection` 항목은 동일한 `Family Sharing group` 내의 device가 응용 프로그램을 식별하는데 사용할 수 있는 토큰을 제공합니다.

## Token
신원을 밝히지 않는 앱 또는 웹사이트와 같은 활동의 표현입니다.

``` swift 
struct Token<T>
```

`Managed Settings`은 사용자 개인정보를 보호하고 `Family Sharing group` 외부의 사람이 가족이 액세스하는 앱과 웹사이트를 식별하지 못하도록 하기 위해 `Token`을 사용합니다. 
토큰을 사용하여 개인 정보에 접근하지 않고 장치 사용을 제한하고 필터링할 수 있습니다.

`ManagedSettings` 프레임워크는 다음 유형의 토큰을 제공합니다.

[`ApplicationToken`](https://developer.apple.com/documentation/managedsettings/applicationtoken)

선택한 앱의 opaque 표현입니다.

[`WebDomainToken`](https://developer.apple.com/documentation/managedsettings/webdomaintoken)

선택한 웹 도메인의 opaque 표현입니다.

[`ActivityCategoryToken`](https://developer.apple.com/documentation/managedsettings/activitycategorytoken)

선택한 활동 범주의 opaque 표현입니다.

## Application

``` swift 
struct Application
```

`ManagedSettings`은 사용자 개인정보 보호 및 제어를 유지하기 위해 토큰이 있는 앱을 나타냅니다.

### initialization

``` swift 
init(bundleIdentifier: String)

init(token: ApplicationToken)
```

I think Primary Property is bundleIndentifier

### bundleIdentifier
The unique string that identifies this app

`shield configurations`을 제공하는 extension에서 이 property는 앱의 bundleIdentifier를 제공합니다. 
해당 extension 외부에서 이 속성에 액세스하는 경우 값은 입니다 `nil`.
자세한 내용은 `ManagedSettingsUI`의 `ShieldConfigurationDataSource` 프레임워크를 참조 하십시오 .


# ManagedSettingsUI

## ShieldConfigurationDataSource
```swift
@objc class ShieldConfigurationDataSource
```

The base class for the principal object of an app extension that configures a shield’s appearance.
방패 모양을 구성하는 앱 확장의 주요 개체에 대한 기본 클래스입니다.

The system provides your extension with the display names, bundle identifiers, and domains for each application, website, or category it shields. Your extension is expected to return an appropriate configuration as quickly as possible, in order to provide the best possible user experience. To protect the Family Sharing group’s privacy, your extension runs in a sandbox. This sandbox prevents your extension from making network requests or moving sensitive content outside the extension’s address space. The system provides a default appearance for any methods that your subclass doesn’t override, or if it takes too long to return a configuration.

시스템이 응용 프로그램이나 웹 사이트를 가리기 위해 사용하는 실드의 모양을 사용자 지정하는 확장 프로그램을 customize 만들 수 있습니다. 
시스템은 보호하는 각 애플리케이션, 웹 사이트 또는 category에 대한 display names, bundle identifiers 및 도메인을 확장 프로그램에 제공합니다. 
최상의 사용자 경험을 제공하기 위해 귀하의 확장 프로그램은 가능한 한 빨리 적절한 구성을 반환해야 합니다. 가족 공유 그룹의 개인 정보를 보호하기 위해 확장 프로그램은 샌드박스에서 실행됩니다. 이 샌드박스는 확장 프로그램이 네트워크 요청을 하거나 확장 프로그램의 주소 공간 외부로 민감한 콘텐츠를 이동하는 것을 방지합니다. 시스템은 하위 클래스가 재정의하지 않거나 구성을 반환하는 데 너무 오래 걸리는 경우 모든 메서드에 기본 모양을 제공합니다.


>참고 자료
[ApplicationToken](https://developer.apple.com/documentation/managedsettings/applicationtoken)
[bundleidentifier](https://developer.apple.com/documentation/managedsettings/application/bundleidentifier)
[ShieldConfigurationDataSource](https://developer.apple.com/documentation/managedsettingsui/shieldconfigurationdatasource)