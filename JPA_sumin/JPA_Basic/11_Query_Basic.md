# 객체지향 쿼리 언어1 - 기본 문법

## 소개 (39)
### JPQL
- JPA를 사용하면 엔티티 객체를 중심으로 개발
- 문제는 검색 쿼리
- 검색을 할 때도 테이블이 아닌 엔티티 객체를 대상으로 검색 -> 객체 지향 SQL
- 모든 DB 데이터를 객체로 변환해서 검색하는 것은 불가능
- 애플리케이션이 필요한 데이터만 DB에서 불러오려면 결국 검색 조건이 포함된 SQL 필요
### Criteria
- 복잡하고 실용성이 없음. QueryDSL 사용 권장.
### QueryDSL
- 문자가 아닌 자바코드로 JPQL을 작성할 수 있음.
- 컴파일 시점에 문법 오류를 찾을 수 있고 동적 쿼리 작성 편리함
- 단순하고 쉬움.
- 실무 사용 권장
### 네이티브 SQL
- JPA를 제공하는 SQL을 사용하는 기능
- JPQL로 해결할 수 없는 특정 데이터베이스에 의존적인 기능 ex) 오라클 connect by
### JDBC 직접 사용, SpringJdbcTemplate 등
- JPA를 사용하며넛 JDBC 커넥션을 직접 사용하거나, 스프링 JdbcTemplate, 마이바티스 등을 함께 사용 가능
- 단 영속성 컨텍스트를 적절한 시점에 강제로 플러시 필요

## 기본 문법과 쿼리 API
### JPQL
- SQL을 추상화해서 특정 데이터베이스 SQL에 의존하지 않음
- JPQL은 결국 SQL로 변환
### JPQL 문법
- 엔티티와 속성은 대소문자 구분 O (Member, m.age)
- JPQL 키워드는 대소문자 구분 X (SELECT, from)
- 엔티티 이름 사용, 테이블 이름이 아님 
- 별칭은 필수 (Member m)
- 집합과 정렬
    - count, sum, avg, ...
    - group by, having, order by
- TypeQuery, Query
    - TypeQuery : 반환 타입이 명확할 때 사용
    - Query : 반환 타입이 명확하지 않을 때 사용
    ```java
    TypedQuery<Member> query1 = em.createQuery("select m FROM Member m", Member.class);
    TypedQuery<String> query2 = em.createQuery("select m.username FROM Member m", String.class);
    Query query3 = em.createQuery("select m.username, m.age FROM Member m");
    ```
- 결과 조회 API
    - Query.getResultList() : 결과가 하나 이상일 때, 리스트 반환
    - Query.getSingleResult() : 결과가 정확히 하나, 단일 객체 반환
        - 결과가 많거나 없으면 에러 발생
- 파라미터 바인딩
    - 이름 기준으로만 쓰기

## 프로젝션(SELECT)
- SELECT 절에 조회할 대상을 지정
- 프로젝션 대상 : 엔티티, 임베디드 타입, 스칼라 타입(기본 타입)
- distinct로 중복 제거 
### 여러 값 조회
```java
SELECT m.age, m.username FROM Member m
```
- Query 타입으로 조회
- Object[] 타입으로 조회
- new 명령어로 조회
  ```java
    em.createQuery("select new jpql.MemberDTO(m.username, m.age) FROM Member m", MemberDTO.class)
  ```
    - 단순 값을 DTO로 바로 조회
    - 패키지명을 포함한 전체 클래스 명 입력
    - 순서와 타입이 일치하는 생성자 필요 

## 페이징
### 페이징 API
- JPA는 페이징을 다음 두 API로 추상화
  - setFirstResult(int start) : 조회 시작위치
  - setMaxResults(int maxResult) : 조회할 데이터 수

## 조인
### 조인 종류
- 내부 조인
- 외부 조인
- 세타 조인
### 조인 - ON절
- 조인 대상 필터링
- 연관 관계가 없는 엔티티 외부 조인 

## 서브쿼리
### 지원 함수
- EXISTS, ALL, ANY, SOME / IN
### 서브쿼리 한계
- JPA는 WHERE, HAVING절에서만 서브 쿼리 사용 가능
- SELECT절도 가능(하이버네이트에서 지원)
- FROM 절의 서브쿼리는 현재 JPQL에서 불가능
  - 조인으로 풀 수 있으면 풀어서 해결

## JPQL 타입 표현과 기타식
### JPQL 타입 표현
- ENUM : 패키지명 포함해서 
- 엔티티 타입 : TYPE(m) = Member (상속 관계에서 사용)

## 조건식 (CASE 등)
### CASE 식
- COALESCE : 하나씩 조회해서 null이 아니면 반환
- NULLIF : 두 값이 같으면 null 반환 다르면 첫번째 값 반환

## JPQL 함수 (47)
### 기본 함수
- CONCAT, SUBSTRING, TRIM, LENGTH, LOCATE, ...
### 사용자 정의 함수
- 하이버네이트는 사용 전 방언에 추가해야 함.
  - 사용하는 DB 방언을 상속받고, 사용자 정의 함수 등록
