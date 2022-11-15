## @Autowired 필드 명, @Quilifier, @Primary
- 조회 대상 빈이 2개 이상일 때 해결 방법
    - @Autowired 필드 명 매칭
    - @Qualifier -> @Qualifier 매칭 -> 빈 이름 매칭
    - @Primary 사용

### @Autowired 필드 명 매칭
- ``@Autowired``는 타입 매칭을 시도하고, 이 때 여러 빈이 있으면  필드 이름(파라미터 이름)으로 빈 이름을
추가 매칭함
- 기존 코드
```java
@Autowired
private DiscountPolicy discountPolicy
```  
- 필드 명을 빈 이름으로 변경
```java
@Autowired
private DiscountPolicy rateDiscountPolicy
```
- 필드명이 ``rateDiscountPolicy``이므로 정상 주입됨
- 필드 명 매칭은 먼저 타입 매칭을 시도하고 그 결과에 여러 빈이 있을 때 추가로 동작하는 기능임

#### Autowired 매칭 정리
1. 타입 매칭
2. 타입 매칭의 결과가 2개 이상일 때 필드 명, 파라미터 명으로 빈 이름 매칭

### @Qualifier 사용
- ``@Qualifier``는 추가 구분자를 붙여주는 방법.
주입 시 추가적인 방법을 제공하는 것이지 빈 이름을 변경하는 것은 아님
- 빈 등록시 ``@Qualifier``를 붙이고 등록한 이름을 넣어줌
```java
public OrderServiceImpl(MemberRepository memberRepository, @Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) {
        this.memberRepository = memberRepository;
        this.discountPolicy = discountPolicy;
    }
```
- 직접 빈 등록 시에도 ``@Qualifier``를 사용할 수 있음

#### @Qualifier 정리
1. @Qualifier끼리 매칭
2. 빈 이름 매칭
3. ``NoSuchBeanDefinitionException`` 발생

## @Primary 사용
- ``@Primary``는 우선 순위를 정하는 방법. ``@Autowired`` 시에 여러 빈이 매칭되면 ``@Primary``가
우선권을 가짐
```java
@Component
public class FixDiscountPolicy implements DiscountPolicy{
```  
```java
@Component
@Primary
public class RateDiscountPolicy implements DiscountPolicy{
```

### 우선 순위
- ``@Primary``는 기본값처럼 동작하는 것이고 ``@Qualifier``는 매우 상세하게 동작함.
이런 경우 어떤 것이 우선권을 가질까?
  스프링은 자동보다는 수동이, 넓은 범위의 선택권 보다는 좁은 범위의 선택권이 우선 순위가 높음.
  따라서 여기서도 ``@Qualifier``가 우선권이 높음
