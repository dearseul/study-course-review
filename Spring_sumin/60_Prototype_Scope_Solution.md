## 프로토타입 스코프 - 싱글톤 빈과 함께 사용시 Provider로 문제 해결
- 싱글톤 빈과 프로토타입 빈을 함께 사용할 때, 어떻게 하면 사용할 때마다 항상 새로운 프로토타입 빈을
생성할 수 있을까?
  
### 스프링 컨테이너에 요청
- 가장 간단한 방법은 싱글톤 빈이 프로토타입 빈을 사용할 때마다 스프링 컨테이너에 새로 요청하는 것
```java
    @Scope("singleton")
    static class ClientBean {
        @Autowired
        private ApplicationContext ac;
        
        public int logic() {
            prototypeBean.addCount();
            int count = prototypeBean.getCount();
            return count;
        }
    }
```
- 의존관계를 외부에서 주입(DI) 받는 게 아니라 이렇게 직접 필요한 의존관계를 찾는 것을 Dependency Lookup
 의존관계 조회라 함
-  그런데 이렇게 스프링의 애플리케이션 컨텍스트 전체를 주입받게 되면, 스프링 컨테이너에 종속적인 코드가 되고,
단위 테스트를 하기 힘들어짐.
   
### ObjectFactory, ObjectProvider
- 지정한 빈을 컨테이너에서 대신 찾아주는 DL 서비스를 제공하는 것이 바로 ``ObjectProvider``임.
참고로 과거에는 ``ObjectFactory``가 있었는데, 여기에 편의 기능을 추가해서 ``ObjectProvider``가 만들어짐.
```java
    @Scope("singleton")
    static class ClientBean {
        @Autowired
        private ObjectProvider<PrototypeBean> prototypeBeanProvider;


        public int logic() {
            PrototypeBean object = prototypeBeanProvider.getObject();
            object.addCount();
            int count = object.getCount();
            return count;
        }
    }
```  
- ``getObject()``를 호출하면 내부에서는 스프잉 컨테이너를 통해 해당 빈을 찾아서 반환함.
- 딱 필요한 DL 정도의 기능만 제공함
- 특징
    - ObjectFactory : 기능이 단순, 별도의 라이브러리 필요 없음. 스프링에 의존
    - ObjectProvider : ObjectFactory 상속. 스트림 처리 등 편의 기능이 많고, 별도의 라이브러리 필요 없음
    스프링에 의존함

### JSR-330 Provider
- 마지막 방법은 ``javax.inject.Provider``라는 JSR-330 자바 표준을 사용하는 방법임.
이 방법을 사용하려면 gradle 에 라이브러리 추가해야함
```java
    @Scope("singleton")
    static class ClientBean {
        @Autowired
        private Provider<PrototypeBean> prototypeBeanProvider;

        public int logic() {
            PrototypeBean object = prototypeBeanProvider.get();
            object.addCount();
            int count = object.getCount();
            return count;
        }
    }
```  
- ``get()``을 통해서 항상 새로운 프로토타입 빈이 생성되는 것을 확인할 수 있음
- 자바 표준이고 기능이 단순하므로 단위테스트를 만들거나 mock 코드를 만들기 쉬움
- ``Provider``는 지금 딱 필요한 DL 정도만 제공함
- 특징
    - ``get()``메서드 하나로 기능이 매우 단순
    - 별도의 라이브러리가 필요함
    - 자바 표준이므로 스프링이 아닌 다른 컨테이너에서도 사용 가능
    
### 정리
- 그러면 프로토타입 빈을 언제 사용할까? 매번 사용할 때마다 의존관꼐 주입이 완료된 새로운 객체가 필요하면
사용하면 됨. 그런데 실무에서 웹 애플리케이션을 개발해보면, 싱글톤 빈으로 대부분의 문제를 해결할 수 있기
  때문에 프로토타입 빈을 직접 사용하는 일은 드묾
- ``ObjectProvider``, ``JSR303 Provider`` 등은 프로토타입 뿐만 아니라 DL이 필요한 경우 언제든지 사용 가능

```
참고

실무에서 자바 표준인 JSR-330 Provider를 사용할 것인지, 아니면 스프링이 제공하는 ObjectProvider를 
사용할 것인지 고민이 될 것. ObjectProvider는 DL을 위한 편의 기능을 많이 제공해주고 스프링 외에 별도의
의존관계 추가가 필요 없기 때문에 편리함. 
만약 코드를 스프링이 아닌 다른 컨테이너에서도 사용할 수 있어야 한다면 JSR-330 Provider를 사용해야 함

스프링을 사용하다 보면 이 기능 뿐만 아니라 다른 기능들도 자바 표준과 스프링이 제공하는 기능이 겹칠 때가 있음.
대부분 스프링이 더 다양하고 편리한 기능을 제공해주기 때문에, 특별히 다른 컨테이너를 사용할 일이 없다면,
스프링이 제공하는 기능을 사용하면 됨.
```






