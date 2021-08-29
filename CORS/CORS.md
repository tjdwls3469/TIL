### CORS

* Cross-Origin Resource Sharing의 줄임말이다.
* 한 Origin에서 실행 중인 웹 어플리케이션이 다른 Origin의 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제다.
* <https://developer.mozilla.org/ko/docs/Web/HTTP/CORS>

<br>

### CORS가 필요한 이유

* 보안 상의 이유로, 브라우저는 스크립트에서 시작한 교차 출처 HTTP 요청을 제한한다.
* 다른 Origin의 자원에 접근하려면 신뢰할 때에만 허용한다.
<img src = "https://user-images.githubusercontent.com/53414240/130447851-a60e6296-0c01-4ef3-bcc5-2b4fa6d7657a.png" width="55%" height="55%">

<br>

### 접근 제어 방법

* 서버에서 Access-Control-Allow-Origin을 설정한다.
* "preflighted" request를 사용하여 먼저 OPTIONS 메소드를 통해 다른 Origin의 자원으로 HTTP 요청을 보내 실제 요청이 전송하기에 안전한지 확인한다.
