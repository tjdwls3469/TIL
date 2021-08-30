### Spring 트랜잭션의 이점

* Spring은 글로벌 및 로컬 트랜잭션의 단점을 해결
* JTA(Java Transaction API), JDBC, Hibernate 및 JPA(Java Persistence API)와 같은 다양한 트랜잭션 API에서 일관된 프로그래밍 모델을 제공
* 선언적 트랜잭션 관리 지원
* JTA와 같은 복잡한 트랜잭션 API보다 프로그래밍 방식의 트랜잭션 관리를 위한 더 간단한 API 제공
* 뛰어난 접근 추상화

<br>

### 선언적 트랜잭션 관리

* 대부분의 Spring 사용자는 선언적 트랜잭션 관리를 선택한다
* 애클리케이션 코드에 가장 적은 영향을 미친다
* @Transaction 을 통해서 사용한다
* AOP 프록시를 통해 활성화되고 메타데이터(XML 또는 어노테이션)에 의해 구동된다
* 일반적으로 PlatformTransactionManager를 사용하고 reactive transaction인 경우에 ReactiveTransactionManager를 사용한다

<br>

### @Transactional 사용

* 가까운 @Transactional 선언의 영향을 받는다
* 클래스에도 @Transactional이 있고 메소드에도 @Transactional이 있으면 메소드의 @Transactional의 영향을 받는다
* public 접근지정자 일 때만 @Transactional이 적용된다
* private, protected, package 접근지정자의 메소드에 @Transactional을 붙여도 오류는 발생하지 않지만 실제로 트랜잭션은 동작하지 않는다 사용하고 싶다면 AspectJ compile-time 또는 load-time weaving을 사용해야 한다
* @Transational은 인터페이스가 아닌 구체 클래스에서 사용하는 것을 권장한다

<br>

### Transaction-bound 이벤트

* Spring 4.2부터 이벤트리스너를 통해서 트랜잭션의 단계마다 바인딩을 할 수 있다
* 예를 들면, 트랜잭션이 성공적으로 완료되었을 때 이벤트를 처리하는 것이다
* @TransactionalEventListener는 기본적으로 트랜잭션의 커밋 단계에 바인딩 된다
* BEFORE_COMMIT, AFTER_COMMIT(디폴트), AFTER_ROLLBACK, AFTER_COMPLETION
* 실행 중인 트랜잭션이 없으면 리스너가 호출되지 않는다
* reactive transaction에서는 사용할 수 없다
