## 2차시 라이브러리 살펴보기
- intellJ 오른편 gradle에 의존관계(dependencies)를 볼 수 있다.
- 예전에는 웹서버(WAS)를 직접 다운을 받아서, java code를 밀어넣는 식으로 작업했으나
요즘에는 내장(embed)되어 있어서 펀하게 코딩가능.
### 스프링 부트 라이브러리
- spring-boot-starter-logging
  - log를 통해 에러를 표시, (system.out.println X) 당연하지만 언급.
  - logback, slf4j
### 테스트 라이브러리
  - spring-boot-starter-test
    - JUnit: 테스트 프레임 워크
    - mockito: 목 라이브러리
    - assertJ: 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
    - spring-teset: 스프링 통합 테스트 지원
