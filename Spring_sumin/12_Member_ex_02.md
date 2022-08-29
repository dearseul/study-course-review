## 멤버 조회 개발 예제

### 테스트
- given -> when -> then 순서로 코딩하여 테스트
- 테스트 코드 예시) Assertions.assertThat(member).isEqualTo(findMember)

### 설계상 문제점
- MemberServiceImpl 클래스에서 MemberRepository = new MemoryMemberRepository 로 구현한다면 문제점은?
    - MemberServiceImpl 클래스가 인터페이스와 구현체 모두에 의존한다는 점.
    - 즉 DI를 위반한다는 문제점이 있음.