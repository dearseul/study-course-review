## 스프링  컨테이너와 스프링 빈

### 스프링 컨테이너 생성
````
ApplicationContext applicationContext = new AnnotationApplicationContext(AppConfig.class);
````
- ApplicationContext :  스프링 컨테이너 / 인터페이스
- 스프링 컨테이너는 XML 기반 or 애노테이션 기반의 자바 설정 클래스로 만들 수 있음

### 스프링 컨테이너의 생성 과정
1. 스프링 컨테이너 생성
- 생성할 때에는 구성정보(AppConfig.class)를 지정해주어야 함
- new AnnotationApplicationContext(AppConfig.class)
2. 스프링 빈 등록
- AppConfig의 @bean 객체들이 호출되어 스프링빈에 저장됨
- 빈 이름은 보통 메서드 이름과 같게 함
- 빈 이름은 항상 다른 이유를 부여해야 함
3. 스프링 빈 의존관계 설정
- 스프링 컨테이너는 설정 정보를 참고해서 의존관계를 주입
- 단순히 자바 코드를 호출하는 것과는 다른 개념
