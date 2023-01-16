# 쿼리 메소드 기능 (12~18)
## 메소드 이름으로 쿼리 생성
### 장점
- 엔티티의 필드명이 변경되면 인터페이스에 정의한 메서드 이름도 함께 변경해야 함. 그렇지 않으면 애플리케이션 시작 시점에 오류 발생.
이렇게 애플리케이션 로딩 시점에 오류를 인지할 수 있는 것이 스프링 데이터 JPA의 큰 장점
## JPA NamedQuery
### 장점
- 애플리케이션 로딩 시점에 파싱을 함으로써 문법 오타를 잡아낼 수 있음.

## @Query, 리포지토리 메서드에 쿼리 정의하기
```java
@Query("select m from Member m where m.username = :username and m.age = :age")
List<Member> findUser(@Param("username") String username, @Param("age") int age);
```
### 장점
- 애플리케이션 로딩 시점에 파싱을 함으로써 문법 오타를 잡아낼 수 있음.

## @Query, 값, DTO 조회하기
- 실무에서 많이 사용하는 기능
```java
@Query("select new study.datajpa.dto.MemberDto(m.id, m.username, t.name) from Member m join m.team t")
List<MemberDto> findMemberDto();
```

## 파라미터 바인딩
### 이름 기반
```java
@Query("select m from Member m where m.username in :names")
List<Member> findByNames(@Param("names") Collection<String> names);
```
### 위치 기반
- 거의 사용하지 않음

## 반환 타입
```java
List<Member> findListByUsername(String username);
Member findMemberByUsername(String username);
Optional<Member> findOptionalByUsername(String username);
```
- 이 외에도 많은 return 타입이 있음.

## 순수 JPA 페이징과 정렬