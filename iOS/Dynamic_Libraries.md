
앱의 성능을 결정하는 두 가지 중요한 요소는 실행 시간과 메모리 사용량입니다. 앱 실행 파일의 크기를 줄이고 실행 후 메모리 사용을 최소화하면 앱 실행 속도가 빨라지고 실행 후 메모리 사용량이 줄어듭니다. 정적 라이브러리 대신 동적 라이브러리를 사용하면 앱의 실행 파일 크기가 줄어듭니다. 또한 앱이 실행 시간이 아닌 필요할 때만 특수 기능이 있는 라이브러리 로드를 지연할 수 있습니다. 이 기능은 실행 시간 단축과 효율적인 메모리 사용에 더욱 기여합니다.

이 기사에서는 동적 라이브러리를 소개하고 정적 라이브러리 대신 동적 라이브러리를 사용하여 이를 사용하는 앱의 파일 크기와 초기 메모리 사용량을 줄이는 방법을 보여줍니다. 이 문서에서는 앱이 런타임에 동적 라이브러리로 작업하는 데 사용하는 동적 로더 호환성 기능에 대한 개요도 제공합니다.

## 동적 라이브러리란 무엇입니까?

대부분의 앱 기능은 실행 가능한 코드 라이브러리에서 구현됩니다. 앱이 정적 링커를 사용하여 라이브러리와 연결되면 앱이 사용하는 코드가 생성된 실행 파일에 복사됩니다. 정적 _링커는_ 개체 코드로 알려진 컴파일된 소스 코드와 라이브러리 코드를 런타임 시 전체가 메모리에 로드되는 하나의 실행 파일로 수집합니다. 앱 실행 파일의 일부가 되는 종류의 라이브러리를 정적 라이브러리라고 합니다. _정적 라이브러리는_ 개체 파일의 모음 또는 아카이브입니다.

**참고: 정적 라이브러리는** _정적 아카이브 라이브러리_ 및 _정적 링크 공유 라이브러리_  라고도 합니다 .

앱이 시작되면 연결된 정적 라이브러리의 코드를 포함하는 앱의 코드가 앱의 주소 공간에 로드됩니다. 많은 정적 라이브러리를 앱에 연결하면 큰 앱 실행 파일이 생성됩니다. 그림 1정적 라이브러리에 구현된 기능을 사용하는 앱의 메모리 사용량을 보여줍니다. 큰 실행 파일이 있는 응용 프로그램은 시작 시간이 느리고 메모리 사용량이 많습니다. 또한 정적 라이브러리가 업데이트되면 해당 클라이언트 앱은 향상된 기능을 이용할 수 없습니다. 향상된 기능에 액세스하려면 앱 개발자가 앱의 개체 파일을 새 버전의 라이브러리와 연결해야 합니다. 그리고 앱 사용자는 앱 사본을 최신 버전으로 교체해야 합니다. 따라서 정적 라이브러리에서 제공하는 최신 기능을 사용하여 앱을 최신 상태로 유지하려면 개발자와 최종 사용자 모두에게 방해가 되는 작업이 필요합니다

![[address_space1_2x 1.png]]


더 나은 접근 방식은 실행 시 또는 런타임에 앱이 실제로 필요할 때 주소 공간에 코드를 로드하는 것입니다. 이러한 유연성을 제공하는 라이브러리 유형을 _동적 라이브러리_ 라고 합니다 . 동적 라이브러리는 클라이언트 앱에 정적으로 연결되지 않습니다. 실행 파일의 일부가 되지 않습니다. 대신 앱이 실행될 때 또는 실행될 때 동적 라이브러리를 앱에 로드(및 연결)할 수 있습니다.

**참고: 동적 라이브러리는** _동적 공유 라이브러리_ , _공유 객체_ 또는 _동적으로 연결된 라이브러리_  라고도 합니다 .

그림 2는 일부 기능을 정적 라이브러리 대신 동적 라이브러리로 구현하여 실행 후 앱에서 사용하는 메모리를 줄이는 방법을 보여줍니다.

![[address_space2_2x.png]]

