### Spring과 ORM

* Spring은 JPA(Java Persistence API)와의 통합을 지원하고 리소스 관리, DAO(Data Access Object) 구현 및 트랜잭션 전략을 위한 기본 Hibernate를 지원한다.
* Dependency Injection 을 통해 ORM에 대해 지원되는 모든 기능을 구성할 수 있다.
* Hibernate 또는 JPA API에 대해서 DAO를 코딩하는 것을 권장한다.

<br>

### Spring을 사용하여 ORM DAO를 생성하는 이점

* 더 쉬운 테스트
* 일반적인 데이터 액세스 예외
* 일반 자원 관리
* 통합 트랜잭션 관리

<br>

### Spring의 ORM 목적

* 명확한 애플리케이션 계층화와 애플리케이션 객체의 느슨한 결합
* 더 이상 데이터 엑세스 또는 트랜잭션 전략에 대한 비즈니스 서비스 종속성, 하드 코딩된 리소스 조회, 교체하기 어려운 싱들톤을 사용하지 말자

<br>

### 예외

* DAO에서 Hibernate 또는 JPA를 사용할 때 HibernateException 또는 PersistenceException를 throw 해야 한다.

<br>

### JPA

* org.springframework.orm.jpa 패키지에서 사용 가능한 Spring JPA는 추가 기능을 제공하기 위해 기본 구현을 인식하면 Hibernate와의 통합과 유사한 방식으로 Jva Persistance API에 대한 포괄적인 지원을 제공한다.
