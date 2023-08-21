

# 앱의 scheme 호출을 통한 앱을 깨우는 법


your-scheme의 scheme를 가진 앱 A를 앱 B에서 깨우기 위한 코드이다.

```swift
let schemeURL = "your-scheme://"

 if let url = URL(string: schemeURL) {
	print("URL init success !!")

	if UIApplication.shared.canOpenURL(url) {
		print("open success !!")
		UIApplication.shared.open(url)
	} else {
		print("open fail !!")
	}
} else {
	print("URL init fail !!")
}
```


실행을 해보면 우린 이러한 에러를 만나볼 수 있다.

> -canOpenURL: failed for URL: "**your-scheme**://" - error: "This app is not allowed to query for scheme **your-scheme**"


B 앱의 info.plist에 A 앱의 scheme이 없어서 생긴 문제이다

Property List Key 값: Queried URL Schemes
XML Key 값: LSApplicationQueriesSchemes


```xml
<key>LSApplicationQueriesSchemes</key>
<array>
	<string>your-scheme</string>
</array>
```

