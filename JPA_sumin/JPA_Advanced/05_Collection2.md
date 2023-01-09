# API 개발 고급 - 컬렉션 조회 최적화 (18~21)

## 주문 조회 V4 : JPA에서 DTO 직접 조회
### 
- Query: 루트 1번, 컬렉션 n번
- ToOne 관계들을 먼저 조회하고, ToMany 관계는 각각 별도로 처리함
    - 이런 방식을 선택한 이유는
    - ToOne 관계는 조인해도 데이터 row가 증가하지 않음
    - ToMany 관계는 조인하면 row 수가 증가함
- row 수가 증가하지 않는 ToOne 관계는 조인으로 최적화 하기 쉬우므로 한번에 조회하고,
ToMany 관계는 최적화하기 어려우므로 findOrderItems() 같은 별도의 메서드로 조회함

## 주문 조회 V5 : JPA에서 DTO 직접 조회 - 컬렉션 조회 최적화
###
- Query: 루트 1번, 컬렉션 1번
- ToOne 관계들을 먼저 조회하고, 여기서 얻은 식별자 orderId로 ToMany 관계인 OrderItem을 한꺼번에 조회
- Map을 사용해서 매칭 성능 향상(O(1))

## 주문 조회 V6 : JPA에서 DTO 직접 조회, 플랫 데이터 최적화

## API 개발 고급 정리 
### 권장 순서
- 엔티티 조회 방식으로 우선 접근
- 엔티티 조회 방식으로 해결 안 되면 DTO 조회 방식 이용
- DTO 조회 방식으로 해결 안 되면 NativeSQL or JdbcTemplate