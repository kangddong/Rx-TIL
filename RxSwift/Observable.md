
**Reactive X**에서 `Observer`는 `Observable`을 **구독**(`subscribe`)한다.
`Observer`는 `Observable`이 **방출**(`emits`)하는 `item` 혹은 `sequence`에 반응한다.

?
이러한 패턴은 동시성 연산을 가능하게 한다. 그 이유는 Observable이 객체를 배출할 때까지 기다릴 필요 없이 어떤 객체가 배출되면 그 시점을 감시하는 관찰자를 옵저버 안에 두고 그 관찰자를 통해 배출 알림을 받으면 되기 때문이다.
?


# 배경
우리가 "옵저버"라고 말하는 것이 다양한 문서나 문맥에서는 "구독자"나 "관찰자" 또는 "리액터"로 불려지고 있지만, 통상적으로 이 모델은 [리액터 패턴](http://en.wikipedia.org/wiki/Reactor_pattern)을 말한다.


## onNext, onCompleted, 그리고 onError

### `onNext`

### `onCompleted`

### `onError`


## Unsubscribing(구독해지)


# “Hot” and “Cold” Observables


# Observable 연산자를 활용한 구성

Observable과 옵저버는 그저 ReactiveX의 시작점일 뿐이다. 우리가 알고 있는 **표준 옵저버 패턴**을 조금 확장한 것이며, 연속된 이벤트를 처리하는데 있어서는 싱글 콜백보다는 훨씬 더 효과적인 방법을 제공한다.

"리액티브 확장(reactive extensions)"(그래서 "ReactiveX"로 부르는)의 진짜 힘은 연산자로부터 나온다. 연산자들은 Observable이 배출하는 연속된 항목들을 변환시키고, 결합하고, 조작하는 기능들을 제공한다.

이 연산자들은 콜백이 제공하는 효율적인 장점들을 바탕으로 선언적인 방법을 통해 연속된 비동기 호출을 구성할 수 있는 방법을 제공하는데, 중요한 것은 일반적인 비동기 시스템이 가진 중첩된 콜백 핸들러의 단점들을 제거했다는 점이다.

여기에서 제공하는 문서들은 [다양한 연산자](https://reactivex.io/documentation/operators.html#alphabetical)에 대한 내용을 그룹으로 나눠 연결된 링크들을 통해 실제 사용에 필요한 예제를 제공한다:

[Observable 생성](https://reactivex.io/documentation/operators.html#creating)
`Create`, `Defer`, `Empty`/`Never`/`Throw`, `From`, `Interval`, `Just`, `Range`, `Repeat`, `Start`, 그리고 `Timer`

[Observable 항목 변환](https://reactivex.io/documentation/operators.html#transforming)
`Buffer`, `FlatMap`, `GroupBy`, `Map`, `Scan`, 그리고 `Window`

[Observable 필터](https://reactivex.io/documentation/operators.html#filtering)
`Debounce`, `Distinct`, `ElementAt`, `Filter`, `First`, `IgnoreElements`, `Last`, `Sample`, `Skip`, `SkipLast`, `Take`, 그리고 `TakeLast`

[Observable 결합](https://reactivex.io/documentation/operators.html#combining)
`And`/`Then`/`When`, `CombineLatest`, `Join`, `Merge`, `StartWith`, `Switch`, 그리고 `Zip`

[오류 처리 연산자](https://reactivex.io/documentation/operators.html#error)
`Catch` , `Retry`

[유틸리티 연산자](https://reactivex.io/documentation/operators.html#utility)
`Delay`, `Do`, `Materialize`/`Dematerialize`, `ObserveOn`, `Serialize`, `Subscribe`, `SubscribeOn`, `TimeInterval`, `Timeout`, `Timestamp`, 그리고 `Using`

[조건 및 불린(Boolean) 연산자](https://reactivex.io/documentation/operators.html#conditional)
`All`, `Amb`, `Contains`, `DefaultIfEmpty`, `SequenceEqual`, `SkipUntil`, `SkipWhile`, `TakeUntil`, 그리고 `TakeWhile`

[수학과 조합 연산자](https://reactivex.io/documentation/operators.html#mathematical)
`Average`, `Concat`, `Count`, `Max`, `Min`, `Reduce`, 그리고 `Sum`

[변환 Observable](https://reactivex.io/documentation/operators.html#conversion)
`To`

[연결 가능한 Observable 연산자](https://reactivex.io/documentation/operators.html#connectable)

`Connect`, `Publish`, `RefCount`, 그리고 `Replay`

[역압(backpressure) 연산자](https://reactivex.io/documentation/operators/backpressure.html)

특정 제어흐름 원칙들을 적용하는 다양한 연산자들
## Chaining Operators(연산자 체인)

대부분의 연산자들은 Observable 상에서 동작하고 Observable을 리턴한다. 이런 접근 방법은 연산자들을 하나의 Observable에 적용하고 또 다음 연산자에 다시 적용할 수 있는 연산자 체인을 제공한다. 연산자 체인에 걸려있는 각각의 연산자들은 이전 연산자가 리턴한 Observable을 변경한다.

특정 클래스의 다양한 메서드 연산을 통해서 같은 클래스에 있는 항목들을 변경하는 빌더 패턴 같은 것도 존재한다. 이 패턴 역시 비슷한 방법으로 메서드 체인을 제공한다.
하지만, 연산자의 호출 순서가 문제가 되지 않는 빌더 패턴과는 달리, Obervable 연산자들은 _호출 순서_에 영향을 받는다.

Observable 연산자 체인은 원본 Observable과는 떨어져서 동작할 수 없고 _순서대로_ 동작하기 때문에, 호출 체인 중 바로 이전에 호출된 연산자가 리턴한 Observable을 기반으로 실행된다.


항상 궁금했던 부분
RxSwift 는 빌더패턴을 차용한 것일까 ? 궁금했었는데
공식문서에 떡하니 소개가 되어있었다.
빌더패턴이 언급되어있고, 사용법이 비슷한 것을 보니 영향을 받았다 정도가 아닐까싶다

소개 글에 의하면 RxSwift에 대표적인 패턴 컨셉은 이렇게 3가지인 것 같다
* 리액터 패턴
* 옵저버 패턴
* 빌더 패턴

 


출처
[Reactive X observable Docs](https://reactivex.io/documentation/ko/observable.html)
[김배추](https://baechukim.tistory.com/14)

