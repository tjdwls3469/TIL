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
* Root WebApplicationContext에는 일반적으로 여러 Servlet 인스턴스에서 공유해야 하는 Data Repository 및 Business Service와 같은 인프라 빈이 포함된다.
<img src = "https://user-images.githubusercontent.com/53414240/131442447-9c91e22b-e076-4803-bedf-3daa04ca6692.png" width="40%" height="40%">

<br>

### Special Bean 종류

* Spring 관리 인스턴스를 의미한다.
* 일반적으로 기본적인 속성을 갖추어 제공되지만 속성을 확장하거나 교체할 수 있다.

|Bean type|설명|
|------|-------|
|HandlerMapping|사전 및 사후 처리를 위한 인터셉터 목록과 요청을 핸들러에 매핑한다. 매핑은 기본 기준을 기반으로 하며 세부 사항은 HandlerMapping 구현에 따라 다르다. HandlerMapping을 구현하는 주요 두가지 방법은 RequestMappingHandlerMapping, SimpleUrlHandlerMapping이다.|
|HandlerAdapter|핸들러가 실제로 호출되는 방식에 관계없이 매핑된 핸들러를 호출하는데 도움이 된다.|
|HandlerExceptionResolver|예외를 해결하기 위한 전략|
|ViewResolver|핸들러에서 반환된 논리적 기반 뷰 이름(String)을 응답에 렌더링할 실제 이름(View)으로 확인한다.|
|LocaleResolver, LocaleContextResolver|국제화된 보기를 제공할 수 있도록 클라이언트가 사용하고 있는 시간대를 확인한다.|
|ThemeResolver|개인환된 레이아웃을 제공하기 위해 웹 애플리케이션에서 사용할 수 있는 테마를 해결해준다.|
|MultipartResolver|예를 들면 파일 업로드의 구문을 분석하기 위한 추상화를 도와준다.|
|FlashMapManager|redirect를 통해 속성을 전달하는 데 사용할 수 있는 "input" 및 "output"을 저장하고 검색한다.|

<br>

### Spring Web MVC 동작원리

1. WebApplicationContext는 검색 과정에서 컨트롤러와 다른 요소가 사용할 수 있는 속성으로 요청에 결합된다. 기본적으로 DispatcherServlet.WEB_APPLICATION_CONTEXT_ATTRIBUTE 키에 바인딩 된다.
2. LocaleResolver는 locale을 확인하도록 요청에 바인딩 된다. locale 해석이 필요하지 않으면 LocaleResolver는 무시해도 된다.
3. ThemeResolver는 View와 같은 요소가 사용할 테마를 결정하도록 하는 요청에 바인딩 된다. 테마를 사용하지 않는다면 무시해도 된다.
4. MultipartResolver를 지정하면 요청에서 Multipart가 검사된다. Multipart가 발견되면 추가 처리를 위해 MultipartHttpServletRequest로 래핑된다.
5. 적절한 Controller를 검색해서 실행시킨다.
6. 모델이 반환되면 뷰가 렌더링 된다. 만약 모델이 반환되지 않으면 요청이 이미 수행되었을 수 있으므로 렌더링되지 않는다.

* HTTP 캐싱 지원을 위해 WebRequest의 checkNotModified 메소드를 사용할 수 있다.
