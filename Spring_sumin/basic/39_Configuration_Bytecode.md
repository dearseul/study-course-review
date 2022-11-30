## @Configuration과 바이트코드 조작의 마법
```java
AppConfig bean = ac.getBean(AppConfig.class);
System.out.println("bean= " + bean.getClass());
-> // bean= class hello.core.AppConfig$$EnhancerBySpringCGLIB$$ae0d1a15
```
- 순수한 클래스라면 ``class hello.core.AppConfig``로 출력되어야 함
- 그런데 예상과는 다르게 클래스 명에 xxxCGLIB가 붙으면서 상당히 복잡해짐.
이것은 내가 만든 클래스가 아니라 스프링이 CGLIB라는 바이트코드 조작 라이브러리를 사용해서 AppConfig 클래스를
  상속받은 임의의 다른 클래스를 만들고, 그 다른 클래스를 스프링 빈으로 등록한 것
- 그 임의의 다른 클래스가 싱글톤이 보장되도록 해줌
- @Bean이 붙은 메서드마다 이미 스프링 빈이 존재하면 존재하는 빈을 반환하고, 스프링 빈이 없으면 생성해서 스프링
빈으로 등록하고 반환하는 코드가 동적으로 만들어짐.
  - 덕분에 싱글톤이 보장됨.

### @Configuration을 적용하지 않고, @Bean만 적용하면 어떻게 될까?
- @Configuration을 붙이면 바이트코드를 조장하는 CGLIB 기술을 사용해서 싱글톤을 보장하지만, 만약 @Bean만 
적용하면 어떻게 될까?
    - 순수한 클래스 ``class hello.core.AppConfig``가 출력됨
    - 스프링 빈이 다 등록됨
    - 다만 출력 결과 MemberRepository가 세번 호출되고 각각 다른 인스턴스임
    
### 정리
- @Bean만 사용해도 스프링 빈으로 등록되지만 싱글톤을 보장하지 않음
    - ``memberRepository()`` 처럼 의존관계 주입이 필요해서 메서드를 직접 호출할 때 싱글톤을 보장하지 않음
- 크게 고민할 것 없이 스프링 설정 정보는 항상 ``@Configuration``을 사용하자    