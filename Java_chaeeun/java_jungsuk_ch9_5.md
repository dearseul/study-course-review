StringBuilder
-----

* StringBuilder는 동기화 X 
* StringBuffer는 동기화되어 있다. == 멀티 쓰레드에 안전(thread-safe) 
    + 싱글 쓰레드 : 한번에 1개 작업
    + 멀티 쓰레드 : 한번에 n개 작업 
        - 한번에 여러잡업을 같이 하므로 데이터 공유 ( 데이터가 꼬일 수 있음 )
        - 이런걸 막아주는 것이 동기화 (데이터 보호)
* 멀티쓰레드 프로그램이 아닌 경우, 동기화는 불필요한 성능 저하
* 이럴 땐 StringBuffer 대신 StringBuilder를 사용하면 성능 향상(싱글 스레드 프로그램)
```java
StringBuffer sb;
sb = new StringBuffer();
sb.append("abc");

// <==>
StringBuilder sb;
sb = new StringBuilder();
sb.append("abc");
```

> 지금까지 작성해온 프로그램은 전부 싱글쓰레드로 작성된 것이고 멀티쓰레드로 프로그램을 작성하는 법은 13장에서 배움 

Math 클래스
-----

* 수학관련 static 메서드의 집합
```java
public static final double E = 2.7182818285.... // 자연로그의 밑 
public static final double PI = 3.141592... // 원주율
```
* round()로 원하는 소수점 아래 세 번쨰 자리에서 반올림하기
    1. 원래 값에 100을 곱한다
        - 90.7552 * 100 -> 9075.52
    2. 위의 결과에 Math.round()를 사용한다.
        - Math.round(9075.52) -> 9076
    3. 위의 결과를 다시 100.0으로 나눈다.
        - 9076/100.0 -> 90.76
        - 9076.100 -> 90

Math클래스의 메서드
-----

* static double abs(double a)
* static double abs(float f)
* static double abs(int i)
* static double abs(long l)
    + 절대값 반환
* static double ceil(double a)
    + 올림하여 반환 
* static double floor(double a)
    + 버림하여 반환
* static double max(double a, double b)
* static double max(float a, float b)
* static double max(int a, int b)
* static double max(long a, long b)
    + 큰 값 반환
* static double min(double a, double b)
* static double min(float a, float b)
* static double min(int a, int b)
* static double min(long a, long b)
    + 작은 값 반환
* static double random()    
* static double rint(double a)
    + 짝수 반올림
* static double round(double a)
* static long round(float a)
    + 반올림 
