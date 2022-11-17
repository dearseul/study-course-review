## 애노테이션 직접 만들기
-  ``@Qualifier("mainDiscountPolicy")`` 이렇게 문자를 적으면 컴파일시 타입 체크가 안 됨.
애노테이션을 만들어서 문제 해결 가능
```java
@Target({ElementType.FIELD, ElementType.METHOD, ElementType.PARAMETER, ElementType.TYPE, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Inherited
@Documented
@Qualifier("mainDiscountPolicy")
public @interface MainDiscountPolicy {
}
```
```java
@Component
@MainDiscountPolicy
public class RateDiscountPolicy implements DiscountPolicy {
}
```
```java
public OrderServiceImpl(MemberRepository memberRepository, @MainDiscountPolicy DiscountPolicy discountPolicy) {
    this.memberRepository = memberRepository;
    this.discountPolicy = discountPolicy;
}
```

- 애노테이션에는 상속이라는 개념이 없음. 이렇게 여러 애노테이션을 모아서 사용하는 것은 스프링이 제공하는 기능.
@Qualifier 뿐만 아니라 다른 애노테이션들도 함께 조합해서 사용할 수 있음. 
  다만 뚜렷한 목적 없이 무분별하게 재정의 하는 것은 유지보수에 혼란을 가중할 수 있음.