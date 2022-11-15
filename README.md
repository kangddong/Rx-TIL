# Rx's TIL

## 목차
- [Swift](##Swift)
- [iOS](##iOS)
----

<div align=center>

## Swift
</div>

문법에 대한 정리는 [이곳](Swift/README.md)

꼼꼼한 재은씨 기본편/실전편 스터디에 대한 자료는 [이곳](LetsSwiftyStudy.md)

----
<div align=center>

## iOS

</div>

* [UIKit](iOS/UIKit/README.md) 프레임워크에 있는 클래스들의 개념과 사용해보면서 알게 된 내용 정리

----
<div align=center>

## Trouble Shooting
</div>

트러블슈팅에 대한 원인 및 해결 과정을 적었습니다.

<details>
<summary> 2022.11.02 - Push를 통한 화면전환 구조 변경 간 발생한 SideEffect </summary>
AS-IS 푸시가 없었음, 그래서 푸시로 인한 화면 전환 로직이 없음
ParentsViewController -> MainNavi -> MainViewController의 형태였음
ParentsViewController -> NotiViewController로의 이동 간 VC <-> UINavigationController 전환이 어려운 상황

TO-BE 

[new]ParentsNavi -> ParentsViewController -> MainNavi -> MainViewController의 형태로 변경 -> 푸시 화면 전환 성공

- Side Effect 발생

-> MainViewController에서 SideMenu가 import 된 MenuViewController를 performSegue로 호출을 할 때 MainViewController가 사라짐

- 원인

***여기서 seugue의 종류가 show로 되어있었음 -> present로 수정

UIViewController에서는 화면 전환을 present, dismiss 호출하여 사용가능하며, UINavigationController의 화면 전환 메소드는 사용할 수 없다

UINavigationController에서는 화면 전환을 push, pop 호출하여 사용가능하며, UIViewController의 화면 전환 메소드는 사용할 수 없다

- 해결

show의 특성은 호출하는 클래스에 맞춰서 화면 전환을 해준다.호출하는 화면의 클래스가 UINavigationController였기 때문에 SideMenu View를 push 해줬기에 Side Effect가 발생하였다
segue를 끊고 화면 전환 코드를 작성해도 되었지만, 기존 코드를 살려 segue의 종류를 show -> present Modally 변경해주었다
</details>

<details>
<summary> 2022.11.08 Xcode 14 cocoapods pod init이 되지않은 경우</summary>

[블로그 포스팅 대체](https://plcprogrammer-dy.tistory.com/78)
</details>
