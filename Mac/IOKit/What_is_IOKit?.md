
I/O 키트 개발자에는 두 가지 일반적인 유형이 있으며 이 문서는 두 가지 모두에 유용하도록 노력합니다.
유형은 아래와 같습니다.
* 커널에 상주할 장치 드라이버를 만드는 개발자입니다.
* I/O 키트 장치 인터페이스를 사용하여 하드웨어와 통신하는 응용 프로그램 개발자

앱과 서비스에서 하드웨어 장치와 드라이버에 액세스하세요.

IOKit 프레임워크는 `device-interface mechanism`을 통해 `drivers`와 `nubs`와 같은 `IOKit` 객체에 대한 `nonkernel` 액세스를 구현합니다.

macOS 11 이상에서 지원되는 장치에는 DriverKit이 필요합니다.
앱과 서비스에서 IOKit을 사용하여 장치를 발견하고 사용하세요.


## I/O Kit 기능
- 동적 및 자동 장치 구성(플러그 앤 플레이)
- 다음을 포함한 많은 새로운 유형의 장치그래픽 가속 및멀티미디어 장치
- 전원 관리(예: "절전" 모드)
- 커널의 보호 메모리 시행 - 커널과 사용자 프로그램을 위한 별도의 주소 공간
- 선제적 멀티태스킹
- 대칭 다중 처리
- 장치 유형 간에 공유되는 공통 추상화
- 향상된 개발 경험 - 새 드라이버는 작성하기 쉬워야 합니다.


## I/O Kit 제한 사항
I/O 키트는 대부분의 유형을 지원하지만OS X 시스템의 하드웨어에서는 모든 하드웨어를 완전히 지원하지 않습니다. 그러한 장치의 한 범주는 다음에 사용되는 장치입니다.그 중에서도 이미징프린터,스캐너 및디지털 카메라. I/O 키트는 FireWire 및 USB 제품군을 통해 이러한 장치와의 통신을 처리하면서 이러한 장치에 대한 제한된 지원만 제공합니다.

## I/O Kit의 언어는 C ++ 입니다


보통 우리가 말하는 Computer에서 IO는 Input/Output(입출력) 장치들을 뜻한다.
자세한 내용은 [IO란 무엇일까 ?](CS/What_is_IO?) 에서 확인할 수있다.

