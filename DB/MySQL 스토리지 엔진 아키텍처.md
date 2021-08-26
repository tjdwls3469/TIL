### MySQL (MySQL 서버)

* MySQL 엔진과 스토리지 엔진을 모두 합친 걸 의미한다.
* MySQL 엔진은 하나만 사용할 수 있지만 스토리지 엔진은 동시에 여러 개를 사용할 수 있다. 때문에 플러그형 스토리지 엔진 아키텍처라고 한다.
* 애플리케이션 프로그래머와 DBA를 분리하여 일관되고 쉬운 애플리케이션 모델 및 API를 제공한다.
* <https://dev.mysql.com/doc/refman/8.0/en/pluggable-storage-overview.html>
<img src = "https://user-images.githubusercontent.com/53414240/130951821-2dd904d2-d8b9-4451-bb2c-31d01c09eaed.png" width="45%" height="45%">

<br>

### 스토리지 엔진을 사용할 때의 주요 이점

* 특정 애플리케이션에 필요한 기능만 제공하므로 데이터베이스의 시스템 오버헤드가 줄어들고 최종 결과는 더 효율적이고 더 높은 데이터베이스 성능을 얻을 수 있다.
* 동시성
* 트랜잭션 지원
* 참조 무결성
* 물리적 저장소
* 인덱스 지원
* 메모리 캐시
* 성능 지원
* 기타 대상 기능
