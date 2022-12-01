##  변경 감지와 병합
### 준영속 엔티티
- 영속성 엔티티가 더이상 관리하지 않음. 영속성 컨텍스트가 더는 관리하지 않는 엔티티
- 기존의 식별자를 가지고 있다. (DB에서 한번 저장되고 가져온 엔티티)
- 아무리 준영속 엔티티를 바꾼다고 한들, 데이터 베이스의 변화가 있지 않다.
### 준영속 엔티티를 수정하는 방법
- 변경 감지 기능 사용
- merge(병합) 사용

### 변경 감지 기능 사용
    java
    @Transactinal
    public void updateItem(Long itemId, Book bookParam) {
        item findItem = itemRepository.findOne(itemId);
        findItem.setName(param.geName());
        findItem.setPrice(param.gePrice());
        findItem.setStockQuantity(param.getStockQuantity());
    }
### 병합 사용
- 병합은 준영속 상태의 엔티티를 영속 상태로 변경할 때 사용하는 기능이다.

    
    @Transactional
        void update(Item itemParam) { 
        //itemParam: 파리미터로 넘어온 준영속 상태의 엔티티 
        Item mergeItem = em.merge(item);
    }

### 병합 동작 방식
1. merge()를실행한다.
2. 파라미터로 넘어온 준영속 엔티티의 식별자 값으로 1차 캐시에서 엔티티를 조회한다.
   2-1. 만약 1차 캐시에 엔티티가 없으면 데이터베이스에서 엔티티를 조회하고, 1차 캐시에 저장한다.
3. 조회한 영속 엔티티( mergeMember )에 member 엔티티의 값을 채워 넣는다. (member 엔티티의 모든 값
   을 mergeMember에 밀어 넣는다. 이때 mergeMember의 “회원1”이라는 이름이 “회원명변경”으로 바
   뀐다.)
4. 영속 상태인 mergeMember를 반환한다.
- 참고: 책 자바 ORM 표준 JPA 프로그래밍 3.6.5 

### 병합시 동작 방식을 간단히 정리
1. 준영속 엔티티의 식별자 값으로 영속 엔티티를 조회한다.
2. 영속 엔티티의 값을 준영속 엔티티의 값으로 모두 교체한다.(병합한다.)
3. 트랜잭션 커밋 시점에 변경 감지 기능이 동작해서 데이터베이스에 UPDATE SQL이 실행

- 주의: 변경 감지 기능을 사용하면 원하는 속성만 선택해서 변경할 수 있지만, 병합을 사용하면 모든 속성이 변경된다. 
- 병합시 값이 없으면 null 로 업데이트 할 위험도 있다. (병합은 모든 필드를 교체한다.)

### 가장 좋은 해결 방법
- 엔티티를 변경할 때는 항상 변경 감지를 사용하세요
- 컨트롤러에서 어설프게 엔티티를 생성하지 마세요.
- 트랜잭션이 있는 서비스 계층에 식별자( id )와 변경할 데이터를 명확하게 전달하세요.
  - (파라미터 or dto) 트랜잭션이 있는 서비스 계층에서 영속 상태의 엔티티를 조회하고, 
  엔티티의 데이터를 직접 변경하세요. 트랜잭션 커밋 시점에 변경 감지가 실행됩니다.
