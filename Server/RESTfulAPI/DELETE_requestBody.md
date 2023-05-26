
결론부터 말하면, Spring 버전문제였다.

Spring에 내장된 RestTemplete 객체를 사용하는데,
Spring 4.2.x 버전부터는 DELETE 메서드에 대해서 body를 세팅해준다.

3.2.x  버전에서는 여서 body가 세팅이 되지않는다

### 이유

Http 1.1 가이드 문서격인 [RFC-7231](https://datatracker.ietf.org/doc/html/rfc7231)
[한글 번역본](https://hochan049.gitbook.io/cs-interview/web/rfc-7321-http-1.1)

>A payload within a DELETE request message has no defined semantics; sending a payload body on a DELETE request might cause some existing implementations to reject the request.

최신 문서 [RFC-9110](https://www.rfc-editor.org/rfc/rfc9110)

> Although request message framing is independent of the method used, content received in a DELETE request has no generally defined semantics, cannot alter the meaning or target of the request, and might lead some implementations to reject the request and close the connection because of its potential as a request smuggling attack (Section 11.2 of [HTTP/1.1]). A client SHOULD NOT generate content in a DELETE request unless it is made directly to an origin server that has previously indicated, in or out of band, that such a request has a purpose and will be adequately supported. An origin server SHOULD NOT rely on private agreements to receive content, since participants in HTTP communication are often unaware of intermediaries along the request chain.

### 해결 방법

>request를 생성하고 속성을 정의하는 클래스는 ClientHttpRequestFactory 인터페이스의 구현체 SimpleClientHttpRequestFactory다.
>이 클래스에서 request를 생성할 때 사용하는 메서드 createRequest 안에 있는 prepareConnection 메서드를 보면 아래와 같은 코드가 있다.


DELETE 안에 있는 페이로드에 대해서는 정의가 되지 않았다고 한다.


**RFC(Request For Comment : IETF(Internet Engineering Task Force)**에서,
인터넷에서 기술을 구현하는 데에 필요한 절차 등을 제공하는 **공문서 간행물**이다.

https://dogpaw.tistory.com/4 - Spring 버전문제 및 해결
https://datatracker.ietf.org/doc/html/rfc7231 - RFC-7231
https://velog.io/@lks93/delete-메서드-body-사용하기 - RFC-9110 언급