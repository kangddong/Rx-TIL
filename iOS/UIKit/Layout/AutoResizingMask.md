
AutoResizingMask의 개념은 2007년 UIKit의 초기 릴리스와 함께 도입되었으므로 iOS 개발 초기부터 사용할 수 있었습니다.

반면 Auto Layout 은 2012년에 출시된 iOS 6에서 도입되었습니다.


# Overview

superview의 bounds가 바뀔 때 수신기의 크기를 조정하는 방법을 결정하는 정수 비트 마스크.

Combining these constants lets you specify which dimensions of the view should grow or shrink relative to the superview. The default value of this property is `none`, which indicates that the view should not be resized at all. 

view's bounds가 변경되면, 그 view는 각 subview의 autoresizing mask에 따라 subviews의 크기를 자동으로 조정합니다. C 비트 OR 연산자를 사용하여 UIView.AutoresizingMask에 설명된 상수를 결합하여 이 마스크의 값을 지정합니다. 
이러한 상수를 결합하면 view의 어떤 dimensions(차원)이 superview에 비해 증가하거나 축소되어야 하는지 지정할 수 있습니다. 이 속성의 기본값은 none이며, 이는 보기의 크기를 전혀 조정해서는 안 된다는 것을 나타냅니다.

When more than one option along the same axis is set, the default behavior is to distribute the size difference proportionally among the flexible portions. The larger the flexible portion, relative to the other flexible portions, the more it is likely to grow. For example, suppose this property includes the [`flexibleWidth`](https://developer.apple.com/documentation/uikit/uiview/autoresizingmask/1622468-flexiblewidth) and [`flexibleRightMargin`](https://developer.apple.com/documentation/uikit/uiview/autoresizingmask/1622662-flexiblerightmargin)constants but does not include the `flexibleLeftMargin` constant, thus indicating that the width of the view’s left margin is fixed but that the view’s width and right margin may change. Thus, the view appears anchored to the left side of its superview while both the view width and the gap to the right of the view increase.

If the autoresizing behaviors do not offer the precise layout that you need for your views, you can use a custom container view and override its [`layoutSubviews()`](https://developer.apple.com/documentation/uikit/uiview/1622482-layoutsubviews) method to position your subviews more precisely.



같은 축을 따라 하나 이상의 옵션이 설정되면, 기본 동작은 유연한 부분에 비례하여 크기 차이를 분배하는 것입니다. 다른 유연한 부분에 비해 유연한 부분이 클수록, 더 많이 자랄 가능성이 높다. 예를 들어, 이 속성은 flexibleWidth와 flexibleRightMargin 상수를 포함하지만 flexibleLeftMargin 상수를 포함하지 않으므로 뷰의 왼쪽 여백의 너비가 고정되어 있지만 뷰의 너비와 오른쪽 여백이 변경될 수 있음을 나타냅니다. 따라서, 뷰는 뷰 너비와 뷰 오른쪽의 간격이 모두 증가하는 동안 superview의 왼쪽에 고정되어 있는 것처럼 보인다.

자동 크기 조정 동작이 뷰에 필요한 정확한 레이아웃을 제공하지 않는 경우, 사용자 지정 컨테이너 뷰를 사용하고 layoutSubviews() 메서드를 재정의하여 하위 뷰를 더 정확하게 배치할 수 있습니다.



- **None (`UIViewAutoresizingNone`):** 이는 슈퍼뷰의 프레임 변경에 따라 뷰의 크기나 위치가 변경되지 않아야 함을 나타냅니다.
- **Flexible left margin(`UIView.AutoresizingMask.flexibleLeftMargin`):** 보기의 왼쪽 여백은 슈퍼뷰의 너비가 변경될 때 자동으로 조정됩니다. 뷰는 수퍼 뷰의 왼쪽 가장자리를 기준으로 위치를 유지합니다.
- **Flexible width(`UIView.AutoresizingMask.flexibleWidth`):** 뷰의 너비는 슈퍼뷰의 너비와 일치하도록 자동으로 조정됩니다. 뷰는 수퍼 뷰의 가장자리를 기준으로 왼쪽 또는 오른쪽 위치를 유지합니다.
- **Flexible right margin(`UIView.AutoresizingMask.flexibleRightMargin`):** 보기의 오른쪽 여백은 슈퍼뷰의 너비가 변경될 때 자동으로 조정됩니다. 뷰는 수퍼 뷰의 오른쪽 가장자리를 기준으로 위치를 유지합니다.
- **Flexible top margin(`UIView.AutoresizingMask.flexibleTopMargin`):** 슈퍼뷰의 높이가 변경되면 보기의 위쪽 여백이 자동으로 조정됩니다. 뷰는 수퍼 뷰의 상단 가장자리를 기준으로 위치를 유지합니다.
- **Flexible height(`UIView.AutoresizingMask.flexibleHeight`):** 뷰의 높이는 슈퍼뷰의 높이와 일치하도록 자동으로 조정됩니다. 뷰는 수퍼 뷰의 가장자리를 기준으로 위쪽 또는 아래쪽 위치를 유지합니다.
- **Flexible bottom margin(`UIView.AutoresizingMask.flexibleBottomMargin`):** 뷰의 아래쪽 여백은 슈퍼뷰의 높이가 변경될 때 자동으로 조정됩니다. 뷰는 수퍼 뷰의 아래쪽 가장자리를 기준으로 위치를 유지합니다.


공식 문서 번역 중 내가 모르는 단어들
- 비트 마스크