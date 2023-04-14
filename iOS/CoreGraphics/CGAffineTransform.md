

## CGAffineTransform 통한 UIVIew Rotate

```swift
let angle: CGFloat = barcodeInfoView.transform.a == 1.0 ? 90 : -90
let radians = angle / 180.0 * CGFloat.pi

barcodeInfoView.transform = CGAffineTransformRotate(barcodeInfoView.transform, radians)

barcodeInfoView.transform = barcodeInfoView.transform.rotated(by: radians)
```