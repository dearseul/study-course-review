## 관심사의 분리

- 공연의 예 
  - 공연 기획자를 만들고, 배우와 공연 기획자의 책임을 분리

### AppConfig의 등장
- 애플리케이션의 동작 방식을 구성하기 위해, 구현 객체를 생성하고 연결하는 책임을 가지는 별도의 설정 클래스
    - 직접 new로 생성하지 않고, AppConfig 안에서 생성  
 
- 생성한 객체 인스턴스의 참조(레퍼런스)를 생성자를 사용하여 주입(연결)함
- DIP 완성 
- 관심사의 분리(객체의 생성, 연결 역할과 실행 역할의 분리)
- 클라이언트 입장에서 보면 의존관계를 마치 외부에서 주입해주는 것과 같다고 해서 DI(의존성 주입)이라 함.

