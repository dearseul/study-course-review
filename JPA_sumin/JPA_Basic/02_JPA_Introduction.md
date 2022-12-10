## JPA 소개
### ORM
- Object-relational-Mapping 객체형 관계 매핑
- 객체는 객체대로 설계
- 관계형 데이터베이스는 관계형 데이터베이스대로 설계
- ORM 프레임워크가 중간에서 매핑
- 대중적인 언어에는 대부분 ORM 기술이 존재

### JPA
- 애플리케이션과 JDBC 사이에서 동작
  - Entity 분석, insert sql 작성, JDBC Api 사용, 패러다임 불일치 해결

### JPA 사용 이유
- 생산성
  - 저장 : jpa.persist
  - 조회 : jpa.find
  - 수정 : jpa.setName("변경할 이름")
  - 삭제 : jpa.remove
- 유지보수
- 상속
- 신뢰할 수 있는 엔티티, 계층

### JPA의 성능 최적화
- 1차 캐시와 동일성 보장
  - 같은 트랜잭션 안에서는 같은 엔티티를 반환
- 트랜잭션을 지원하는 쓰기 지원
  - 트랜잭션을 커밋할 때까지 insert sql을 모음
  - JDBC Batch Sql 기능을 사용하여 한번에 전송
- 지연 로딩과 즉시 로딩
  - 지연 로딩 : 객체가 실제 사용될 때 로딩
  - 즉시 로딩 : JSON SQL로 한번에 연관된 객체까지 미리 조회
  
