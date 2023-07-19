
`Property List Key  NSAppTransportSecurity`

```xml
<key>NSAppTransportSecurity</key>
```
HTTP 연결의 기본 보안에 대한 변경 사항에 대한 설명


Apple 플랫폼에서 ATS(App Transport Security)라는 네트워킹 기능은 모든 앱과 앱 확장 프로그램의 개인 정보 보호 및 데이터 무결성을 향상시킵니다.

ATS(App Transport Security) 를 사용하려면 [URL Loading System](/iOS/NetworkInApp/URL_loading_system.md)(일반적으로 URL 세션 클래스 사용)을 사용하는 모든 HTTP 연결이 HTTPS를 사용해야 합니다. 또한 TLS(Transport Layer Security) 프로토콜에 의해 규정된 기본 서버 신뢰 평가를 보완하는 확장된 보안 검사를 수행합니다. ATS는 최소 보안 규격을 충족하지 못하는 연결을 차단합니다.


### NSAllowsArbitraryLoads

`Property List Key  NSAllowsArbitraryLoads`
모든 네트워크 연결에 대해 앱 전송 보안 제한이 비활성화되었는지 여부를 나타내는 Bool 값입니다.
모든 네트워크 연결 --> HTTP 연결을 허용하고자 할 때 사용

`NSExceptionDomains` 사전에 지정되지 않은 모든 도메인에 대해 `ATS(App Transport Security)` 제한을 사용하지 않으려면 이 키의 값을 `YES`로 설정합니다.
`NSExceptionDomains` 은 `NSAllowsArbitraryLoads` 키 값의 **영향을 받지않는다.** 

`ATS(App Transport Security)`를 사용 불가능으로 설정하면 보안되지 않은 HTTP 연결이 허용됩니다. HTTPS 연결도 허용되며 네트워크 서버가 최소 요구 사항을 충족하는지 확인에서 설명한 대로 기본 서버 신뢰도 평가 대상이지만 최소 `TLS(Transport Layer Security)` 프로토콜 버전 요구와 같은 확장 보안 검사는 실행 중지됩니다. `ATS(App Transport Security)`가 없으면 수동 서버 신뢰 인증 수행에 설명된 대로 기본 서버 신뢰 요구사항을 완화할 수도 있습니다

```xml
<key>NSAppTransportSecurity</key>
<dict>
	<key>NSAllowsArbitraryLoads</key>
	<true/>
</dict>
```

참고
[공식문서](https://developer.apple.com/documentation/bundleresources/information_property_list/nsapptransportsecurity/)