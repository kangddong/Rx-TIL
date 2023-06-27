
[FlexLayout](https://github.com/layoutBox/FlexLayout)

야무지게 정리해보기

Flex

1. container를 Setup 해야한다.
2. container를 Layout 해야한다.





## ScrollView+

[PinLayout에서 pin 메소드를 통해 사용법 설명 대체](PinLayout.md)


``` swift

// 기존 UI
// SnapKit으로 되어있는 커스텀 네비게이션 뷰
@IBOutlet weak var commonNaviView: CommonNaviView!
...

override func viewDidLayoutSubviews() {
    super.viewDidLayoutSubviews()

    // How to pin 2-way
    
    // way 1 - 기존 뷰를 살리고 하는 방법 네비 하단에 붙이기 위해 pin의 위치를 적절하게 잡아준다
    contentsView.pin
        .top(commonNaviView.frame.height)
        .bottom(view.pin.safeArea.bottom)
        .left(view.pin.safeArea.left)
        .right(view.pin.safeArea.right)
    
    // way 2 - view에 pin를 하는 방법이기에 기존 commonNaviView 가 가려진다.
    contentsView.pin.all(view.pin.safeArea)
    contentsView.flex.layout()
    contentsView.contentSize = rootFlexContainer.frame.size

}
```