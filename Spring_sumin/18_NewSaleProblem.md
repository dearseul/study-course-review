## 새로운 할인 정책 적용과 문제점

### 문제점
- 할인 정책을 변경하려면 클라이언트 코드를 변경해야 함.
- 클래스 의존관계를 분석해보면?
    - 인터페이스 뿐만 아니라 구현 클래스에도 의존하고 있음
    - 즉 DIP를 위반함 (인터페이스에도 의존하고 구체클래스에도 의존함)
    - 소스 변경 없이 확장 불가능 --> OCP 위반
    
### 해결방법
- 인터페이스에만 의존하도록 소스를 변경
  ```
    private final DiscountPolicy discountPolicy = new FixDiscountPolicy();
    -->
    private DiscountPolicy discountPolicy;
  ```
    - discountPolicy.discount() 실행 시 구현체가 없어서 null pointer error가 발생  
- 누군가가 클라이언트에 DiscountPolicy의 구현 객체를 대신 생성하고 주입해야 함
