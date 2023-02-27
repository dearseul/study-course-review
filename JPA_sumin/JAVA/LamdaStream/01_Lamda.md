## 함수형 인터페이스
- 람다식을 다루기 위한 인터페이스.
- 오직 하나의 추상 메서드만 정의. static, default 메서드는 개수 제약 없음.
```java
@FunctionalInterface
interface MyFunction {
    void myMethod(); // 추상 메서드
}
```
- 메서드를 호출할 때 람다식을 참조하는 참조변수를 매개변수로 지정해야 함.
- 즉 변수처럼 메서드를 주고 받을 수 있게 됨.
- 람다식은 함수형 인터페이슬만 형변환이 가능
```java
() -> {}; // 에러
(MyFunction) () -> {}; // 정상
```
- 람다식 내에서 참조하는 지역변수는 final이 붙지 않아도 상수로 간주됨

## java.util.function 패키지
### 종류
- Supplier<T> : 매개변수는 없고 반환값만 있음
- Consumer<T> : 매개변수는 있고 반환값은 없음
- Function<T,R> : 일반적 함수. 매개변수를 받아서 결과를 반환
- Predicate<T> : 조건식을 표현할 때 사용. 매개변수는 하나, 반환값은 boolean
    - 반환값이 boolean이라는 점만 제외하면 Function과 동일함
```java
Predicate<String> isEmptyStr = s -> s.length() == 0;
String s = "";
if(isEmptyStr.test(s))
System.out.println("s is empty");
```
- 매개변수가 두개인 함수형 인터페이스
    - BiConsumer, BiFunction, BiPredicate
- UnaryOperator : Function의 자손. 매개변수와 결과의 타입이 같다는 차이.
- BinaryOperator : BiFunction의 자손. 매개변수와 결과의 타입이 같다는 차이.
### 컬렉션 프레임워크와 함수형 인터페이스
```java
list.forEach(i -> System.out.println(i+","));
list.removeIf(x -> x%2==0 || x%3==0);
list.replaceAll(i -> i*10);
map.forEach((k,v) -> System.out.println("k="+k+", v="+v));
```
- 매개변수 타입과 반환 타입이 일치할 때에는 Function 대신 UnaryOperator를 사용. 언박싱 오토박싱의 횟수가 줄어듦.
## Function의 합성과 Predicate의 결합
### Function의 합성
- andThen / compose / identify
### Predicate의 결합
- and / or / negate

## 메서드 참조
- static메서드 참조 
  - (x) -> ClassName.method(x)
  - ClassName::method
- 인스턴스메서드 참조
  - (obj,x) -> obj.method(x)
  - ClassName::method
- 특정 객체 인스턴스메서드 참조
  - (x) -> obj.method(x)
  - obj::method

























