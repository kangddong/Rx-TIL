


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