## 스프링 빈 조회 - 동일한 타입이 둘 이상
- 타입으로 조회시 같은 타입의 스프링 빈이 둘 이상이면 오류가 발생. 이 때에는 빈 이름을 지정하자
- ``ac.getBeansOfType()`` 을 이용하면 해당 타입의 모든 빈을 조회할 수 있음
