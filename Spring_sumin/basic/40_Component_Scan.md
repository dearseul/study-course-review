## 컴포넌트 스캔

### 컴포넌트 스캔과 의존관계 자동 주입 시작하기
- 지금까지 스프링 빈을 등록할 때는 자바 코드의 @Bean이나 XML의 <bean> 등을 통해서 설정 정보에 직접 등록할
스프링 빈을 나열했음
- 등록해야 할 스프링이 많아지면 설정 정보도 커지고 누락 문제도 생김
- 그래서 스프링은  설정 정보가 없어도 자동으로 스프링 빈을 등록하는 컴포넌트 스캔이라는 기능을 제공
- 또 의존관계도 자동으로 주입하는 ``@Autowired`` 기능도 제공

```java
@Configuration
@ComponentScan(
        excludeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = Configuration.class)
        // 실무에서는 잘 안 쓰는 내용이지만, 기존 예제 코드를 최대한 유지하기 위해 사용한 것
)
public class AutoAppConfig {
    
}
```
- 컴포넌트 스캔을 사용하려면 먼저 ``@ComponentScan``을 설정 정보에 붙임
- 기존의 AppConfig와는 다르게 @Bean으로 등록된 크래스가 하나도 없음
- 컴포넌트 스캔은 이름 그대로 ``@Component`` 애노테이션이 붙은 클래스를 스캔해서 스프링 빈으로 등록함
``` 
참고: @Configuration이 컴포넌트 스캔의 대상이 된 이유도 @Configuration 소스코드를 열어보면
@Component 애노테이션이 붙어있기 때문
```
- 이제 각 클래스가 컴포넌트 스캔의 대상이 되도록 ```@Component```를 붙여주자.

- 이전에 AppConfig에서는 ```@Bean```으로 직접 설정 정보를 작성했고 의존관계도 직접 명시함. 이제는 이런 설정
정보 자체가 없기 때문에, 의존관계 주입도 이 클래스 안에서 해결해야 함
- ```@Autowired```는 의존관계를 자동으로 주입해줌.  