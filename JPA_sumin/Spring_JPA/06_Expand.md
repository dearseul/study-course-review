# 확장 기능 (23~26)

## 사용자 정의 리포지토리 구현
- 스프링 데이터 JPA 리포지토리는 인터페이스만 정의하고 구현체는 스프링이 자동 생성
- 스프링 데이터 JPA가 제공하는 인터페이스를 직접 구현해야 하는 기능이 너무 많음
- 다양한 이유로 인터페이스의 메서드를 직접 구현하고 싶다면?
    - JPA 직접 사용 (EntityManager)
    - 스프링 JDBC Template 사용
    - MyBatis 사용
    - 데이터베이스 커넥션 직접 사용 등
    - Querydsl 사용

## Auditing
- 엔티티를 생성, 변경할 때 변경한 사람과 시간을 추적하고 싶으면?
    - 등록일, 수정일, 등록자, 수정자
### Jpa 주요 이벤트 어노테이션
- @PrePersist, @PostPersist
- @PreUpdate, @PostUpdate
### 스프링 데이터 JPA 사용
- @EnableJpaAuditing 넣는 거 까먹지 말기

## Web 확장 - 도메인 클래스 컨버터
- HTTP 파라미터로 넘어온 엔티티의 아이디로 엔티티 객체를 찾아서 바인딩
```java
@GetMapping("/members/{id}")
public String findMember(@PathVariable("id") Long id) {
    Member member = memberRepository.findById(id).get();
    return member.getUsername();
}

@GetMapping("/members2/{id}")
public String findMember2(@PathVariable("id") Member member) {
    return member.getUsername();
}

@PostConstruct
public void init() {
    memberRepository.save(new Member("userA"));
    }
```
- 주의) 도메인 클래스 컨버터로 엔티티를 파라미터로 받으면, 이 엔티티는 단순 조회용으로만 사용해야 함

## Web 확장 - 페이징과 정렬
### 요청 파라미터
- page, size, sort
### 기본값
```java
  Data:
    web:
      pageable:
        default-page-size: 10
        max-page-size: 2000
```
```java
    @GetMapping("/members")
    public Page<Member> list(@PageableDefault(size = 5, sort = "username") Pageable pageable) {
        Page<Member> page = memberRepository.findAll(pageable);
        return page;
    }
```
### 접두사
- 페이징 정보가 둘 이상이면 접두사로 구분
- @Qualifier에 접두사명 추가 
### Page 내용을 Dto로 변환하기
```java
    @GetMapping("/members")
    public Page<MemberDto> list(@PageableDefault(size = 5, sort = "username") Pageable pageable) {
        Page<Member> page = memberRepository.findAll(pageable);
        return page.map(member -> new MemberDto(member.getId(), member.getUsername(), null));
    }
```
### Page를 1부터 시작하기
