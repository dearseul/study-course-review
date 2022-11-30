## 다양한 설정 형식 지원 - 자바코드, XML
- 스프링 컨테이너는 다양한 형식의 설정 정보를 받아들일 수 있게 유연하게 설계됨
    - 자바코드, XML, Groovy 등
  
### 에노테이션 기반 자바 코드 설정 사용
- ``new AnnotationConfigApplicationContext(AppConfig.class)``
- ``AnnotationConfigApplicationContext`` 클래스를 사용하면서 자바 코드로 된 설정 정보를 넘기면 됨

### XML 설정 사용
- 최근에는 스프링부트를 많이 사용하면서 XML 기반의 설정은 잘 사용하지 않음. 아직 많은 레거시 프로그램들이 
XML로 되어있고, 또 XML을 사용하면 컴파일 없이 빈 설정 정보를 변경할 수 있는 장점도 있으므로 한번쯤 배워둘만 함.
- ``GenericXmlApplicationContext``를 사용하면서 ``xml`` 설정 파일을 넘기면 됨  