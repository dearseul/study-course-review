## 중복 등록과 충돌
- 자동 빈 등록 vs 자동 빈 등록
- 수동 빈 등록 vs 자동 빈 등록

### 자동 빈 등록 vs 자동 빈 등록
- 컴포넌트 스캔에 의해 자동으로 스프링 빈이 등록되는데, 그 이름이 같은 경우 스프링은 오류 발생
    - ``@ConflictingBeanDefinitionException`` 예외 발생

### 수동 빈 등록 vs 자동 빈 등록
``` java
@Component
public class MemoryMemberRepository implements MemberRepository {}
```

```java
@Configuration
@ComponentScan()
public class AutoAppConfig {
    
    @Bean("memoryMemberRepository")
    public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }
}
```
- 이 경우 수동 빈이 우선권을 가짐 (수동 빈이 자동 빈을 오버라이딩 함)

``` 
최근 스프링 부트에서는 수동 빈 등록과 자동 빈 등록이 충돌나면 오류가 발생하도록 기본 값을 바꿈
```
