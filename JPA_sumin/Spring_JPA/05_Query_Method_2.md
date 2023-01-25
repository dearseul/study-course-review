# 쿼리 메소드 기능 (19~22)

## 스프링 데이터 JPA 페이징과 정렬
### 특별한 반환 타입
- Page : count 쿼리를 포함하는 페이징
- Slice : count 쿼리 없이 다음 페이지만 확인 가능 (내부적으로 limit+1 조회)
- List : 추가 count 쿼리 없이 결과 반환

## 벌크성 수정 쿼리
- @Modifying 어노테이션 이용. 사용하지 않으면 예외 발생
- 벌크성 쿼리를 실행하고 나서 영속성 컨텍스트 초기화 필요
    - ```@Modifying(clearAutomatically = true)```
    - 이 옵션 없이 조회시 영속성 컨텍스트에 과거 값이 남아서 문제가 될 수 있음. (영속성 컨텍스트의 값과 DB의 값이 다른 경우)   
- 권장 방안
    - 영속성 컨텍스트에 엔티티가 없는 상태에서 벌크 연산을 먼저 실행
    - 부득이하게 영속성 컨텍스트에 엔티티가 있으면 벌크 연산 직후 영속성 컨텍스트를 초기화 함 

## @EntityGraph
```java
  @Override
  @EntityGraph(attributePaths = {"team"})
  List<Member> findAll();
  
  @EntityGraph(attributePaths = {"team"})
  @Query("select m from Member m")
  List<Member> findMemberEntityGraph();
  
  @EntityGraph(attributePaths = {"team"})
  List<Member> findEntityGraphByUsername(@Param("username") String username);
```
- 페치조인 기능 구현해줌

## Jpa Hint & Lock
### JPA Hint
- JPA 쿼리 힌트 (SQL 힌트가 아니라 JPA 구현체에게 제공하는 힌트)
```java
  @QueryHints(value = @QueryHint(name = "org.hibernate.readOnly", value = "true"))
  Member findReadOnlyByUsername(String username);
```
### Lock
```java
  @Lock(LockModeType.PESSIMISTIC_WRITE)
  List<Member> findLockByUsername(String username);
```