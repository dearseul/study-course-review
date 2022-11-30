## 옵션 처리
- 주입할 스프링 빈이 없어도 동작해야 할 때가 있음
- 그런데 ``@Autowired``만 사용하면 ``@Required``옵션의 기본 값이 true로 되어 있어서
자동 주입 대상이 없으면 오류가 발생

### 자동 주입 대상을 옵션으로 처리하는 방법  
- ``@Autowired(required=false)`` : 자동 주입할 대상이 없으면  수정자 메서드 자체가 호출 안 됨
- ``org.springframework.lang.@Nullable`` : 자동 주입할 대상이 없으면 null이 입력됨
- ``Optional<>`` : 자동 주입할 대상이 없으면 ``Optional.empty``가 입력됨