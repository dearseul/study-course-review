## Hello JPA - 프로젝트 생성 (5)
- 주의사항
    - pom.xml에서 h2의 버전은 반드시 설치 버전과 동일하게
    - hibernate도 spring의 hibernate 버전과 일치시키는게 좋음
> 데이터베이스 방언
> ```xml
>   <property name="hibernate.dialect" value="org.hibernate.dialect.H2Dialect"/>
>  ```
> jpa는 특정 데이터베이스에 종속되지 않음.   
> 각각의 데이터베이스가 제공하는 SQL 문법과 함수는 조금씩 다름   
> ex) 가변문자(varchar, varchar2), 페이징(Limit, Rownum)   
> 방언 : SQL 표준을 지키지 않는 특정 데이터베이스만의 고유한 기능

## Hello JPA - 애플리케이션 개발 (6)
### JPA 구동 방식
- Persistence 클래스에서 persistence.xml 파일의 설정 정보를 조회
- EntityManagerFactory를 생성해서, EntityManager들을 생성

### 주의
- 엔티티 매니저 팩토리는 하나만 생성해서 애플리케이션 전체에서 공유
- 엔티티 매니저는 쓰레드 간에 공유 X (사용하고 버려야 함)
- JPA의 모든 데이터 변경은 트랜잭션 안에서 실행

### 조회
- em.find
- 18세 이상인 사용자를 모두 조회하고 싶으면?
  - JPQL 사용
  
### JPQL 
- JPA를 사용하면 엔티티 객체를 중심으로 개발
- 문제는 검색 쿼리
- 검색을 할 때도 테이블이 아닌 엔티티 개체를 대상으로 검색
- 모든 DB 데이터를 객체로 변환해서 검색하는 것은 불가능
- 애플리케이션이 필요한 데이터만 DB에서 불러오려면 결국 검색 조건이 포함된 SQL이 필요

### JPQL 특징
- JPA는 SQL을 추상화한 JPQL이라는 객체 지향 쿼리 언어를 제공
- SQL과 문법 유사, SELECT, FROM, WHERE, GROUP BY, HAVING , JOIN 지원
- JPQL은 엔티티 객체를 대상으로 쿼리
  - 방언을 바꾸어도 JPQL 코드를 바꿀 필요가 없음.
- SQL은 데이터베이스 테이블을 대상으로 쿼리
- 테이블이 아닌 객체를 대상으로 검색하는 객체지향 쿼리. 즉 객체 지향 SQL