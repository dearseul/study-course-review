# API 개발 고급 - 실무 필수 최적화 (22)

## OSIV ON
### 장점
- OSIV 전략은 데이터베이스 커넥션 시작 시점부터 API 응답이 끝날 때까지 영속성 컨텍스트와 데이터베이스 커넥션을 유지함.
- 지연 로딩은 영속성 컨텍스트가 살아있어야 가능하고, 영속성 컨텍스트는 기본적으로 데이터베이스 커넥션을 유지함. 이 자체가 큰 장점
### 단점 
- 커넥션 리소스 사용 시간이 길기 때문에, 실시간 트래픽이 중요한 애플리케이션에서 커넥션이 모자랄 수 있음. 장애로 이어질 수 있음.

## OSIV OFF
### 장점
- 트랜잭션을 종료할 때 영속성 컨텍스트를 닫고, 데이터베이스 커넥션도 반환함. 따라서 커넥션 리소스 낭비하지 않음
### 단점
- 모든 지연로딩을 트랜잭션 안에서 처리해야 함. 따라서 많은 지연 로딩 코드를 트랜잭션 안으로 넣어야 한다는 번거로움이 있음.
- view template에서 지연로딩이 동작하지 않음. 따라서 트랜잭션이 끝나기 전에 지연 로딩을 강제로 호출해 두어야 함

## 해결방안
### command와 query 분리
- OrderService
    - OrderService : 핵심 비즈니스 로직
    - OrderQueryService : 화면이나 API에 맞춘 서비스 (주로 읽기 전용 트랜잭션 사용)
- 고객 서비스의 실시간 API는 OSIV를 끄고, ADMIN처럼 커넥션을 많이 사용하지 않는 곳에서는 OSIV를 켜는 걸 추천    