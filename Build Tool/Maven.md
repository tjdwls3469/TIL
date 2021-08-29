### POM

* Project Object Model
* Maven에서 프로젝트를 빌드 하는 데 사용하는 프로젝트 및 세부 정보에 대한 정보가 포함된 XML 파일이다.
* <https://maven.apache.org/guides/introduction/introduction-to-the-pom.html>

<br>

### Super POM

* 모든 POM은 명시적으로 설정하지 않는 한 Super POM을 상속받는다.

<br>

### SNAPSHOT

* SNAPSHOT은 안정 또는 불변 보장을 제공하지 않는 '개발'버전을 의미한다.
* release 버전의 코드는 변경되지 않는다.
* <https://maven.apache.org/guides/getting-started/index.html>

<br>

### Build Lifecycle

|단계|설명|
|------|-------|
|validate|프로젝트가 정확하고 필요한 모든 정보를 사용할 수 있는지 확인|
|compile|프로젝트의 소스 코드를 컴파일|
|test|적절한 단위 테스트 프레임워크를 사용하여 컴파일된 소스 코드를 테스트한다. 이 테스트에서는 코드를 패키징 하거나 배포할 필요가 없다.|
|package|컴파일된 코드를 가져와서 JAR과 같은 배포 가능한 형식으로 패키징 한다.|
|verify|품질 기준이 충족되는지 확인하기 위해 통합 테스트 결과에 대한 모든 확인 실행|
|install|다른 프로젝트에서 로컬로 사용하기 위해 패키지를 로컬 저장소에 설치한다.|
|deploy|빌드 환경에서 완료되고 다른 개발자 및 프로젝트와 공유하기 위해 원격 저장소에 최종 패키지를 복사한다.|

1. Maven이 먼저 프로젝트의 유효성을 검사한다.
2. 컴파일한다.
3. 테스트한다.
4. JAR로 패키징 한다.
5. 통합 테스트한다.
6. 결과물을 local repository에 설치한다.
7. 설치된 패키지를 remote repository에 배포한다.
* https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html

<br>

### clean

* 항상 배포를 할 때에는 이전에 했던 빌드를 재사용할 수 있기에 clean 한 다음 실행하자.
* mvn clean deploy
