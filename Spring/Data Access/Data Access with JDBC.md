### JDBC 데이터베이스 엑세스에 대한 접근 방식 선택

* 모든 접근 방식에는 JDBC 2.0 드라이버가 필요하고 일부 고급 기능에는 JDBC 3.0 드라이버가 필요하다.
* JdbcTemplate
    * 가장 널리 사용되는 Spring JDBC 접근 방식이다.
    * JdbcTemplate의 인스턴스는 스레드로부터 안전하다.
* NamedParameterJdbcTemplate
* SimpleJdbcInsert, SimpleJdbcCall
* MappingSqlQuery, SqlUpdate, StoredProcedure

<br>

### 패키지 계층

* core
    * org.springframework.jdbc.core 패키지에는 JdbcTemplate클래스와 다양한 콜백 인터페이스 및 다양한 관련 클래스가 포함되어 있다.
* datasource
    * rg.springframework.jdbc.datasource 패키지에는 쉽게 액세스할 수 있는 유틸리트 클래스 DataSource와 Java EE 컨테이너 외부에서 수정되지 않은 JDBC 코드를 테스트하고 실행하는데 사용할 수 있는 다양하고 간단한 기능들이 포함되어 있다.
* object
    * org.springframework.jdbc.object 패키지에는 RDBMS 쿼리, 업데이트 및 저장 프로시저를 스레드로부터 안전하게 재사용 가능한 객체로 나타내는 클래스가 포함되어 있다.
* support
    * org.springframework.jdbc.support 패키지는 SQLException 번역 기능과 일부 유틸리티 클래스를 제공한다.

<br>

### IN 절에 대한 값 목록 전달

* 많은 값을 전달할때 주의해야한다.
* JDBC 표준은 in 에 대해 100개 이상의 값은 보장하지 않는다.
* 다양한 데이터베이스가 이 수를 초과하지만 일반적으로 허용되는 값 수는 엄격한 제한이 있다.
* 예를 들어, Oracle의 제한은 1000이다.

<br>

### 임베디드 데이터베이스

* org.springframework.jdbc.datasource.embedded 패키지는 임베디드 자바 데이터베이스 엔진에 대한 지원을 제공한다.
* HSQL, H2, Derby
* 빠른 구성, 빠른 시작, 테스트 등의 이유(가벼운 특성)로 개발 단계에서 유용할 수 있다.
