# 객체지향 쿼리 언어2 - 중급 문법

## 경로 표현식 (48)
### 경로 표현식
- .(점)을 찍어 객체 그래프를 탐색하는 것
```java
select m.username // 상태 필드
from Member m 
join m.team t // 단일 값 연관 필드
join m.orders o // 컬렉션 값 연관 필드
WHERE t.name = '팀A'
```
### 용어 정리
- 상태 필드 : 단순히 값을 저장하기 위한 필드
  - 경로 탐색의 끝, 더 이상 탐색 X
- 연관 필드 : 연관관계를 위한 필드
    - 단일 값 연관 필드 : @ManyToOne, @OneToOne
      - 묵시적 내부 조인 발생, 탐색 O
    - 칼렉션 값 연관 필드 : @OneToMany @ManyToMany
      - 묵시적 내부 조인 발생, 탐색 X
      - FROM 절에서 명시적 조인을 통해 별칭을 얻으면 별칭을 통해 탐색 가능
### 명시적 조인, 묵시적 조인
- 명시적 조인 : join 키워드 직접 사용
- 묵시적 조인 : 경로 표현식에 의해 묵시적으로 SQL 조인 발생 (내부 조인만 가능)
- 가급적 묵시적 조인보다는 명시적 조인 사용하기.
    - 조인은 SQL 튜닝에 중요 포인트이기 때문
    - 묵시적 조인은 조인이 일어나는 상황을 한눈에 파악하기 어려움

## 페치 조인 1 - 기본 (중요!!!)
### 페치 조인
- SQL의 종류가 아님
- JPQL에서 성능 최적화를 위해 제공하는 기능
- 연관된 엔티티나 컬렉션을 SQL 한 번에 함께 조회하는 기능
- join fetch 명령어 사용
### 다대일 조인
- SELECT m FROM Member m join fetch m.team;
- 관계가 LAZY여도 페치 조인이 우선적으로 적용됨 
### 일대다 조인
- 컬렉션 조인
- SELECT t FROM Team t join fetch t.members;
- members의 크기에 따라 중복 조회 발생 가능
### 페치 조인과 DISTINCT
- SQL의 DISTINCT는 중복된 결과를 제거하는 명령
- JPQL의 DISTINCT 2가지 기능 제공
    - SQL에 DISTINCT를 추가
    - 애플리케이션에서 엔티티의 중복 제거 
### 페치 조인과 일반 조인의 차이
- 일반 조인 실행시 연관된 엔티티를 함께 조회하지 않음
- JPQL은 결과를 반환할 때 연관관계 고려 X. 단지 SELECT 절에 지정한 엔티티만 조회
- 페치 조인을 사용할 때에는 연관된 엔티티도 함께 조회 (즉시로딩)
- 페치 조인은 객체 그래프를 SQL 한번에 조회하는 개념

## 페치 조인 2 - 한계 
### 페치 조인의 한계
- 페치 조인 대상에는 별칭을 줄 수가 없음
- 둘 이상의 컬렉션은 페치 조인 할 수 없음
- 컬렉션을 페치 조인하면 페이징 API(setFirstResult, setMaxResults)를 사용할 수 없음
### 페치 조인의 특징과 한계
- 연관된 엔티티들을 SQL 한 번에 조회 - 성능 최적화
- 엔티티에 직접 적용하는 글로벌 로딩 전략보다 우선함
    - @OneToMany(fetch = FetchType.LAZY) // 글로벌 로딩 전략
- 실무에서 글로벌 로딩 전략은 모두 지연 로딩
- 최적화가 필요한 곳은 페치 조인 적용
### 페치 조인 - 정리
- 모든 것을 페치 조인으로 해결할 수는 없음
- 페치 조인은 객체 그래프를 유지할 때 사용하면 효과적
- 여러 테이블을 조인해서 엔티티가 가진 모양이 아닌 전혀 다른 결과를 내야 하면, 
페치 조인 보다는 일반 조인을 사용하고 필요한 데이터들만 조회해서 DTO로 반환하는 것이 효과적

## 다형성 쿼리
### Type
- 조회 대상을 특정 자식으로 한정
- SELECT i FROM Item i WHERE type(i) IN (Book, Movie);
### Treat
- 자바의 캐스팅 타입과 유사
- SELECT i FROM Item i WHERE treat(i AS Book).author = 'Kim'

## 엔티티 직접 사용
### 엔티티 직접 사용 - 기본 키 값
- JPQL에서 엔티티를 직접 사용하면 SQL에서 해당 엔티티의 기본 키 값을 사용
    - count(m) -> count(m.id)
### 엔티티의 직접 사용 - 외래 키 값    

## Named 쿼리
### Named 쿼리 - 정적 쿼리
```java
@Entity
@NamedQuery(
        name = "Member.findByUsername",
        query = "select m from Member m where m.username = :username"
)
```
- 미리 정의해서 이름을 부여해두고 사용하는 JPQL
- 정적 쿼리
- 어노테이션, XML에 정의
- 애플리케이션 로딩 시점에 초기화 후 재사용
- 애플리케이션 로딩 시점에 쿼리를 검증

## 벌크 연산 (54)
### 벌크 연산
- 쿼리 한번으로 여러 테이블의 로우 변경
### 벌크 연산 주의
- 벌크 연산은 영속성 컨텍스트를 무시하고 데이터베이스에 직접 쿼리
    - 벌크 연산을 먼저 실행
    - 벌크 연산 수행 후 영속성 컨텍스트 초기화
    ```java
    int resultCnt = em.createQuery("update Member m set m.age=20").executeUpdate();
    em.clear();
    ```
  