동적 라이브러리를 사용하면 라이브러리에 대한 링크가 정적이 아니라 동적이기 때문에 프로그램에서 자동으로 사용하는 라이브러리의 개선 사항을 활용할 수 있습니다. 즉, 앱 개발자가 앱을 다시 컴파일하지 않고도 클라이언트 앱의 기능을 개선하고 확장할 수 있습니다. OS X용으로 작성된 앱은 OS X의 모든 시스템 라이브러리가 동적 라이브러리이기 때문에 이 기능이 유용합니다. 이것이 Carbon 또는 Cocoa 기술을 사용하는 앱이 OS X의 개선으로 얻는 이점입니다.

동적 라이브러리가 제공하는 또 다른 이점은 로드 시 초기화할 수 있고 클라이언트 앱이 정상적으로 종료될 때 정리 작업을 수행할 수 있다는 것입니다. 정적 라이브러리에는 이 기능이 없습니다. 자세한 내용은 [모듈 이니셜라이저 및 파이널라이저를](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/DynamicLibraries/100-Articles/DynamicLibraryDesignGuidelines.html#//apple_ref/doc/uid/TP40002013-SW17) 참조하십시오 .

동적 라이브러리를 개발할 때 개발자가 염두에 두어야 할 한 가지 문제는 라이브러리가 업데이트될 때 클라이언트 앱과의 호환성을 유지하는 것입니다. 클라이언트 앱의 개발자 모르게 라이브러리를 업데이트할 수 있기 때문에 앱은 코드를 변경하지 않고 새 버전의 라이브러리를 사용할 수 있어야 합니다. 이를 위해 라이브러리의 API는 변경되지 않아야 합니다. 그러나 개선을 위해 API 변경이 필요한 경우가 있습니다. 이 경우 클라이언트 앱이 제대로 실행되려면 이전 버전의 라이브러리가 사용자 컴퓨터에 남아 있어야 합니다. [동적 라이브러리 설계 지침은](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/DynamicLibraries/100-Articles/DynamicLibraryDesignGuidelines.html#//apple_ref/doc/uid/TP40002013-SW19) 동적 라이브러리가 발전함에 따라 클라이언트 앱과의 호환성 관리 주제를 탐구합니다.

## 동적 라이브러리 사용 방법

앱이 시작되면 OS X 커널은 앱의 코드와 데이터를 새 프로세스의 주소 공간에 로드합니다. 커널은 또한 동적 로더( `/usr/lib/dyld`)를 프로세스에 로드하고 제어를 전달합니다. 그런 다음 동적 로더는 앱의 _종속 라이브러리를_ 로드합니다 . 앱이 연결된 동적 라이브러리입니다. 정적 링커는 앱이 연결될 때 각 종속 라이브러리의 파일 이름을 기록합니다. 이 파일 이름은 동적 라이브러리의 _설치 이름 으로 알려져 있습니다._. 동적 로더는 앱의 종속 라이브러리 설치 이름을 사용하여 파일 시스템에서 찾습니다. 동적 로더가 실행 시 모든 앱의 종속 라이브러리를 찾지 못하거나 라이브러리 중 하나라도 앱과 호환되지 않는 경우 실행 프로세스가 중단됩니다. 종속 라이브러리 호환성에 대한 자세한 내용은 [종속 라이브러리와의 클라이언트 호환성 관리를](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/DynamicLibraries/100-Articles/DynamicLibraryDesignGuidelines.html#//apple_ref/doc/uid/TP40002013-SW20) 참조하십시오 . 동적 라이브러리 개발자는 옵션을 사용하여 라이브러리를 컴파일할 때 라이브러리에 대해 다른 설치 이름을 설정할 수 있습니다 `gcc -install_name`. 자세한 내용은 매뉴얼 페이지를 참조하십시오 `gcc`.

동적 로더는 실행 프로세스 중에 앱이 실제로 사용하는 정의되지 않은 외부 기호만 해결합니다. 다른 기호는 앱에서 사용할 때까지 확인되지 않은 상태로 유지됩니다. 앱이 실행될 때 동적 로더가 진행하는 프로세스에 대한 자세한 내용은 Mach- _[O 프로그래밍 항목의 "Mach-](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/MachOTopics/0-Introduction/introduction.html#//apple_ref/doc/uid/TP40001519)_ [O 파일 실행](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/MachOTopics/1-Articles/executing_files.html#//apple_ref/doc/uid/TP40001829) " 을 참조하십시오 ._[](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/MachOTopics/0-Introduction/introduction.html#//apple_ref/doc/uid/TP40001519)_

동적 로더는 시작 시 동적 라이브러리를 자동으로 로드하는 것 외에도 앱의 요청에 따라 런타임에 동적 라이브러리를 로드합니다. 즉, 앱이 실행될 때 동적 라이브러리를 로드할 필요가 없는 경우 개발자는 앱의 개체 파일을 동적 라이브러리와 연결하지 않고 대신 앱의 일부에서만 동적 라이브러리를 로드하도록 선택할 수 있습니다. 그것을 요구합니다. 이러한 방식으로 동적 라이브러리를 사용하면 시작 프로세스의 속도가 빨라집니다. _런타임에 로드되는 동적 라이브러리를 동적으로 로드되는 라이브러리_ 라고 합니다 . 런타임 시 라이브러리를 로드하기 위해 앱은 실행 중인 플랫폼의 동적 로더와 상호 작용하는 함수를 사용할 수 있습니다.

**참고:**  클라이언트와 동적 라이브러리의 대상 아키텍처는 동일해야 합니다. 그렇지 않으면 동적 로더가 라이브러리를 로드하지 않습니다.

플랫폼마다 동적 로더를 다르게 구현합니다. 또한 플랫폼 간에 코드를 이식하기 어렵게 만드는 사용자 지정 동적 코드 로딩 인터페이스가 있을 수 있습니다. 예를 들어 UNIX에서 Linux로 앱을 쉽게 포팅하기 위해 Jorge Acereda와 Peter O'Gorman은 _동적 로더 호환성(DLC)_ 기능을 개발했습니다. 개발자에게 앱에서 동적 라이브러리를 사용할 수 있는 표준적이고 이식 가능한 방법을 제공합니다.

DLC 함수는 에서 선언됩니다 `/usr/include/dlfcn.h`. 다섯 가지가 있습니다.

- `dlopen(3) OS X Developer Tools Manual Page`: 동적 라이브러리를 엽니다. 앱은 라이브러리의 내보낸 기호를 사용하기 전에 이 함수를 호출합니다. 동적 라이브러리가 현재 프로세스에 의해 열리지 않은 경우 라이브러리는 프로세스의 주소 공간에 로드됩니다. `dlsym`이 함수는 및 에 대한 호출에서 열린 라이브러리를 참조하는 데 사용되는 핸들을 반환합니다 `dlclose`. _이 핸들을 동적 라이브러리 핸들_ 이라고 합니다 . `dlopen`이 함수는 현재 프로세스가 특정 동적 라이브러리를 여는 데 사용한 횟수를 나타내는 참조 횟수를 유지합니다 .
    
- `dlsym(3) OS X Developer Tools Manual Page`: 동적으로 로드된 라이브러리에서 내보낸 심볼의 주소를 반환합니다. 앱은 에 대한 호출을 통해 라이브러리에 대한 핸들을 얻은 후 이 함수를 호출합니다 `dlopen`. 이 `dlsym`함수는 반환된 핸들 `dlopen`또는 기호 검색 범위와 기호 이름을 지정하는 상수를 매개 변수로 사용합니다.
    
- `dladdr(3) OS X Developer Tools Manual Page`: 제공된 주소에 대한 정보를 반환합니다. 주소가 앱의 주소 공간 내에서 동적으로 로드된 라이브러리에 해당하는 경우 이 함수는 주소에 대한 정보를 반환합니다. `Dl_info`이 정보 는 동적 라이브러리의 경로 이름, 라이브러리의 기본 주소, 제공된 주소에 가장 가까운 심볼의 주소 및 값을 캡슐화하는 구조로 반환됩니다 . 제공된 주소에서 동적 라이브러리를 찾을 수 없는 경우 함수는 정보를 반환하지 않습니다.
    
- `dlclose(3) OS X Developer Tools Manual Page`: 동적으로 로드된 라이브러리를 닫습니다. 이 함수는 에서 반환한 핸들을 매개변수로 사용합니다 `dlopen`. 해당 핸들의 참조 횟수가 0에 도달하면 라이브러리가 현재 프로세스의 주소 공간에서 언로드됩니다.
    
- `dlerror(3) OS X Developer Tools Manual Page``dlopen`: , `dlsym`또는 에 대한 마지막 호출에서 발생한 오류 조건을 설명하는 문자열을 반환합니다 `dlclose`.
    

DLC 기능에 대한 자세한 내용은 _OS X ABI Dynamic Loader Reference 를_ 참조하십시오 .