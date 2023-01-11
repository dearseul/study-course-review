# 공통 인터페이스 기능 (8~11)

## 순수 JPA 기반 리포지토리 만들기
### 스프링 데이터 JPA가 구현 클래스 대신 생성
- ```org.springframework.data.repository.Repository```를 구현한 클래스는 스캔 대상
    - MemberRepository 인터페이스가 동작한 이유
    - 실제 출력해보면 Proxy 객체
- @Repository 생략 가능
    - 컴포넌트 스캔을 스프링 데이터 JPA가 자동으로 처리
    - JPA 예외를 스프링 예외로 변환하는 과정도 자동으로 처리

## 공통 인터페이스 설정

## 공통 인터페이스 적용

## 공통 인터페이스 분석
### JpaRepository 주요 기능
- 대부분의 공통 기능을 제공함
- 주요 메서드
    - save(S) : 새로운 엔티티는 저장하고 이미 있는 엔티티는 병합
    - delete(T) : 엔티티 하나를 삭제.
    - findById(ID)
    - getOne(ID) : 엔티티를 프록시로 조회
    - findAll() : 모든 엔티티 조회. 정렬이나 페이징 조건을 파라미터로 제공 가능