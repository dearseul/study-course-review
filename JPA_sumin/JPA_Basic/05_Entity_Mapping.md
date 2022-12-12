# 엔티티 매핑

## 객체와 테이블 매핑 (12)
### 엔티티 매핑
- 객체와 테이블 매핑 : @Entity, @Table
- 필드와 컬럼 매핑 : @Column
- 기본 키 매핑 : @Id
- 연관관계 매핑 : @ManyToOne, @JoinColumn

### 객체와 테이블 매핑
- @Entity
    - @Entity가 붙은 클래스는 JPA가 관리, 엔티티라 함
    - JPA를 사용해서 테이블과 매핑할 클래스는 @Entity가 필수
    - 주의
        - 기본 생성자 필수. 
        - final 클래스, enum, interface, inner 클래스 사용 X
        - 저장할 필드에 final 사용 X
    - 속성
        - name
- @Table
    - 엔티티와 매핑할 테이블 지정
    
## 데이터베이스 스키마 자동 생성 (13)
- DDL을 애플리케이션 실행 시점에 자동 생성
- 테이블 중심 -> 객체 중심
- 데이터베이스 방언을 활용해서 데티어베이스에 맞는 적절한 DDL 생성
- 이렇게 생성된 DDL은 개발 장비에서만 사용
- 생성된 DDL은 운영서버에서는 사용하지 않거나, 적절히 다듬은 후 사용
### 속성
- create : 기존 테이블 삭제 후 다시 생성 (Drop + Create)
- create-drop : create와 같으나 종료 시점에 테이블 Drop
- update : 변경분만 반영 (운영 DB에는 사용하면 안 됨)
- validate : 엔티티와 테이블이 정상 매핑되었는지만 확인
- none : 사용하지 않음
### 주의점
- 운영 장비에는 절대 create, create-drop, update 사용하면 안 됨
- 개발 초기 단계는 create 또는 update
- 테스트 서버는 update 또는 validate
- 스테이징과 운영 서버는 validate 또는 none
### DDL 생성 기능
- 제약 조건 추가
    - ex) @Column(unique=true, length=10)
- DDL  생성 기능은 DDL을 자동 생성할 때에만 사용되고 JPA의 실행 로직에는 영향을 안 줌

## 필드와 컬럼 매핑 (14)
### 매핑 어노테이션 정리
- @Column 
  - name, insertable, updatable, nullable, unique, length, columnDefinition
- @Temporal : 날짜 타입 매핑
  - 하이버네이트 최신 버전에서는 생략해도 됨
- @Enumerated : enum 타입 매핑
  - EnumType을 쓸 때에는 Ordinal 사용 X
- @Lob : clob, blob 매핑
- @Transient : 메모리에서만 사용하고 싶을 때

## 기본 키 매핑 (15)
### 기본 키 매핑 방법
- 직접 할당 : @Id만 사용
- 자동 생성 (@GeneratedValue)
    - IDENTITY : 데이터베이스에 위임
    - SEQUENCE : 시퀀스로 생성
    - TABLE : 키 생성 전용 테이블을 만들어 데이터베이스 시퀀스를 흉내내는 전략
### 권장하는 식별자 전략
- 기본 키 제약 조건 : null 아님, 유일, 변하면 안 됨
- 미래까지 이 조건을 만족하는 자연 키(전화번호, 주민번호)는 찾기 어려움. 대리 키를 사용하자.
- 권장 : Long형 + 대체키 + 키 생성 전략
### IDENTITY 전략 - 특징
- 기본 키 생성을 데이터베이스에 위임
- 주로 MySql, PostgreSql, SQL Server, DB2에서 사용
- JPA는 보통 트랜잭션 커밋 시점에 Insert Sql 실행
- Auto_Increment는 데이터베이스에 Insert Sql을 실행한 후에 ID 값을 알 수 있음
- IDENTITY 전략은 em.persist() 시점에 즉시 Insert Sql을 실행하고 DB에서 식별자 조회

## 실전 예제1 - 요구사항 분석과 기본 매핑 (16)
### 데이터 중심 설계의 문제점
```java
@Entity
@Table(name = "orders")
public class Order {
    
    private String memberId;
```
- 현재 방식은 객체 설계를 테이블 설계에 맞춘 방식
- 테이블의 외래키를 객체에 그대로 가져옴
- 객체 그래프 탐색이 불가능
- 참조가 없으므로 UML도 잘못됨


























