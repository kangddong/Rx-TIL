
```swift
extension ObservableType where Element: ObservableConvertibleType {
    // 모든 observable 시퀀스에서 지정 된 enumerable 시퀀스 element들을 단일 observable 시퀀스로합친다.
    public func merge() -> Observable<Element.Element> {
            Merge(source: self.asObservable())
    }
}
```

merge 주의할 점은 return 해주는 타입이 같아야한다.

```swift
// 여러 `Element`들을 새로운 Observable instance로 만들어 준다
public static func of(
					  _ elements: Element ...,
					  scheduler: ImmediateSchedulerType = CurrentThreadScheduler.instance
					  ) -> Observable<Element> {
        ObservableSequence(
        elements: elements,
         scheduler: scheduler
         )
}
```


```swift
import RxSwift
 
let disposeBag = DisposeBag()
 
let subject = PublishSubject<String>()
let subject2 = PublishSubject<String>()
 
Observable.of(subject, subject2).merge()
    .subscribe(onNext: { print($0) })
    .disposed(by: disposeBag)
 
subject.onNext("R")
subject.onNext("x")
subject.onNext("S")
subject.onNext("w")
subject.onNext("")
 
subject2.onNext("i")
subject2.onNext("f")
subject2.onNext("t")
subject2.onNext("!")
subject2.onNext("!")

```