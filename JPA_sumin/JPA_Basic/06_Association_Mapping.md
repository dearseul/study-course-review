# 연관관계 매핑 기초

## 단방향 연관관계 (17)
- 1:N 관계에서 N 테이블에 FK가 있고, 해당 컬럼이 연관관계의 주인이 됨

## 양방향 연관 관계와 연관관계의 주인 1 - 기본
### 객체와 테이블이 관계를 맺는 차이
- 객체 연관관계 = 2개
    - 객체의 양방향 관계는 사실 양방향 관계가 아니라 서로 다른 단방향 관계 2개임
    - 회원 -> 팀 연관관계 1개 (단방향)
    - 팀 -> 회원 연관관계 1개 (단방향)
- 테이블 연관관계 = 1개
    - 테이블은 외래키  하나도 두 테이블의 연관관계를 관리 (양쪽으로 조인 가능)
    - 회원 <-> 팀 연관관계 1개 (양방향)

### 양방향 관계
- 외래키 관리
    - Member의 Team으로 관리? Team의 List<Member>로 관리?
- 양방향 관계      
    - 객체의 두 관계 중 하나를 연관관계의 주인으로 지정
    - 연관관계의 주인만이 외래 키를 관리 (등록, 수정)
    - 주인이 아닌 쪽은 읽기만 가능
    - 주인은 mappedBy 속성 사용 X
    - 주인이 아니면 mappedBy 속성으로 주인 지정
- 누구를 주인으로?
    - 외래키가 있는 곳을 주인으로 정해라
    - 여기서는 Member.team이 연관관계의 주인

## 양방향 연관 관계와 연관관계의 주인 2 - 주의점, 정리
### 가장 많이 하는 실수
- 연관관계의 주인에 값을 입력하지 않음
  - 양방향 매핑시 연관관계 주인에 값을 입력해야 함
  - 순수한 객체 관계를 고려하면 항상 양쪽 다 값을 입력해야 함
  ```java
    member.setTeam(team); 
    Team findTeam = em.find(Team.class, team.getId);
    List<Members> members = findTeam.getMembers();
  ```
  - 연관관계 편의 메서드를 생성하자. 둘 중 한 군데에만 생성
  - 양방향 매핑시 무한 루프를 조심하자
  
### 양방향 매핑 정리
- 단방향 매핑만으로 이미 연관관계 매핑은 완료
- 양방향 매핑은 반대 방향으로 조회 기능이 추가된 것 뿐
- JPQL에서 역방향으로 탐색할 일이 많음
- 단방향 매핑을 잘 하고 양방향은 필요할 때 추가해도 됨 (테이블에 영향을 주지 않음)

## 살전 예제 2 - 연관관계 매핑 시작 (20)
