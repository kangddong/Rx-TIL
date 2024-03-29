
# what is the main thread ?

메인 큐 또는 UI 스레드라고도 하는 메인 스레드는 iOS를 포함한 많은 프로그래밍 프레임워크에서 기본 실행 컨텍스트입니다. 기본 UI(사용자 인터페이스) 작업 및 상호 작용이 발생하는 스레드입니다.

iOS에서 기본 스레드는 사용자 입력 처리, 사용자 인터페이스 업데이트 및 UI 상호 작용과 관련된 코드 실행을 담당합니다. 여기에는 터치 이벤트 처리, 사용자 제스처에 응답, UI 요소 업데이트 및 애니메이션 수행과 같은 작업이 포함됩니다.

사용자 인터페이스 작업은 일반적으로 UI 응답성을 보장하고 동시 업데이트 간의 충돌을 피하기 위해 단일 스레드에서 수행되어야 하므로 기본 스레드가 중요합니다. 여러 스레드에서 UI 작업을 동시에 수행할 수 있는 경우 경합 상태, 데이터 불일치 및 응답하지 않는 UI가 발생할 수 있습니다.

따라서 iOS는 UI 관련 코드를 메인 스레드에서 실행해야 한다는 규칙을 적용합니다. UI 요소를 업데이트하거나 백그라운드 스레드에서 UI 관련 작업을 수행하려고 하면 예기치 않은 동작이나 충돌이 발생할 수 있습니다.

개발자는 Grand Central Dispatch(GCD) 또는 Operation Queues와 같은 iOS에서 제공하는 다양한 메커니즘을 사용하여 작업을 백그라운드 스레드에서 기본 스레드로 디스패치할 수 있습니다. 이를 통해 UI 관련 작업이 메인 스레드에서 동기식 또는 비동기식으로 실행되어 원활한 사용자 경험을 유지할 수 있습니다.

# Why should UI code be done on the main thread?

UI 코드는 몇 가지 중요한 이유로 기본 스레드에서 실행되어야 합니다.

1. 사용자 인터페이스 응답성: 메인 스레드는 터치 이벤트 및 제스처와 같은 사용자 상호 작용을 처리합니다. 기본 스레드에서 UI 코드를 수행하면 사용자 인터페이스가 응답성을 유지하고 사용자 작업에 즉각적인 피드백을 제공할 수 있습니다. UI 코드가 백그라운드 스레드에서 실행되면 지연이 발생하고 UI가 느리거나 응답하지 않는 것처럼 느껴질 수 있습니다.
2. 스레드 안전성: 메인 스레드에서 UI 코드를 수행하면 스레드 안전성이 보장됩니다. 대부분의 UI 프레임워크는 여러 스레드에서 동시에 액세스하도록 설계되지 않았습니다. 여러 스레드에서 UI 코드를 실행하면 서로 다른 스레드가 UI 요소를 동시에 업데이트하려고 시도할 수 있으므로 경합 상태 및 데이터 불일치가 발생할 수 있습니다. UI 작업을 기본 스레드로 제한하면 이러한 충돌을 방지하고 UI 업데이트의 무결성을 유지할 수 있습니다.
3. 사용자 입력과 동기화: UI 코드는 종종 사용자 작업을 기반으로 UI 요소를 업데이트하거나 터치 이벤트에 응답하는 등 사용자 입력과 상호 작용해야 합니다. 기본 스레드에서 UI 코드를 실행하면 사용자 입력과 동기화됩니다. 이렇게 하면 동기화되지 않은 UI 업데이트 또는 사용자 입력과 UI 업데이트 간의 경합 상태와 같은 문제를 방지할 수 있습니다.
4. UIKit 제한: iOS의 UI 프레임워크인 UIKit은 스레드로부터 안전하지 않으며 모든 UI 작업이 기본 스레드에서 수행된다고 가정합니다. 백그라운드 스레드에서 UI 요소를 업데이트하려고 하면 예기치 않은 동작이나 충돌이 발생할 수 있습니다. 기본 스레드에서 UI 코드를 실행해야 한다는 요구 사항을 준수하면 UIKit과의 호환성이 보장되고 잠재적인 문제가 방지됩니다.
전반적으로 메인 스레드에서 UI 코드를 실행하는 것은 반응적이고 일관된 사용자 인터페이스를 유지하고 스레드 관련 문제를 피하며 UIKit과 같은 UI 프레임워크와의 호환성을 보장하는 데 필수적입니다.

