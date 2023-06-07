
`WidgetKit`는 WWDC 2020 [Meet WidgetKit](https://developer.apple.com/videos/play/wwdc2020/10028/)를 통해서 소개되었다.
`iOS 14.0+, iPadOS 14.0+, masOS 11.0+, Mac Catalyst 14.0+ watchOS 9.0+` 에서 사용할 수 있다

`WidgetKit`로 사용 가능한 것은 현재 4가지이다.
* Widgets
* Smart Stacks
* Watch complications
* Live Activites


## Widgets
앱을 실행하지 않고도 특정 앱 기능을 제공합니다.
iPhone과 iPad에서 사람들은 Today View, 홈 화면 및 잠금 화면에 위젯을 배치합니다.
Mac에서, 사람들은 데스크톱과 알림 센터에 네이티브 Mac 앱 위젯을 둔다. 
iOS 17과 macOS 14부터 사람들은 Mac 데스크톱과 알림 센터에 iPhone 위젯을 배치할 수도 있습니다. 
Apple Watch에서 위젯은 스마트 스택에 나타납니다.

## Smart Stacks
iPhone에서, 사람들은 위젯을 쌓고 스마트 스택을 만든다. 스마트 스택에서 `WidgetKit`은 `Smart Rotate`을 위한 `App Intents` 프레임워크에서 제공하는 온디바이스 인텔리전스와 기능을 사용합니다.
`Smart Rotate`은 사람의 현재 상황에 맞는 스택 상단에 위젯을 표시합니다. 
Apple Watch에서 사람들은 위젯을 스마트 스택에 배치하고 고정된 위치에 고정하거나 시스템이 사람의 상황에 가장 잘 맞도록 정렬하도록 할 수 있습니다.

## Watch complications

사람들은 손목을 들어 올릴 때 시기적절하고 관련 있는 정보를 보기 위해 Apple Watch 얼굴에 `watch complications`을 놓습니다. 또한, Apple Watch의 스마트 스택은 최대 세 가지 합병증을 위한 공간을 제공합니다.

## Live Activites

`Live Activities`은 잠금 화면이나 다이나믹 아일랜드의 이벤트 및 작업 정보와 같은 앱의 최신 콘텐츠를 표시합니다. 
`Live Activities`은 업데이트를 위해 `ActivityKit`을 사용하고 선택적으로 Apple 푸시 알림 서비스(APNs)를 사용하여 `ActivityKit` 푸시 알림을 보냅니다. 