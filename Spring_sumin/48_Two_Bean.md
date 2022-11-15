## 조회 빈이 2개이상 - 문제
- ``@Autowired``는 타입으로 조회함
```java
@Autowired
private DiscountPolicy discountPolicy
```
- 타입으로 조회하기 때문에 마치 다음 코드와 유사하게 동작함
    - ``ac.getBean(DiscountPolicy.class)``
    
- 타입으로 조회하면 선택된 빈이 2개 이상일 때 문제가 발생함
- ```DiscountPolicy```의 하위 타입인 ```FixDiscountPolicy```와 ```RateDiscountPolicy``` 둘 다
스프링 빈으로 선언해보자
```java
@Component
public class FixDiscountPolicy implements DiscountPolicy {}
```  
```java
@Component
public class RateDiscountPolicy implements DiscountPolicy {}
``` 
- 그리고 의존관계 주입을 실행하면
```java
@Autowired
private DiscountPolicy discountPolicy
```
- ```NoUniqueBeanDefinitionException```이 발생함
- 이 때 하위 타입으로 지정할 수 있지만, 하위 타입으로 지정하는 것은 DIP를 위배하고 유연성이 떨어짐.
그리고 이름만 다르고 완전히 똑같은 스프링 빈이 2개 있을 때 해결이 안 됨
  스프링 빈을 수동으로 등록하여 문제를 해결해도 되지만 의존 관계 주입에서 해결할 수 있음