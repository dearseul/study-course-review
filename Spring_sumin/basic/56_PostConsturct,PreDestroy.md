## 애노테이션 @PostConstruct, @PreDestroy

- 이 방법을 쓰면 됨

### @PostConstruct, @PreDestroy 특징
- 최신 스프링에서 권장하는 방법
- 패키지를 보면 ``javax.annotation.PostConstruct``임. 스프링에 종속적인 기술이 아니라 자바 표준임.
따라서 스프링이 아닌 다른 컨테이너에서도 동작함
- 컴포넌트 스캔과 잘 어울림
- 유일한 단점은 외부 라이브러리에 적용하지 못한다는 것. 외부 라이브러리를 초기화, 종료 해야 하면 
@Bean 메서드를 사용해야 함
  

### 정리
- @PostConstruct, @PreDestroy를 사용하자
- 코드를 고칠 수 없는 외부 라이브러리를 초기화, 종료 해야하면 ``@Bean``의 ``initMethod``, 
  ``destroyMethod``를 사용하자