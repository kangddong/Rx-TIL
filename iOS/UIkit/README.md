아래 공식 문서와 서술한 순서가 같습니다.

[Apple Developer - UIKit](https://developer.apple.com/documentation/uikit)

User Interface

## Views and controls

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
- Collection views
- Table views
- UIStackView
- UIScrollView

## Content views
- UIActivityIndicatorView
- UICalendarView
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
- UIPickerView
- UIProgressView
- UIWebView

## Controls
- UIControl

#### UIButton
<details>
  <summary> 2022.12.28 UIImage.SymbolConfiguration </summary>
  
  ```swift
     button.preferredSymbolConfigurationForImage(in: .normal)
     button.setPreferredSymbolConfiguration(UIImage.SymbolConfiguration(pointSize: 10), forImageIn: .normal)
  ```
  
</details>

- UIColoerWell
- UIDatePicker
- UIPageControl
- UISegmentControl
- UISlider
- UIStepper
- UISwitch

### Text views
- UILabel
- UITextField
- UITextView

### Search field
- UISearchTextField
- UISearchToken