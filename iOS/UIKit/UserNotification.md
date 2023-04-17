
# 알림 권한 요청하기

기존의 방식과 aync await 두 가지 방식 모두 작성한다.

**기존 방식**
```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: **Any**]?) -> Bool {
    // Override point for customization after application launch.
    let center = UNUserNotificationCenter.current()
    center.requestAuthorization(options: [.alert, .badge, .sound, .provisional]) { granted, error in

		if let error = error {
			print(error.localizedDescription)
		}

	}
    return true
}
```

async await 방식
```swift
func requestAuthorization() async throws -> Bool {
    let center = UNUserNotificationCenter.current()
    let granted = try await center.requestAuthorization(options: [.alert, .badge, .sound, .provisional])
    
    return granted
}

// AppDelegate에서는 이렇게 사용 가능하다.
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: **Any**]?) -> Bool {
    // Override point for customization after application launch.
    let notificationManager = NotificationManager.shared
    Task {
        try await notificationManager.requestAuthorization()
    }
    return true
}
```

# APNS 등록하기

```swift
func application(_ application: UIApplication,
				 didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
				 application.registerForRemoteNotifications()
}

```

Apple Push Notification service에 등록하는 프로세스를 시작하는 메소드이다.

등록이 성공하게되면, [`application:didRegisterForRemoteNotificationsWithDeviceToken:`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622958-application?language=objc) 

메소드를 호출하게되고 device token을 전달한다.

**Simulator**에서는 `registerForRemoteNotifications()` 호출하여도 [`application:didRegisterForRemoteNotificationsWithDeviceToken:`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622958-application?language=objc)
가 호출되지않는다.

# Push Scedule 만들기



# UNNotificationTrigger

-   [`UNTimeIntervalNotificationTrigger`](https://developer.apple.com/documentation/usernotifications/untimeintervalnotificationtrigger)
주의해야 할 점:  If this parameter is `true`, the value in the `timeInterval` parameter must be 60 seconds or greater.
```swift
func addScehdule() {

	let content = UNMutableNotificationContent()
	content.title = "Weekly Staff Meeting"
	content.body = "Every Tuesday at 2pm"
	
	// Create the trigger as a repeating event.
	let trigger = UNTimeIntervalNotificationTrigger(timeInterval: 5.0, repeats: false)
	let request = UNNotificationRequest(identifier: "identifier", content: content, trigger: trigger)
	
	center.add(request)

}
```


-   [`UNCalendarNotificationTrigger`](https://developer.apple.com/documentation/usernotifications/uncalendarnotificationtrigger)
-   [`UNLocationNotificationTrigger`](https://developer.apple.com/documentation/usernotifications/unlocationnotificationtrigger)
-   [`UNPushNotificationTrigger`](https://developer.apple.com/documentation/usernotifications/unpushnotificationtrigger)
 
 