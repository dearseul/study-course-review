## request 스코프 예제 만들기

### 웹 환경 추가
- 웹 스코프는 웹 환경에서만 동작하므로 라이브러리를 추가해야 함
```java
// web 라이브러리 추가
implementation 'org.springframework.boot:spring-boot-starter-web'
```
- ``spring-boot-starter-web`` 라이브러리를 추가하면 스프링 부트는 내장 톰캣 서버를 활용하여 웹 서버와
스프링을 함께 실행함
- 스프링 부트는 웹 라이브러리가 없으면 ``AnnotatationConfigApplicationContext``를 기반으로
애플리케이션을 구동. 
  웹 라이브러리가 추가되면 웹과 관련된 추가 설정과 환경들이 필요하므로 ``AnnotationConfigServletWebServerApplicationContext``를
  기반으로 애플리케이션을 구동.
  
### request 스코프 예제 개발
동시에 여러 HTTP 요청이 오면 정확히 어떤 요청이 남긴 로그인지 구분하기 어려움
이럴 때 사용하기 좋은 것이 바로 request 스코프

```java
@Component
@Scope(value="request")
public class MyLogger {

    private String uuid;
    private String requestURL;

    public void setRequestURL(String requestURL) {
        this.requestURL = requestURL;
    }

    public void log(String message) {
        System.out.println("[" + uuid + "]" + "[" + requestURL + "]" + message);
    }

    @PostConstruct
    public void init() {
        uuid = UUID.randomUUID().toString();
        System.out.println("[" + uuid + "] request scope bean create:" + this);
    }

    @PreDestroy
    public void close() {
        System.out.println("[" + uuid + "] request scope bean close:" + this);
    }
}
```
- request 스코프로 지정. 이 빈은 HTTP 요청 당 하나씩 생성되고, HTTP 요청이 끝나는 시점에 소멸됨
- 이 빈이 생성되는 시점에 자동으로 ``@PostConstruct`` 초기화 메서드를 사용해서 uuid를 생성해 저장함.
이 빈은 HTTP 요청 당 하나씩 생성되므로, uuid를 저장해두면 다른 HTTP 요청과 구분할 수 있음.
- 이 빈이 소멸되는 시점에 ``@PreDestroy``를 사용해서 종료 메서드를 남김
- ``requestURL``은 이 빈이 생성되는 시점에는 알 수 없으므로, 외부에서 setter로 입력받음

```java
@Controller
@RequiredArgsConstructor // private이 붙거나 notnull인 필드를 이용하여 자동으로 의존성 주입
public class LogDemoController {

    private final LogDemoService logDemoService;
    private final MyLogger myLogger;

    @RequestMapping("log-demo")
    @ResponseBody
    public String logDemo(HttpServletRequest request) {
        String requestURL = request.getRequestURL().toString();
        myLogger.setRequestURL(requestURL);
        // 이 부분은 컨트롤러 보다는 공통 처리가 가능한 스프링 인터셉터나 서블릿 필터 같은 곳에서 활용하는 게 좋음

        myLogger.log("controller test");
        logDemoService.logic("testID");
        return "OK";
    }
}
```
- 여기서 HttpServletRequest를 통해서 요청 URL을 받음
- 받은 requestURL 값을 myLogger에 저장함. myLogger는 HTTP 요청 당 각각 구분되므로 다른 HTTP 요청
때문에 값이 섞이지 않음
  
```java
@Service
@RequiredArgsConstructor
public class LogDemoService {

    private final MyLogger myLogger;

    public void logic(String id) {
        myLogger.log("service id = " + id);
    }
}

```
- 비즈니스 로직이 있는 서비스 계층
- 여기서 중요한 점. request scope를 사용하지 않고 파라미터로 이 모든 정보를 서비스 계층에 넘긴다면, 파라미터가
많아서 지저분해짐. 더 문제는 requestURL 같은 웹과 간련된 정보가 웹과 관련없는 서비스 계층까지 넘어가게 됨.
  웹과 관련된 부분은 컨트롤러까지만 사용해야 함. 서비스 계층은 웹 기술에 종속되지 않고, 가급적 순수하게
  유지하는 것이 유지보수 관점에서 좋음.
- request scope의 MyLogger 덕분에 이런 부분을 파라미터로 넘기지 않고, MyLogger의 멤버 변수에 저장해서
코드와 계층을 깔끔하게 유지 가능
  
### 실행 결과
- 오류 발생
- 스프링 애플리케이션을 실행하는 시점에 싱글톤 빈은 생성해서 주입이 가능하지만, request 스코프 빈은
아직 생성되지 않음. 이 빈은 실제 고객의 요청이 와야 생성할 수 있음.