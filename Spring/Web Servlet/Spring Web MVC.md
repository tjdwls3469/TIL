### Spring Web MVC

* Servlet API를 기반으로 구축된 Web Framework다.
* 정식 명칭은 Spring Web MVC이다.
* 일반적으로 Spring MVC로 알려져 있다.
* Spring Framework 5.0은 "Spring WebFlux"라는 모듈을 기반으로 하는 반응형 웹 프레임워크를 도입했다.
* <https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#spring-web>

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

<br>

### Spring Web MVC 동작원리 다시 정리

1. 클라이언트로 요청이 온다.
2. LocaleResolver, ThemeResolver, MultipartResolver를 통해서 locale, theme, multipart를 체크한다.
3. HandlerMapping을 통해 적절한 Controller를 찾아 요청을 위임한다.
4. 실행에 대한 결과(model)를 받으면 ViewResolver를 통해 View를 받는다.
5. 최종적으로 결과를 응답한다.

<br>

### Interception

* 모든 HandlerMapping 구현은 유용한 핸들러 인터셉터를 지원한다.
* org.springframework.web.servlet 패키지의 HandlerInterceptor에서 구현해야 한다.
* preHandle(..)
    * 실제 핸들러가 실행되기 전
* postHandle(..)
    * 핸들러 실행 후
* afterCompletion(..)
    * 완전한 요청이 완료된 후
* Controller Advice를 활용하는 방법도 있다.

<br>

### 예외

* 요청 매핑 중에 예외가 발생하거나 @Controller에서 예외가 발생하면 DispatcherServlet가 예외 처리를 HandlerExceptionResolver에게 위임하여 예외를 해결한다.

|HandlerExceptionResolver|설명|
|------|-------|
|SimpleMappingExceptionResolver|예외 클래스 이름과 오류 보기 등 응용 프로그램에서 오류 페이지를 렌더링 하는 데 유용하다.|
|DefaultHandlerExceptionResolver|Spring MVC에서 발생한 예외를 해결하고 이를 HTTP 상태 코드에 매핑한다. ResponseEntityExceptionHandler 참조|
|ResponseStatusExceptionResolver|ResponseStatus 어노테이션으로 예외를 해결하고 HTTP 상태 코드에 매핑한다.|
|ExceptionHandlerExceptionResolver|@Controller 클래스 안에 있는 @ExceptionHandler 메소드를 호출하거나 @ControllerAdvice 클래스를 통해서 예외를 해결한다.|

<br>

### Redirecting

* redirect: 접두사를 사용하면 Redirecting을 수행할 수 있다.
* UrlBasedViewResolver가 redirect:를 인식한다.
* Redirecting을 하면 URL이 변경된다. 
* @ResponseStatus는 Redirecting보다 우선순위가 높다.

<br>

### Forwarding

* forward: 접두사를 사용하면 Forwarding을 수행할 수 있다.
* 리소스를 전달할 수 있다.

<br>

### MultipartResolver

* org.springframework.web.multipart 패키지에서 파일 업로드를 포함한 multipart 요청을 분석하기 위한 전략이다.
* Commons FileUpload을 기반으로 하는 구현과 Servlet 3.0 multipart request parsing을 기반으로 하는 구현이 있다.
* Commons FileUpload는 전통적으로 POST 요청에만 적용되지만 모든 multipart/ 콘텐츠 유형을 허용한다.
* CommonsMultipartResolver 세부사항 및 구성 옵션은 javadoc 참조
* Servlet 3.0은 모든 Servlet 컨테이너에서 지원되지 않을 수 있다.
* StandardServletMultipartResolver 세부사항 및 구성 옵션은 javadoc 참조

<br>

### Annotated Controllers

* @Controller, @RestController
* @RestController는 @Controller와 @ResponseBody가 합쳐진 것이다.

<br>

### Request Mapping

* 클래스 수준에서는 공유 매핑을 해야하기 때문에 @RequestMapping이 필요하다.
* HTTP 메소드별 @RequestMapping
* @GetMapping
* @PostMapping
* @PutMapping
* @DeleteMapping
* @PatchMapping

<br>

### URI 패턴

