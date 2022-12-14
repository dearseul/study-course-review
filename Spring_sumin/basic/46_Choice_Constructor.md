## 생성자 주입을 선택해라
- 과거에는 수정자 주입과 필드 주입을 많이 사용했지만, 최근에는 스프링을 포함한 DI 프로젝트 대부분이 생성자
주입을 권장함
  
### 불변
- 대부분의 의존관계 주입은 한번 일어나면 애플리케이션 종료시점까지 의존관계를 변경할 일이 없음.
오히려 대부분의 의존관계는 애플리케이션 종료 전까지 변하면 안 됨
- 수정자 주입을 사용하면 setXxx 메서드를 public으로 열어두어야 함
- 누군가 실수로 변경할 수 있고, 변경하면 안 되는 메서드를 열어두는 것은 좋은 설계 방법이 아님
- 생성자 주입은 객체를 생성할 때 딱 1번만 호출되므로 이후에 호출되는 일이 없음.

### 누락
- 생성자 주입을 사용하면 주입 데이터를 누락했을 때 컴파일 오류가 발생함
- 그리고 IDE에서 바로 어떤 값을 필수로 주입해야 하는지 알 수 있음

### final 키워드
- 생성자 주입을 사용하면 필드에 ``final`` 키워드를 사용할 수 있음.
그래서 생성자에서 혹시라도 값이 설정되지 않는 오류를 컴파일 시점에서 막아줌
- 컴파일 오류가 가장 빠르고 좋은 오류임 !!  
``` 
참고
수정자 주입을 포함한 나머지 주입 방식은 모두 생성자 이후에 호출되므로, 필드에 final 키워드를 사용할 수 없음
오직 생성자 주입 방식만 final 키워드를 사용할 수 있음
```

### 정리
- 생성자 주입 방식을 선택하는 이유는 여러가지가 있지만, 프레임워크에 의존하지 않고, 순수한 자바 언어의 특징을
잘 살리는 방법이기도 함
- 기본으로 생성자 주입을 사용하고, 필수 값이 아닌 경우에는 수정자 주입 방식을 옵션으로 부여하면 됨. 생성자
주입과 수정자 주입을 동시에 사용 가능
- 항상 생성자 주입을 선택하라! 그리고 가끔 옵션이 필요하면 수정자 주입을 선택해라.