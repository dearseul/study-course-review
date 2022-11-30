## 멤버 조회 개발 예제

### 설계
- Member - 회원조회(회원가입, 조회) - 회원저장소(메모리저장소, db저장소, 외부저장소 등)
- 여기서 MemberService 인터페이스에 회원가입, 조회 기능이 있으며 이를 구현하는 MemberServiceImpl 구현체가 있다.
- MemberRepository 인터페이스에 저장, 조회 기능이 있으며 이를 구현하는 MemoryMemberRepository, DBMemberRepository 등의 구현체가 있다. 

tip
> 인터페이스와 구현체를 다른 패키지에 두는 게 좋음.
> 인터페이스의 구현체가 하나일 경우에는 구현체의 파일 명을 ~Impl 하는 경우가 많음.
> 클래스 다이어그램은 정적이고, 객체 다이어그램은 동적이다.