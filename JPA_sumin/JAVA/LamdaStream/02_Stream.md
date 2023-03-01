## 스트림이란
- 데이터 소스를 추상화하고 데이터를 다루는데 자주 사용되는 메서드들을 정의
### 특징
- 데이터 소스를 변경하지 않음.
- 일회용임
- 작업을 내부 반복으로 처리함. ex) forEach
### 연산
- 종류
    - 중간 연산 : 연산 결과가 스트림인 연산. 스트림에 연속해서 중간 연산 가능
      - map, flatMap
    - 최종 연산 : 연산 결과가 스트림이 아닌 연산. 스트림의 요소를 소모하므로 한번만 가능
      - reduce, collect
- 지연된 연산 : 최종 연산이 수행되기 전에 중간 연산이 수행되지 않음
- 병렬 처리가 쉬움

## 스트림 만들기
### 컬렉션
- Collection에 stream()이 정의되어 있어 List, Set 등에서 사용 가능
- 같은 스트림에 대해서 forEach를 두번 실행할 수 없음
### 배열
- Stream.of(), IntStream.of(), Arrays.stream() 등
### 특정 범위의 정수
- range(end 미포함), rangeClosed(end 포함)
### 임의의 수
- ins(), longs(), doubles()
    - 해당 타입의 난수들로 이루어진 스트림을 반환. 무한 스트림.
- limit() or ins(숫자) 사용하여 유한 스트림으로 변경 가능. 
- ins(사이즈, begin, end) 가능
### 람다식
- 람다식을 매개변수로 받아서 이 람다식에 의해 계산되는 값들을 요소로 하는 무한 스트림 생성
- iterate(T seed, UnaryOperator<T> f)
    - 씨앗값부터 시작해서 람다식 f에 의해 계산된 결과를 다시 seed값으로 해서 계산을 반복
- generate(Supplier<T> s)
    - 이전 결과를 이용하여 다음 요소를 계산하지 않음
    - Supplier<T> 이므로 매개변수가 없는 람다식만 허용
- 기본형 스트림 타입의 참조 변수로 다룰 수 없음.
```java
IntStream evenStream = Stream.iterate(0, n->n+2); // 에러
```
### 파일
- 파일의 목록이나 파일의 행을 요소로 하는 스트림 생성
### 기타
- Stream.empty() : 빈 스트림
- Stream.count() : 스트림 요소의 개수 반환
- Stream.concat(str1, str2) : 두 스트림을 하나로 연결

## 스트림의 중간연산
### 스트림 자르기
- skip(3) : 처음 3개 요소 건너뜀
- limit(5) : 스트림의 요소를 5개로 제한함
### 스트림 요소 걸러내기
- filter(Predicate<?, super T> predicate) : 여러번 쓰기 가능
- distinct()
### 정렬
- sorted(Comparator.comparing(String::length))
- 스트림의 요소가 Comparable을 구현한 경우 매개변수 하나짜리를 사용. 그렇지 않은 경우 추가적인 매개변수를
정렬기준으로 따로 지정
- 비교 대상이 기본형인 경우, comparing() 대신 comparingInt, Double, Long 사용하여 효율 높이기.
### 변환
- map(Function)
- mapToInt(), mapToLong(), mapToDouble()
    - Stream<T>는 count() 메서드만 제공하는 반면, 위 메서드들은 sum(), average(), max(), min() 제공
    - 단 결과가 최종 연산이기에 호출 후 메서드가 닫힘. 
    - 따라서 summaryStatics() 메서드 제공
    - mapToInt()와 함께 자주 사용되는 메서드로는 Integer.parseInt()나 valueOf()가 있음.
### 조회
- peek()
- 연산과 연산 사이에 올바르게 처리되었는지 확인할 때 사용
### flatMap()
- Stram<T[]>를 Stream<T>로 변환
