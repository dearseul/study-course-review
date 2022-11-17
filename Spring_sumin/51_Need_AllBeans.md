## 조회한 빈이 모두 필요할 때, List, Map
- 해당 타입의 스프링 빈이 다 필요한 경우가 있음
- 예를 들어 할인 서비스를 제공하는데 클라이언트가 할인의 종류(fix, rate)를 선택할 수 있다고 가정.
스프링을 사용하면 소위 말하는 전략 패턴을 간단하게 구현할 수 있음

```java
    @Test
    void findAllBean() {
        AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(AutoAppConfig.class, DiscountService.class);

        DiscountService discountService = ac.getBean(DiscountService.class);
        Member member = new Member(1L, "memberA", Grade.VIP);
        int discountPrice = discountService.discount(member, 10000, "fixDiscountPolicy");

        Assertions.assertThat(discountService).isInstanceOf(DiscountService.class);
        Assertions.assertThat(discountPrice).isEqualTo(1000);

        int rateDiscountPrice = discountService.discount(member, 20000, "rateDiscountPolicy");
        Assertions.assertThat(rateDiscountPrice).isEqualTo(2000);
    }

    static class DiscountService {
        private final Map<String, DiscountPolicy> policyMap;
        private final List<DiscountPolicy> policies;

        @Autowired
        public DiscountService(Map<String, DiscountPolicy> policyMap, List<DiscountPolicy> policies) {
            this.policyMap = policyMap;
            this.policies = policies;
            System.out.println("policyMap = " + policyMap);
            System.out.println("policies = " + policies);
        }

        public int discount(Member member, int price, String discountCode) {
            DiscountPolicy discountPolicy = policyMap.get(discountCode);
            return discountPolicy.discount(member, price);
        }
    }
```  
### 로직 분석
- DiscountService는 Map으로 만든 DiscoutPolicy를 주입받음. 이 때 fixDiscountPolicy, rateDiscountPolicy가 주입됨/
- ``discount()`` 메서드는 discountCode로 "fixDiscountPolicy"가 넘어오면 map에서 ``fixDiscountPolicy`` 
스프링 빈을 찾아서 실행함. 물론 "rateDiscountPolicy"가 넘어오면 ``rateDiscountPolicy`` 스프링 빈을
  찾아서 실행함
 
### 주입 분석
- ``Map<String,DiscountPolicy>``: map의 키에 스프링 빈의 이름을 넣어주고, 그 값으로 ``DiscountPolicy`` 타입으로
조회한 모든 스프링 빈을 담음
- ``List<DiscountPolicy>``: ``DiscountPolicy``타입으로 조회한 모든 스프링 빈을 담음.
- 만약 해당하는 타입의 스프링 빈이 없으면 빈 컬렉션이나 Map을 주입함
