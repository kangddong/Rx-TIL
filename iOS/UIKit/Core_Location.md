# Core Location

#### 2023.01.10

# 1. 위치 권한 얻기 init
  
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


# 2. 요청 권한 확인

[CLAuthorizationStatus](https://developer.apple.com/documentation/corelocation/clauthorizationstatus)

```swift
func locationManagerDidChangeAuthorization(_ manager: CLLocationManager) { 
    switch manager.authorizationStatus {
        case .authorizedWhenInUse: // Location services are available. 
            enableLocationFeatures()
            break
        case .restricted, .denied: // Location services currently unavailable. 
            disableLocationFeatures()
            break
        case .notDetermined: // Authorization not determined yet. 
            manager.requestWhenInUseAuthorization()
            break
        default:
            break
    }
}
```

위와 같은 경우에 `manager.authorizationStatus` 에서 print CLAuthorizationStatus(rawValue:)
# 위치권한 요청
- 위치권한 요청은 1회만 가능하다.

참고자료
[Requesting authorization to use location services](https://developer.apple.com/documentation/corelocation/requesting_authorization_to_use_location_services)
