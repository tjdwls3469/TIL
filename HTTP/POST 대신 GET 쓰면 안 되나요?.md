### POST 대신 GET 쓰면 안 되나요?

* 일반적으로 GET은 모든 요청을 캐싱 하기 때문에 안된다.
* GET은 safy메소드여서 아무리 호출해도 리소스를 변조시킬 가능성이 없다고 가정하기 때문에  
  GET으로 호출하여 리소스를 바꾼다면 스펙을 어기는 것이다.
  



### GET 이 safy 메소드야?

* GET은 safy메소드다.
* 공식문서를 보면 읽기 전용인 요청 메소드는 "안전한" 것으로 간주한다.  
  즉, 클라이언트는 대상 리소스에 안전한 방법을 적용한 결과로 서버의 상태 변경을 요청하지 않으며 예상하지도 않는다.  
  공식문서에서 정의한 요청 메소드 중 GET, HEAD, OPTIONS, TRACE 메소드는 안전한 것으로 정의되어 있다.
* <https://httpwg.org/specs/rfc7231.html>
>Request methods are considered "safe" if their defined semantics are essentially read-only; i.e., the client does not request, and does not expect, any state change on the origin >server as a result of applying a safe method to a target resource.

>Of the request methods defined by this specification, the GET, HEAD, OPTIONS, and TRACE methods are defined to be safe

