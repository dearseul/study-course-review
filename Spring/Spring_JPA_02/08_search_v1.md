## 주문 조회 V1: 엔티티 직접 노출

> iter + tab : for문 자동으로 생성 

- orderItem , item 관계를 직접 초기화하면 Hibernate5Module 설정에 의해 엔티티를 JSON으로 생성한다. 
- 양방향 연관관계면 무한 루프에 걸리지 않게 한곳에 @JsonIgnore 를 추가해야 한다. 
- 엔티티를 직접 노출하므로 좋은 방법은 아니다.

## 주문 조회 V2: 엔티티를 DTO로 변환

- 지연 로딩으로 너무 많은 SQL 실행 SQL 실행 수 
  - order 1번 
  - member , address N번(order 조회 수 만큼) orderItem N번(order 조회 수 만큼)
  - item N번(orderItem 조회 수 만큼)

> 참고: 지연 로딩은 영속성 컨텍스트에 있으면 영속성 컨텍스트에 있는 엔티티를 사용하고 없으면 SQL을 실행한다. 
> 따라서 같은 영속성 컨텍스트에서 이미 로딩한 회원 엔티티를 추가로 조회하면 SQL을 실행하지 않는다.