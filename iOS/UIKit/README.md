아래 공식 문서와 서술한 순서가 같습니다.

[Apple Developer - UIKit](https://developer.apple.com/documentation/uikit)

# Index

> ## [User Interface](#user-interface)
- [Views and controls](#views-and-controls)
- [Container views](#container-views)
    + [UIView](#uiview)
    + [Collection views](#collection-views)
    + [Table views](#table-views)
    + UIStackView
    + UIScrollView
- [Content views](#content-views)
    + UIActivityIndicatorView
    + UICalendarView
    + [UIImageView](#uiimageview)
    + UIPickerView
    + UIProgressView
    + UIWebView
- [Controls](#controls)
    + UIControl
    + [UIButton](#uibutton)
    + UIColoerWell
    + UIDatePicker
    + UIPageControl
    + UISegmentControl
    + UISlider
    + UIStepper
    + UISwitch
- [Text views](#text-views)
    + UILabel
    + UITextField
    + UITextView
- [Search field](#search-field)
    + UISearchTextField
    
    
- [View controllers](#view-controllers)
    + UIViewController
    + UITableController
    + UICollectionViewController
    + [UINavigationController](#uinavigationcontroller)
 ----

<br>
<br>

> # User Interface
> ## Views and controls

<div>

## Container views

#### UIView
<details>
  <summary> 2022.12.28 UILabel or UIButton rotate 90 degrees, 180 degrees </summary>
  
  UILabel, UIButton은 모두 UIView를 Subclass하기 때문에 UIView에 위치했습니다.
  
  ```swift
     // 90 degrees
     exampleLabel.transform = CGAffineTransform(rotationAngle: CGFloat.pi / 2)

     // 180 degrees
     exampleLabel.transform = CGAffineTransform(rotationAngle: CGFloat.pi)
  ```
  
</details>

#### Collection views
<details>
  <summary> 2023.01.20 collectionView header 설정 </summary>
    // TODO: 블로그 포스팅
    1. create UICollectionReusableView
    2. regist UICollectionReusableView on CollectionView
    3. set size UICollectionReusableView on Flowlayout
  
</details>
    
#### Table views
<details>
  <summary> 2023.01.15 tableview didDeselectRowAt </summary>
    // TODO: 블로그 포스팅
    이건 블로그 링크도 대체해주자
  
</details>
#### UIStackView
#### UIScrollView

## Content views

<div>

#### UIActivityIndicatorView
#### UICalendarView

</div>

#### UIImageView
<details>
  <summary> 2023.01.03 .withRenderingMode(_ renderingMode: UIimage.RenderingMode) </summary>
  
  UIimageView에 같은 이미지에 여러 색상을 사용해야하는 일이 생겼다.
  
  디자이너에게 여러 색상의 이미지를 받았고, 색만 다른 중복 이미지가 쌓여가고있었다.
  
  하지만 기존 .withRenderingMode에 대해서 오해가 하나 있었다.
  
  SFSymbol 에 속한 Apple 기본 이미지만 가능한 줄 알았지만, 직접 등록한 Asset Image 파일도 사용 가능했다.
  
  ```swift
     
     let sampleImage = UIImage(named: "exampleImage").withRenderingMode(.alwaysTemplate)
     exampleImageView.image = sampleImage
     exampleImageView.tintColor = .systemRed
  ```
  
</details>

#### UIPickerView
#### UIProgressView
#### UIWebView

## Controls

#### UIControl

#### UIButton
<details>
  <summary> 2022.12.28 UIImage.SymbolConfiguration </summary>
  
  ```swift
     button.preferredSymbolConfigurationForImage(in: .normal)
     button.setPreferredSymbolConfiguration(UIImage.SymbolConfiguration(pointSize: 10), forImageIn: .normal)
  ```
  
</details>

#### UIColoerWell
#### UIDatePicker
#### UIPageControl
#### UISegmentControl
#### UISlider
#### UIStepper
#### UISwitch

### Text views

#### UILabel
#### UITextField
#### UITextView

### Search field

#### UISearchTextField
</div>

<br>
<br>

> ## View controllers

<div>

#### UIViewController
#### UITableController
#### UICollectionViewController
#### UINavigationController
<details>
  <summary> 2023.01.04 Swipe Back Gesture </summary>
  
  기존 앱에서는 push, pop 같은 수평을 이동하는 구조에서 Swipe를 통해 뒤로 돌아갈 수 있었다.
  
  그런데 간혹 내가 만든 화면에서는 스와이프로 이동이 되지않는 경우가 많았고, 해결하고 싶었다.
  
  ```swift
     // UINavigationController 기본 네비게이션 헤더 영역을 사용할 때
     self.navigationController?.interactivePopGestureRecognizer?.delegate = self
     
     // UINavigationController 커스텀 네비게이션 헤더 영역을 사용할 때
     self.navigationController?.interactivePopGestureRecognizer?.delegate = nil
     
  ```
</details>

</div>


> ## Core Location

### Requesting authorization to use location services

<details>
  <summary> 2023.01.10 위치 권한 얻기 init </summary>
  
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
</details>

> # Animation

<details>
  <summary> 2023.01.17 child to child transition </summary>
</details>


<br>
<br>
<br>

> # Menus and Shortcuts

<br>

> ## Home Screen Quick Actions

<br>

### UIApplicationShortcutItem

<details>
    <summary> 2023.02.03 UIApplicationShortcutItem Basic </summary>
     App icon을 Long press 할 때 나오는 Context menu
</details>