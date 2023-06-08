
# 설정 화면으로 이동 시키기

``` swift
if let url = URL(string: UIApplication.openSettingsURLString) {
	// Ask the system to open that URL.
	await UIApplication.shared.open(url)
}

// 설정 - 알림 화면으로 이동 시키기
if let url = URL(string: UIApplication.openNotificationSettingsURLString) {
	// Ask the system to open that URL.
	await UIApplication.shared.open(url)
}
```


# Safari로 이동 시키기

``` swift
if let url = URL(string: "www.apple.com") {
	// move web browser
	await UIApplication.shared.open(url)
}
```
