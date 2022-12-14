# 영속성 관리 - 내부 동작 방식

## 영속성 컨텍스트 1 (7)
### JPA에서 가장 중요한 두가지
- 객체와 관계형 데이터베이스 매핑하기
- 영속성 컨텍스트

### 영속성 컨텍스트
- JPA를 이해하는데 가장 중요한 용어
- "엔티티를 영구 저장하는 환경" 이라는 뜻
- EntityManager.persist(entity);
- 영속성 컨텍스트는 논리적 개념. 눈에 보이지 않음.
- 엔티티 매니저를 통해 영속성 컨텍스트에 접근

### 엔티티의 생명 주기
- 비영속(new/transient) : 영속성 컨텍스트와 전혀 관계가 없는 새로운 상태
  - ex) 객체를 생성한 상태
- 영속(managed) : 영속성 컨텍스트에 관리되는 상태
  - ex) 객체 생성 후 객체를 저장한 상태
- 준영속(detached) : 영속성 컨텍스트에 저장되었다가 분리된 상태
- 삭제(removed) : 삭제된 상태
  
## 영속성 컨텍스트 2 (8)
### 이점
- 1차 캐시
  - 동일 트랜잭션에서 한번 조회 했던 거를 또 조회하면 db에서 조회 안 함. 1차 캐시에서 조회함.
- 영속 엔티티의 동일성 보장
- 엔티티 등록할 때 트랜잭션을 지원하는 쓰기 지연
- 엔티티 수정할 때 변경감지
- 지연로딩

## 플러시 (9)
- 영속성 컨텍스트의 변경 내용을 데이터베이스에 반영
### 플러시 발생
- 변경 감지
- 수정된 엔티티 쓰기 지연 SQL 저장소에 등록
- 쓰기 지연 SQL 저장소의 쿼리를 데이터베이스에 전송
### 영속성 컨텍스트를 플러시 하는 방법
- em.flush() : 직접 호출
- 트랜잭션 커밋 : 자동 호출
- JPQL 쿼리 실행 : 자동 호출
### 플러시 모드 옵션
- FlushModeType.AUTO : 쿼리 실행이나 커밋할 때. 기본값 
- FlushModeType.COMMIT : 커밋할 때에만 
### 플러시란
- 영속성 컨텍스트를 비우지 않음
- 영속성 컨텍스트의 변경 내용을 데이터베이스에 동기화
- 트랜잭션이라는 작업 단위가 중요 -> 커밋 직전에만 동기화 하면 됨

## 준영속 상태 (10)
- 영속 -> 준영속
- 영속 상태의 엔티티가 영속성 컨텍스트에서 분리
- 영속성 컨텍스트가 제공하는 기능을 사용 못함.
### 준영속 상태로 만드는 법
- em.detach(entity) : 특정 엔티티를 준영속 상태로 전환
- em.clear() : 영속성 컨텍스트를 완전히 초기화
- em.close() : 영속성 컨텍스트를 종료

## 정리 (11)