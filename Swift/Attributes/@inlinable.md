
이 속성을 `funtion`, `method`, `computed property,` `subscript`, `convenience initializer` 또는 `deinitializer` 선언에 적용하여 해당 선언의 구현을 모듈의 공용 인터페이스의 일부로 노출하십시오. 
컴파일러는 inlinable 기호에 대한 호출을 call site에서 기호 구현 복사본으로 대체할 수 있습니다.

Inlinable 코드는 모든 모듈에서 선언된 `public` 기호와 상호 작용할 수 있으며, [usableFromInline](/Swift/Attributes/@usableFromInline.md) 속성으로 표시된 동일한 모듈에서 선언된 `internal` 기호와 상호 작용할 수 있습니다. Inlinable 코드는 `private` 또는 `fileprivate` 기호와 상호 작용할 수 없습니다.

이 속성은 함수 내부에 중첩된 선언이나 `fileprivate` 또는 `private` 선언에 적용할 수 없습니다. Inlinable 함수 내부에 정의된 함수와 클로저는 이 속성으로 표시할 수 없지만 암시적으로 inlinable입니다.

함수 호출의 오버헤드를 줄여 코드 성능을 향상시키는 최적화 목적