# Why is there a delay when running on a background thread?

백그라운드 스레드에서 코드를 실행할 때 다양한 요인으로 인해 코드 실행이 지연될 수 있습니다.

1. `컨텍스트 스위칭(Context switching)`: 메인 스레드에서 백그라운드 스레드로 또는 서로 다른 백그라운드 스레드 간에 전환할 때 운영 체제는 컨텍스트 전환을 수행해야 합니다. 컨텍스트 전환에는 실행 중인 스레드의 현재 상태를 저장하고 새 스레드의 상태를 로드하는 작업이 포함됩니다. 이 프로세스는 시간이 걸리고 오버헤드가 발생하여 백그라운드 스레드가 코드 실행을 시작하기 전에 지연이 발생합니다.
2. 대기열 우선 순위 지정: 백그라운드 스레드는 일반적으로 시스템의 다른 작업 및 스레드와 함께 동시 또는 병렬 방식으로 작동합니다. 운영 체제는 시스템 로드, 스레드 우선 순위 및 사용 가능한 리소스와 같은 요소를 기반으로 작업을 예약하고 우선 순위를 지정합니다. 다른 작업이나 스레드에 더 높은 우선 순위가 지정되면 이 우선 순위 지정으로 인해 백그라운드 스레드에서 코드를 시작하거나 실행하는 데 지연이 발생할 수 있습니다.
3. 종속성 및 동기화: 경우에 따라 백그라운드 스레드에서 코드를 실행하려면 다른 스레드와의 동기화 또는 특정 작업 완료가 필요할 수 있습니다. 예를 들어 백그라운드 스레드가 다른 백그라운드 작업의 완료 또는 특정 리소스의 가용성에 의존하는 경우 이러한 종속성이 충족될 때까지 지연이 있을 수 있습니다.
4. 스레드 풀링 및 리소스 할당: 백그라운드 스레드는 종종 시스템 리소스를 최적화하기 위해 동시 스레드 수를 제한하는 스레드 풀에 의해 관리됩니다. 풀에서 사용 가능한 모든 스레드가 사용 중인 경우 시스템은 백그라운드 스레드에서 코드를 실행하기 전에 스레드가 사용 가능해질 때까지 기다려야 할 수 있습니다. 이로 인해 특히 스레드 사용률이 높은 기간 동안 지연이 발생할 수 있습니다.
5. I/O 또는 네트워크 작업: 백그라운드 스레드는 일반적으로 네트워크 요청 또는 디스크 I/O 작업과 같이 시간이 많이 걸리는 작업을 수행하는 데 사용됩니다. 이러한 작업의 기간은 백그라운드 스레드에서 실행할 때 전체 지연에 기여할 수 있습니다. 예를 들어 백그라운드 스레드가 네트워크 응답을 기다리고 있는 경우 응답을 받을 때까지 유휴 상태가 되어 후속 코드 실행이 지연됩니다.

백그라운드 스레드에서 발생하는 특정 지연은 시스템의 부하, 작업의 복잡성 및 리소스 할당의 효율성에 따라 달라질 수 있다는 점에 유의해야 합니다. 백그라운드 스레드 사용을 효율적으로 관리하고 최적화하면 지연을 최소화하고 전체 시스템 성능을 향상하는 데 도움이 될 수 있습니다.