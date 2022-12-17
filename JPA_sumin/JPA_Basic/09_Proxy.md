# 프록시와 연관관계 관리

## 프록시 (29)
### 프록시 기초
- em.find() vs em.getReference()
- em.find() : 데이터베이스를 통해서 실제 엔티티 객체 조회
- em.getReference() : 데이터베이스 조회를 미루는 가짜(프록시) 엔티티 객체 조회
### 프록시 특징
- 실제 클래스를 상속 받아서 만들어짐
- 실제 클래스와 겉 모양이 같음
- 사용하는 입장에서는 진짜 객체인지 프록시 객체인지 구분하지 않고 사용하면 됨 (이론상)
- 프록시 객체는 실제 객체의 참조(target)을 보관
- 프록시 객체를 호출하면 프록시 객체는 실제 객체의 메소드 호출
### 프록시 객체의 초기화
- 프록시 객체에 getName() -> 영속성 컨텍스트에 초기화 요청 -> DB 조회 -> 반환된 값으로 실제 Entity 생성 
-> target.getName()의 값을 얻어옴
- 두번 요청하면 이미 초기화 되어 있는 프록시이기 때문에 Select Sql을 날리지 않음  
### 프록시 특징(중요!!)
- 프록시 객체는 처음 사용할 때 한번만 초기화
- 프록시 객체를 초기화 할 때, 프록시 객체가 실제 엔티티로 바뀌는 것은 아님. 초기화되면 프록시 객체를 통해서 엔티티에 접근 가능
- 프록시 객체는 원본 엔티티를 상속받음, 따라서 타입 체크시 주의해야 함 (==비교 실패, 대신 instance of 사용)
- 영속성 컨텍스트에 찾는 엔티티가 이미 있으면, em.getReference()를 호출해도 실제 엔티티 반환
- 영속성 컨텍스트의 도움을 받을 수 없는 준영속 상태일 때, 프록시를 초기화 하면 문제 발생
  (하이버네이트는 org.hibernate.LazyInitializationException 예외를 던짐)
### 프록시 확인
- 프록시 인스턴스의 초기화 여부 확인
    - PersistenceUnitUtil.isLoaded(Object entity)
- 프록시 클래스 확인 방법
    - entity.getClass().getName() 출력
- 프록시 강제 초기화
    - org.hibernate.Hibernate.initialize(entity);
- 참고 : JPA 표준은 강제 초기화 없음 / getName()으로 강제 호출  

## 즉시 로딩과 지연 로딩
### 지연로딩 LAZY
```java
Member m = em.find(Member.class, member1.getId()); // 쿼리에 Team이 없음
System.out.println("m = " + m.getTeam().getClass()); // 프록시 

System.out.println("==================");
m.getTeam().getName(); // 초기화 -> 쿼리에 Team이 있음
System.out.println("==================");
```
### 즉시로딩 EAGER
- Member와 Team이 자주 함께 쓰인다면 사용
```java
Member m = em.find(Member.class, member1.getId()); // Member와 Team을 함께 조회
System.out.println("m = " + m.getTeam().getClass()); // 실제 class

System.out.println("==================");
m.getTeam().getName(); // 초기화가 필요 없으므로 출력 안 됨
System.out.println("==================");
```
- 즉시로딩이므로 Member를 조회 할 때 Team을 항상 같이 조회
### 프록시와 즉시로딩 주의
- 가급적 지연 로딩만 사용 (특히 실무에서)
- 즉시 로딩을 적용하면 예상하지 못한 SQL이 발생
- 즉시 로딩은 JPQL에서 N+1의 문제를 일으킴
- @ManyToOne, @OneToOne은 기본이 즉시 로딩 -> LAZY로 설정
- @OneToMany, @ManyTOMany는 기본이 지연 로딩
### 지연 로딩 활용 - 실무
- 모든 연관관계에서 지연 로딩을 사용

## 영속성 전이(CASCADE)와 고아 객체
### 영속성 전이
- 특정 엔티티를 영속 상태로 만들 때 연관된 엔티티도 함께 영속 상태로 만들고 싶을 때   
ex) 부모 엔티티를 저장할 때 자식 엔티티도 같이 저장
- 종류 : ALL, PERSIST, REMOVE  
### 영속성 전이 주의사항
- 영속성 전이는 연관관계를 매핑하는 것과 아무 관련이 없음
- 엔티티를 영속화 할 때 연관된 엔티티도 함께 영속화하는 편리함을 제공할 뿐
### 고아 객체
- 고아 객체 제거 : 부모 엔티티와 연관관계가 끊어진 자식 엔티티를 자동으로 삭제
- orphanRemoval = true
- 참조가 제거된 엔티티는 다른 곳에서 참조하지 않는 고아 객체로 보고 삭제하는 기능
- 참조하는 곳이 하나일 때 삭제해야 함
- 특정 엔티티가 개인 소유할 때 사용
- 고아 객체 기능을 활서오하 하면 부모를 제거할 때 자식도 같이 제거됨. CascadeType.REMOVE 처럼 동작
### 영속성 전이 + 고아객체
- CascadeType.ALL + orphanRemoval=true
- 스스로 생명주기를 관리하는 엔티티는 em.persist()로 영속화, em.remove()로 제거
- 두 옵션을 모두 활성화 하면 부모 엔티티를 통해서 자식의 생명 주기를 관리할 수 있음
- 도메인 주도 설계(DDD)의 Aggregate Root 개념을 구현할 때 유용

## 실전 예제 5 - 연관관계 관리 (32)

































