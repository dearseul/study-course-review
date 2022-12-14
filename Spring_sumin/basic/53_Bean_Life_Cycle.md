## 빈 생명주기 콜백

### 빈 생명주기 콜백 시작
데이터베이스 커넥션 풀이나, 네트워크 소켓처럼 애플리케이션 시작 시점에 필요한 연결을 미리 해두고, 애플리케이션 종료 시점에 연결을 모두 종료하는 
작업을 진행하려면, 객체의 초기화와 종료 작업이 필요함

간단하게 외부 네트워크에 미리 연결하는 객체를 하나 생성한다고 가정해보자. 
이 ``NetworkClient``는 애플리케이션 시작 시점에 ``connect()``를 호출해서 연결을 맺어두어야 하고,
애플리케이션이 종료되면 ``disconnect()``를 호출해서 연결을 끊어야 함

```java
public class BeanLifeCycleTest {

    @Test
    public void lifeCycleTest() {
        AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(LifeCycleConfig.class);
        NetworkClient client = ac.getBean(NetworkClient.class);
        
        ac.close();
    }

    @Configuration
    static class LifeCycleConfig {
        @Bean
        public NetworkClient networkClient() {
            NetworkClient networkClient = new NetworkClient();
            networkClient.setUrl("http://hello.dev");
            return networkClient;
        }
    }
}
```
실행 결과는
```java
생성자 호출, url = null
connect : null
call : null message : 초기화 연결 메시지
```
생성자 부분을 보면 url 정보 없이 connect가 호출되는 것을 확인 할 수 있음.
너무 당연한 이야기이지만 객체를 생성하는 단계에는 url이 없고, 객체를 생성한 다음에 외부에서 수정자 주입을 통해서 ``setUrl()``이 호출되어야
url이 존재함

### 스프링 빈의 라이프 사이클
- 객체 생성 -> 의존관계 주입
- 스프링 빈은 객체를 생성하고, 의존관계 주입이 다 끝난 다음에야 필요한 데이터를 사용할 수 있는 준비가 완료됨. 따라서 초기화 작업은
의존관계 주입이 모두 완료되고 난 다음에 호출해야 함. 개발자가 의존관계 주입이 완료된 시점을 어떻게 알 수 있을까?
- 스프링은 의존관계 주입이 완료되면 스프링 빈에게 콜백 메서드를 통해서 초기화 시점을 알려주는 다양한 기능을 제공함.
또한 스프링은  스프링 컨테이너가 종료되기 직전에 소멸 콜백을 줌. 따라서 안전하게 종료 작업을 진행할 수 있음.
  
### 스프링 빈의 이벤트 라이프사이클
- 스프링 컨테이너 생성 -> 스프링 빈 생성 -> 의존관계 주입 -> 초기화 콜백 -> 사용 -> 소멸 전 콜백 -> 스프링 종료
- 초기화 콜백 : 빈이 생성되고, 의존관계가 주입된 뒤
- 소멸전 콜백 : 빈이 소멸되기 직전

``` 
참고 : 객체의 생성과 초기화를 분리하자.

생성자는 필수 정보(파라미터)를 받고, 메모리를 할당해서 객체를 생성하는 책임을 가짐. 반면에 초기화는 이렇게 생성된 값들을 활용해서
외부 커넥션을 연결하는 등 무거운 동작을 수행함.
따라서 생성자 안에서 무거운 초기화 작업을 함께 하는 것 보다는 객체를 생성하는 부분과 초기화 하는 부분을 명확하게 나누는 것이 
유지보수 관점에서 더 좋음
물론 초기화 작업이 내부 값들만 약간 변겨아는 정도로 단순한 경우에는 생성자에서 한번에 다 처리하는 게 나을 수 있음.
```

