### R2DBC

* Reactive Relational Database Connectivity
* reactive 패턴을 사용하여 SQL 데이터베이스에 대한 엑세스를 표준화하는 작업

<br>

### 패키지 계층

* core
    * org.springframework.r2dbc.core 패키지에는 DatabaseClient 클래스와 다양한 관련 클래스가 포함되어 있다
* connection
    * org.springframework.r2dbc.connection 패키지에는 쉽게 엑세스 할 수 있는 유틸리티 클래스 ConnectionFactory 와 수정되지 않은 R2DBC를 테스트하고 실행하는 데 사용하는 다양한 기능이 있다

<br>

### DatabaseClient

* R2DBC 코어 패키지의 중심 클래스이다
* SQL 쿼리 실행
* 업데이트 문 및 저장 프로시저 호출
* Result 인스턴스에 대해 반복 수행
* R2DBC 예외를 포착하고 보다 유익한 예외 계층으로 변환한다
* H2, MariaDB, Microsoft SQL Server, MySQL, Postgres에서 지원한다
* DatabaseClient 클래스의 인스턴스는 스레드로부터 안전하다
