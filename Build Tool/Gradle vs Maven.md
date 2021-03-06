### 유연성

* Google은 Android용 공식 빌드 도구로 Gradle를 사용한다.
* Gradle은 C/C++를 사용하는 네이티브 개발에 사용할 수 있으며 모든 생태계를 포괄하도록 확장할 수 있다.
* <https://gradle.org/maven-vs-gradle/>

<br>

### 성능

* Gradle은 Maven보다 최대 100배 빠르다.
* Gradle의 빌드 캐시가 극단적인 성능 향상을 만들어낸다.
* 빌드 캐시는 이전 빌드의 빌드 출력이 보존되고 다시 만들 필요가 없기 때문에 매우 유용하다.
* 이를 가능하게 하는 3가지 기능
* Incrementality
    * 입력 또는 출력이 변경되지 않은 경우 Gradle은 해당 작업을 건너뛸 수 있다.
* Build Cache
    * 로컬에서 Gradle 작업의 출력을 재사용하고 머신 간에 작업 출력을 공유한다.
* Gradle Daemon
    * 백그라운드 프로세스다.
    * 프로젝트에 대한 데이터를 메모리에 유지함으로써 값비싼 프로세스를 피하고 캐싱을 활용하여 훨씬 더 빠르게 빌드를 실행한다.
* <https://gradle.org/gradle-vs-maven-performance/>
