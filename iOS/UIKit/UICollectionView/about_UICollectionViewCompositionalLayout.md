

# NSCollectionLayoutSection
# NSCollectionLayoutGroup
# NSCollectionLayoutItem

```swift
@NSCopying
var edgeSpacing: NSCollectionLayoutEdgeSpacing? { get set }
```

이 속성을 사용하여 컨테이너 및 기타 항목과 관련하여 항목의 위치를 조정하십시오. 예를 들어, 이 속성을 사용하여 각 항목의 trailing edge에 추가 공간을 적용할 수 있습니다. `contentInsets`를 적용하기 전에 `edgeSpacing`이 적용됩니다.

```swift
var contentInsets: NSDirectionalEdgeInsets { get set }
```

그리드 레이아웃 내에서 이 속성을 사용하여 각 항목의 각 가장자리 주위에 균일한 간격을 적용할 수 있습니다. 콘텐츠 삽입물은 `edgeSpacing`을 적용한 후에 적용됩니다.

다음 다이어그램은 그룹의 각 항목의 각 가장자리에 2점의 콘텐츠 삽입을 적용한 결과를 보여줍니다.

이 속성의 값은 차원에 대한 `estimated(_:)`을 사용하는 모든 축에 대해 무시됩니다. 


<img src = "https://docs-assets.developer.apple.com/published/ed6f3751fc/NSCollectionLayoutItem-contentInsets~dark@2x.png">


출처
[공식문서 - UICollectionViewCompositionalLayout](https://developer.apple.com/documentation/uikit/uicollectionviewcompositionallayout)
[공식문서 - NSCollectionLayoutItem](https://developer.apple.com/documentation/uikit/nscollectionlayoutitem)
[공식문서 - NSCollectionLayoutGroup](https://developer.apple.com/documentation/uikit/nscollectionlayoutgroup)
[공식문서 - NSCollectionLayoutSection](https://developer.apple.com/documentation/uikit/nscollectionlayoutsection)