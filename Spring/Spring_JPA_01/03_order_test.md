## 주문 기능 테스트
    @NoArgsConstructor(accsee = AccessLevel.PROTECTED)
    직접 생성자를 만드는 것을 방지
- 코드를 만들 때 제약을 만들어야 좋은 코드를 만들 수 있다.

데이터(entity)를 변경하면 dirty checking 데이터 변경 체크를 하여 JPA가 알아서 update, delete..등의 query를 날려줌

### 도메인 모델 패턴
- entity에 비지니스 로직을 몰아 넣는 것
- JPA는 이런 스타일에 최적화되어 있다.
### 트랜잭션 스크립트 패턴
- service에 비즈니스 로직을 넣는 것

어떤 것이 더 유지 보수할 때 더 좋은 것인지 생각하며 코드를 짜도록 한다.

    @RunWith(SpringRunner.class)
    @SpringBootTest
    @Transactional
    // given
    // when
    // then

- 테스트 코드를 작성 할 때에는 메서드 단위로 하는 것이 좋다


    cmd + shift + t 
    => 테스트 코드와 테스트 되는 코드를 번갈아 가며 볼 수 있음

