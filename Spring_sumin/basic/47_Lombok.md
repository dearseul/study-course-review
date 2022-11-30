## 롬복과 최신 트렌드
- 롬복 라이브러리가 제공하는 ``@RequiredArgsConstructor`` 기능을 사용하면 final이 붙은 필드를
모아서 생성자를 자동으로 만들어줌
  
### 정리
- 최근에는 생성자를 딱 1개 두고, ``@Autowired``를 생략하는 방법을 주로 사용함
- 여기에 lombok 라이브러리의 ``@RequiredArgsConstructor``를 함께 사용하면 기능은 다 제공하면서
코드는 깔끔하게 사용할 수 있음
  
