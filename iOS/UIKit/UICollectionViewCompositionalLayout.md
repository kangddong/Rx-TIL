

## orthogonalScrollingBehavior

The section’s scrolling behavior in relation to the main layout axis.
메인 레이아웃 축과 관련된 섹션의 스크롤 동작.

 which means the section lays out its content along the main axis of its layout, defined by the layout configuration’s [`scrollDirection`](https://developer.apple.com/documentation/uikit/uicollectionviewcompositionallayoutconfiguration/3199222-scrolldirection) property. Set a different value for this property to get the section to lay out its content orthogonally to the main layout axis.

이 속성의 기본값은 `UICollectionLayoutSectionOrthogonalScrollingBehavior.none`이며,
이는 섹션이 레이아웃 구성의 `scrollDirection` 속성에 의해 정의된 레이아웃의 주축을 따라 콘텐츠를 배치한다는 것을 의미합니다.
이 속성에 대해 다른 값을 설정하여 섹션이 메인 레이아웃 축에 직각으로 내용을 배치하도록 합니다.

```swift
@available(iOS 13.0, *)

public enum UICollectionLayoutSectionOrthogonalScrollingBehavior : Int, @unchecked Sendable {

    // 기본 동작. Section will layout along main layout axis (i.e. configuration.scrollDirection)
	case none = 0
    
    // NOTE: For each of the remaining cases, the section content will layout orthogonal to the main layout axis (e.g. main layout axis == .vertical, section will scroll in .horizontal axis)

    // Standard scroll view behavior: UIScrollViewDecelerationRateNormal
    case continuous = 1

    // Scrolling will come to rest on the leading edge of a group boundary
    case continuousGroupLeadingBoundary = 2

    // Standard scroll view paging behavior (UIScrollViewDecelerationRateFast) with page size == extent of the collection view's bounds
    case paging = 3

    // Fractional size paging behavior determined by the sections layout group's dimension
    case groupPaging = 4

    // Same of group paging with additional leading and trailing content insets to center each group's contents along the orthogonal axis
    case groupPagingCentered = 5

}
```



https://velog.io/@sopt_official/iOS1 - 기본 개념 매우 좋음