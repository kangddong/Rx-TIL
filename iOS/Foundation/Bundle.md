

iOS 디스크의 번들 디렉토리에 저장된 코드와 리소스의 표현

Bundle이 뭐지?

Apple은 번들을 사용하여 앱, 프레임워크, 플러그인 및 기타 여러 특정 유형의 콘텐츠를 나타냅니다.

번들은 포함된 리소스를 잘 정의된 하위 디렉터리로 구성하며 번들 구조는 플랫폼 및 번들 유형에 따라 다릅니다. 
번들 개체를 사용하면 번들의 구조를 몰라도 번들의 리소스에 액세스할 수 있습니다.
번들 개체는 번들 구조, 사용자 기본 설정, 사용 가능한 현지화 및 기타 관련 요소를 고려하여 항목을 찾기 위한 단일 인터페이스를 제공합니다.

모든 실행 파일은 번들 개체를 사용하여 앱의 번들 내부 또는 다른 위치에 있는 알려진 번들에서 리소스를 찾을 수 있습니다. 컨테이너 디렉터리 또는 파일 시스템의 다른 부분에서 파일을 찾기 위해 번들 개체를 사용하지 않습니다.

번들 객체를 사용하는 일반적인 패턴은 다음과 같습니다.

1.  원하는 번들 디렉터리에 대한 번들 개체를 만듭니다.
    
2.  번들 개체의 메서드를 사용하여 필요한 리소스를 찾거나 로드합니다.
    
3.  다른 시스템 API를 사용하여 리소스와 상호 작용합니다.
    

자주 사용하는 일부 유형의 리소스는 번들 없이 찾아서 열 수 있습니다. 
예를 들어 이미지를 로드할 때 이미지를 자산 카탈로그에 저장하고 그리고
`UIImage` 혹은 `NSImage` `init(named:)`의 메소드를 사용하여 로드합니다 . 
마찬가지로 문자열 리소스의 경우 `NSLocalizedString`를 사용하여 전체 `.strings` 파일을 직접 로드하는 대신 개별 문자열을 로드합니다.


해당 Core Foundation 이름(예: `NSString`및 `CFString` 이 있는 일부 다른 `Foundation` 클래스와 달리 `Bundle`개체는  `CFBundle`  참조로 캐스팅할 수 없습니다 . 
`CFBundle` 에서 제공하는 기능이 필요한 경우 `CFBundle`  API를 생성 하고 사용할 수 있습니다 . 
자세한 내용은 [Toll-Free Bridging](https://developer.apple.com/library/archive/documentation/General/Conceptual/CocoaEncyclopedia/Toll-FreeBridgin/Toll-FreeBridgin.html#//apple_ref/doc/uid/TP40010810-CH2) 참조하십시오 .




# CFBundleShortVersionString, CFBundleVersion


```swift
Bundle.main.infoDictionary?["CFBundleShortVersionString"] as? String ?? "0.0"
```

## infoDictionary

```swift
var infoDictionary: [String : Any]? { get }
```

번들이 .`Info.plist` 파일을 포함하지 않는 경우,
이 사전에는 `Bundle class`에서 내부적으로 사용되는 `private key`만 포함됩니다. 
`Bundle class` 는 자체 사용을 위해 이 사전에 추가 키를 추가할 수 있습니다. 
사전 값에 액세스하기 위한 공통 키는 `CFBundleIdentifier`, `NSMainNibFile`, `NSPrincipalClass`  입니다 

## CFBundleVersion

The version of the build that identifies an iteration of the bundle.

This key is a 10.14.1과 같이 마침표로 구분된 1-3개의 정수로 구성된 시스템에서 읽을 수 있는 문자열입니다. 문자열은 숫자(0-9)와 마침표만 포함할 수 있습니다.

각 정수는 빌드 버전에 대한 정보를 아래와 같은 형식으로 제공한다 
 [_Major_].[_Minor_].[_Patch_]:

-   Major: A major revision number. 
    
-   Minor: A minor revision number. 
    
-   Patch: A maintenance release number.
    

You can include more integers but the system ignores them.

한 개 또는 두 개의 정수만 사용하여 빌드 버전을 축약할 수도 있습니다. 여기서 형식에 누락된 정수는 0으로 해석됩니다. 예를 들어 0은 0.0.0, 10은 10.0.0, 10.5는 10.5.0을 지정합니다.

이 키는 App Store에 필요하며 시스템 전체에서 빌드 버전을 식별하는 데 사용됩니다

## CFBundleShortVersionString

The release or version number of the bundle.
