
이 속성을 `funtion`, `method`, `computed property,` `subscript`, `convenience initializer` 또는 `deinitializer` 선언에 적용하여 선언과 동일한 모듈에 정의된 inlinable 코드에서 해당 기호를 사용할 수 있도록 하십시오. 선언에는 `internal` 액세스 레벨 수정자가 있어야 합니다. `useableFromInline`으로 표시된 구조 또는 클래스는 속성에 공용 또는 `usableFromInline` 유형만 사용할 수 있습니다. `useableFromInline`으로 표시된 열거형은 사례의 원시 값 및 관련 값에 대해 public 또는 `usableFromInline` 유형만 사용할 수 있습니다.

`public` 액세스 수준 수정자와 마찬가지로, 이 속성은 모듈의 공개 인터페이스의 일부로 선언을 노출합니다. `public`과 달리, 컴파일러는 선언의 기호가 내보내지더라도 `usableFromInline`으로 표시된 선언이 모듈 외부의 코드에서 이름으로 참조되는 것을 허용하지 않습니다. 그러나, 모듈 외부의 코드는 여전히 런타임 동작을 사용하여 선언의 기호와 상호 작용할 수 있습니다.

`ininable` 속성으로 표시된 선언은 ininable 코드에서 암시적으로 사용할 수 있습니다. `Inlinable` 또는 `usableFromInline을` `internal` 선언에 적용할 수 있지만, 
두 속성을 모두 적용하는 것은 error입니다.