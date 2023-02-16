UILabel, UIButton은 모두 UIView를 Subclass하기 때문에 UIView에 위치했습니다.
  
```swift
   // 90 degrees
   exampleLabel.transform = CGAffineTransform(rotationAngle: CGFloat.pi / 2)

   // 180 degrees
   exampleLabel.transform = CGAffineTransform(rotationAngle: CGFloat.pi)
```
