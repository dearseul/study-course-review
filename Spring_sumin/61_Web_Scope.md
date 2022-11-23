## 웹 스코프
- 싱글톤은 스프링 컨테이너의 시작과 끝까지 함께하는 매우 긴 스코프이고,
프로토타입은 생성과 의존관계 주입, 그리고 초기화까지만 진해하는 특별한 스코프임
  
### 웹 스코프의 특징
- 웹 스코프는 웹 환경에서만 동작함
- 웹 스코프는 프로토타입과 다르게 스프링이 해당 스코프의 종료시점까지 관리함. 따라서 종료 메서드가 호출됨

### 웹 스코프 종류
- **request** : HTTP 요청 **하나**가 들어오고 나갈 때까지 유지되는 스코프, 각각의 HTTP 요청마다 별도의
빈 인스턴스가 생성되고 관리됨
- **session** : HTTP session과 동일한 생명주기를 가지는 스코프
- **application** : 서블릿 컨텍스트와 동일한 생명주기를 가지는 스코프
- **websocket** : 웹 소켓과 동일한 생명주기를 가지는 스코프