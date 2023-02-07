## 프로젝션과 결과 반환 - 기본
### 프로젝션 대상이 하나
- 프로젝션 대상이 하나면 타입을 명확하게 지정 가능
- 프로젝션 대상이 둘 이상이면 튜플이나 DTO로 조회

## 프로젝션과 결과 반환 - DTO
### 순수 JPA에서 DTO 조회할 때
- 순수 JPA에서 DTO를 조회할 때에는 new 명령어를 사용
- DTO의 package 이름을 다 적어줘야 해서 지저분함
- 생성자 방식만 지원함
### Querydsl 빈 생성
- 프로퍼티 접근, 필드 직접 접근, 생성자 사용

## 프로젝션과 결과 반환 - QueryProjection
- 컴파일러로 타입을 체크할 수 있으므로 가장 안전한 방법.
- 다만 DTO에 QueryDSL 어노테이션을 유지해야 한다는 점과 DTO까지 Q 파일을 생성해야 한다는 단점이 있음

## 수정, 삭제 벌크 연산
- 벌크 연산은 기본적으로 DB에 바로 반영함
- 따라서 영속성 컨텍스트와 충돌이 날 수 있는데, 이 때 덮어쓰는 게 아니라, 영속성 컨텍스트의 값이 출력됨
- 충돌 방지를 위해서 flush, clear를 먼저 해주기

