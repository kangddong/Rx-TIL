> ## Core Location

### Requesting authorization to use location services
#### 2023.01.10

위치 권한 얻기 init
  
1. info.plist에 NSLocationAlwaysAndWhenInUseUsageDescription, NSLocationWhenInUseUsageDescription 를 등록해줘야한다
  
그런데 간혹 내가 만든 화면에서는 스와이프로 이동이 되지않는 경우가 많았고, 해결하고 싶었다.
  
```swift
    
   func requestLocationManager() {
      if LocationUtil.getStateOfLocationPermission() == .notDetermined {
         self.locManager = CLLocationManager()
         locManager?.delegate = self
         // 서브 쓰레드로 해야함
          DispatchQueue.main.async {
             self.locManager?.requestAlwaysAuthorization()
          }
      }
   }   
  ```
