## 필터
- ``includeFilters`` : 컴포넌트 스캔 대상을 추가로 지정
- ``excludeFilters`` : 컴포넌트 스캔에서 제외할 대상을 지정

### FilterType 옵션
- ANNOTATION : 기본값, 애노테이션을 인식해서 동작함
    - ex) ```org.example.SomeAnnotation```
- ASSIGNABLE_TYPE : 지정한 타입과 자식 타입을 인식해서 동작함
    - ex) ```org.example.SomeClass```
- ASPECTG : AspectJ 패턴 사용
    - ex) ```org.example..*Service+```
- REGEX : 정규 표현식
    - ex) ```org\.example\.Default.*```
- CUSTOM: : ``typeFilter``이라는 인터페이스를 구현해서 처리
    - ex) ``org.example.MyTypeFilter``

``` 
@Component면 충분하기 때문에 includeFilter를 사용할 일은 거의 없음.
excludeFilters는 여러가지 이유로 간혹 사용할 때가 있지만 많지는 않음.
특히 최근 스프링 부트는 컴포넌트 스캔을 기본으로 제공하는데, 강사 개인적으로는 옵션을 변경하면서 사용하기 보다는
스프링의 기본  설정에 최대한 맞추어 사용하는 것을 권장하고 선호함
```    