### 2023.01.03

## .withRenderingMode(_ renderingMode: UIimage.RenderingMode)
  
UIimageView에 같은 이미지에 여러 색상을 사용해야하는 일이 생겼다.
  
디자이너에게 여러 색상의 이미지를 받았고, 색만 다른 중복 이미지가 쌓여가고있었다.
  
하지만 기존 .withRenderingMode에 대해서 오해가 하나 있었다.
  
SFSymbol 에 속한 Apple 기본 이미지만 가능한 줄 알았지만, 직접 등록한 Asset Image 파일도 사용 가능했다.
  
```swift
     
  let sampleImage = UIImage(named: "exampleImage").withRenderingMode(.alwaysTemplate)
  exampleImageView.image = sampleImage
  exampleImageView.tintColor = .systemRed
```
