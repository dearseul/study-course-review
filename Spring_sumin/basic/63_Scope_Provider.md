## 스코프와 Provider
- 첫번째 해결방안은 앞서 배운 Provider를 사용하는 것.
```java
@Controller
@RequiredArgsConstructor // private이 붙거나 notnull인 필드를 이용하여 자동으로 의존성 주입
public class LogDemoController {

    private final LogDemoService logDemoService;
    private final ObjectProvider<MyLogger> myLoggerProvider;

    @RequestMapping("log-demo")
    @ResponseBody
    public String logDemo(HttpServletRequest request) {
        MyLogger myLogger = myLoggerProvider.getObject();
        String requestURL = request.getRequestURL().toString();
        myLogger.setRequestURL(requestURL);

        myLogger.log("controller test");
        logDemoService.logic("testID");
        return "OK";
    }
}
```
```java
@Service
@RequiredArgsConstructor
public class LogDemoService {

    private final ObjectProvider<MyLogger> myLoggerProvider;

    public void logic(String id) {
        MyLogger myLogger = myLoggerProvider.getObject();
        myLogger.log("service id = " + id);
    }
}
```
- main() 메서드로 스프링을 실행하고 log-demo 실행
- ``ObjectProvider`` 덕분에 ``getObject()``를 호출하는 시점까지 빈의 생성을 지연할 수 있음
- ``getObject()``를 호출하는 시점에는 http 요청이 진행 중이므로 request scope 빈의 생성이 정상 처리됨
- ``getObject()``를 controller, service에서 각각 한번씩 따로 호출해도 같은 HTTP 요청이면
같은 스프링이 반환됨