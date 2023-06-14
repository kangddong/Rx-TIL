
iOS 에서 delegate, datesource를 가진 객체를 다룰 때

```swift
tableView.datasource = self
tableView.delegate = self
```

위와 같은 코드를 작성하게 된다.
작성 후 어떠한 행위도 하지않는다면 아래와 같은 오류 메세지를 볼 수 있게된다.


type '<Object name>' does not conform to protocol 'UITableViewDataSource'
Do you want to add protocol stubs?

`UITableViewDataSource` 는 아래와 같이 `protocol`로 되어있다.

```swift
@MainActor protocol UITableViewDataSource: NSObjectProtocol
```

`protocol`을 채택했기에 우린 선언 된 파라미터와 메소드 등을 구현해야한다.
그래서 protocol **stubs**? 에서 stubs 는 무엇을 의미하는지 궁금해졌다.


**type '<Object name>' does not conform to protocol 'UITableViewDataSource'**<br>
**Do you want to add protocol stubs?**
  
# stub

테스트 기법에서 많이 쓰이는 용어이다.
stub은 사전에 정의 된(interface로서) 반응으로 동작하게한다.
호출하는 함수가 아직 구현이 되지않았기에 이러한 인터페이스로서 제공하게 되는 함수입니다.
정리해보면, 가짜 함수(속이 빈 함수)라고 생각하시면 됩니다.

참고
[https://blog.naver.com/suresofttech/221204092938](https://blog.naver.com/suresofttech/221204092938)



  

