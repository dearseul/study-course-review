## 회원 등록

###영속성 컨텍스트
영속성 컨텍스트란 엔티티를 영구 저장 하는 환경 이라는 뜻이다.
애플리케이션이 데이터베이스에서 꺼내온 객체를 보관하는 역할을 한다. 영속성 컨텍스트는 엔티티 매니저( Entity Manager )를 통해 엔티티를 조회하거나 저장할때 엔티티를 보관하고 관리한다.

####엔티티 생명주기
- 비영속: 영속성 컨택스트와 관계가 없는 새로운 상태 


    // 엔티티를 생성
    Member member = new Member();
    member.setId("member1");
    member.setUsername("회원1");

- 영속: 엔티티 매니저를 통해 엔티티가 영속성 컨텍스트에 저장되어 관리되고 있는 상태


    // 엔티티 매니저를 통해 영속성 컨텍스트에 엔티티를 저장
    em.persist(entity);

- 준영속: 영속성 컨택스트에서 관리되다가 분리된 상태


    // 엔티티를 영속성 컨택스트에서 분리
    em.detach(entity);
    // 영속성 컨텍스트를 비우기
    em.clear();
    // 영속성 컨택스트를 종료
    em.close();

- 삭제: 영속성 컨택스트에서 삭제된 상태


    em.remove(entity)

### JPA constraints
 잘 사용하면 validation이 편하다.
- AssetFalse
- AssertTrue
- NotEmpty ...


    @NotEmpty(message= "");
    
    //controller
    if (result.hasError()) {
        return "";
    }





