

# stroke와 fill color 넣는 법
UIColor의 `setFill()`, `setStroke()` 메소드를 이용한다.

```swift
// After Initialized UIBezierPath 
let arc = UIBezierPath(arcCenter: arcCenter,
                               radius: radius,
                               startAngle: radAngleRange.lowerBound,
                               endAngle: radAngleRange.upperBound,
                               clockwise: true)
arc.lineWidth = 1


// Fill
UIColor.green.setFill()
ovalPath.fill()

// Stroke
UIColor.lightGray.setStroke()

// Before stroke()
arc.stroke()
```