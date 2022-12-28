아래 공식 문서와 서술한 순서가 같습니다.

[Apple Developer - UIKit](https://developer.apple.com/documentation/uikit)

User Interface

## Views and controls

## Container views
#### UIView
<details>
  <summary> UILabel or UIButton rotate 90 degrees, 180 degrees </summary>
  
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
- UIImageView
- UIPickerView
- UIProgressView
- UIWebView

## Controls
- UIControl

#### UIButton
<details>
  <summary> UIImage.SymbolConfiguration </summary>
  
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
