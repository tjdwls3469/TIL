### Spring Web MVC

* Servlet API를 기반으로 구축된 Web Framework다.
* 정식 명칭은 Spring Web MVC이다.
* 일반적으로 Spring MVC로 알려져 있다.
* Spring Framework 5.0은 "Spring WebFlux"라는 모듈을 기반으로 하는 반응형 웹 프레임워크를 도입했다.

<br>

### DispatcherServlet

* 많은 Web Framework와 마찬가지로 Spring MVC는 DispatcherServlet을 활용한 front controller 패턴을 중심으로 설계되었다.

<br>

### Context 구조

* 하나의 Root WebApplicationContext 가 여러 DispatcherServlet 인스턴스에서 공유되는 구조를 가질 수도 있다.
* Root WebApplicationContext 에는 일반적으로 여러 Servlet 인스턴스에서 공유해야 하는 Data Repository 및 Business Service와 같은 인프라 빈이 포함된다.
<img src = "https://user-images.githubusercontent.com/53414240/131442447-9c91e22b-e076-4803-bedf-3daa04ca6692.png" width="40%" height="40%">