* @RequestMapping메소드는 URL 패턴을 사용하여 매핑할 수 있고 두 가지 방법이 있다.
* PathPattern, AntPathMatcher 
* 웹 어플리케이션에 권장되는 솔루션이다.
* Spring WebFlux에서는 유일한 선택이다.
* Spring 5.3 이전에는 AntPathMatcher가 Spring MVC의 유일한 선택이었고 기본값이었다.

<br>

### @RequestParam

* 요청 매개변수를 컨트롤러의 메소드 인수에 바인딩 할 수 있다.
* 기본적으로 @RequestParam을 사용하면 매개변수는 필수이지만 required를 false로 설정하거나 java.util.Optional 래퍼로 인수를 선언하여 메소드 매개변수를 선택사항으로 지정할 수 있다.
* 매개변수 타입이 String이 아닌 경우 타입 변환이 자동으로 적용된다.
* Map<String, String>, MultiValueMap<String, String>를 사용하면 지정된 각 매개변수 이름에 대한 값으로 맵이 채워진다.

<br>

### @RequestHeader

* 요청의 헤더를 바인딩할 수 있다.
* 매개변수 타입이 String이 아닌 경우 타입 변환이 자동으로 적용된다.
* Map<String, String>, MultiValueMap<String, String>를 사용하면 지정된 각 매개변수 이름에 대한 값으로 맵이 채워진다.

<br>

### @CookieValue

* HTTP 쿠키 값을 바인딩할 수 있다.
* 매개변수 타입이 String이 아닌 경우 타입 변환이 자동으로 적용된다.

<br>

### @ModelAttribute

* 메소드의 인수에 사용하여 모델의 속성에 액세스하거나 존재하지 않는 경우 인스턴스화(기본 생성자 호출)할 수 있다.
* model 속성은 필드 이름과 일치하는 매개변수의 값으로 오버레이 된다.
* 데이터 바인딩으로 오류가 발생하면 기본적으로 BindException이 발생한다.
* @Valid으로 바인딩 후 유효성 검증을 자동으로 적용할 수 있다.

<br>

### @SessionAttributes

* HTTP 서블릿 세션에 모델 속성을 저장하는 데 사용한다.

<br>

### @SessionAttribute

* 전역적으로 관리되는 기존 세션 속성에 접근하는 경우 사용한다.
* 세션이 존재하거나 존재하지 않을 수 있는 경우에도 사용한다.

<br>

### @RequestAttribute

* @SessionAttribute와 유사하게 @RequestAttribute를 사용하여 이전에 생성된 기존 요청 속성에 접근할 수 있다.

<br>

### Multipart

* MultipartResolver가 활성화된 상태에서 POST 요청에 multipart/form-data가 담겨있으면 Multipart를 사용해서 액세스할 수 있다.
* @PostMapping, @RequestParam("file") MultipartFile file 이런 식으로 사용한다.
* JSON이 포함된 파일은 @PostMapping, @RequestPart("meta-data") MetaData metadata, @RequestPart("file-data") MultipartFile file 이런 식으로 사용한다.
* @RequestParam에 이름을 지정하지 않고 Map<String, MultipartFile> 또는 MultiValueMap<String, MultipartFile>를 활용할 수 있다.
* Servlet 3.0을 사용하면 Spring의 MultipartFile 대신 javax.servlet.http.Part를 사용할 수도 있다.

<br>

### @RequestBody

* request body를 읽거나 직렬화를 복원할 때 사용한다.

<br>

### HttpEntity

* @RequestBody와 거의 동일하지만 요청 헤더와 본문을 노출하는 컨테이너 객체를 기반으로 한다.

<br>

### @ResponseBody

* @ResponseBody를 사용하면 HttpMessageConverter를 통해 응답 본문에 반환을 직렬화할 수 있다. 

<br>

### ResponseEntity

* @ResponseBody같지만 상태와 헤더가 있다.

<br>

### JSON Views

* Spring MVC는 Jackson’s Serialization Views를 제공한다.
* @JsonView를 활용한다.

<br>

### 예외

* @Controller 또는 @ControllerAdvice 클래스는 @ExceptionHandler 메소드를 통해서 예외를 처리한다.
* Spring 5.3에서는 임의의 원인 수준을 일치시킬 수 있지만 이전 버전에서는 포괄적인 원인만 고려되었다.
