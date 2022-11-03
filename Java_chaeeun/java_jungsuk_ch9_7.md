문자열을 숫자로 변환하기
-----

* 문자열을 숫자로 변환하는 다양한 방법
    1. 문자열 -> 기본형
    ```java
    int i = new Integer("100").intValue();  //floatValue(), longValue(), ... 
    ```
    ```java
    int i2 = Integer.parseInt("100");
    ```
    2. 문자열 -> 래퍼클래스
    ```java
    Integer i3 = Integer.valueOf("100");
    ```
    ```java
    Integer i4 = new Integer("100");
    ```

* n진법의 문자열을 숫자로 변환하는 방법
```java
int i4 = Integer.parseInt("100",2); // 100(2) -> 4
int i5 = Integer.parseInt("100"8);  // 100(8) -> 64
int i6 = Integer.parseInt("100",16); // 100(16) -> 256
int i6 = Integer.parseInt("FF",16); // FF(16) -> 255
// int i6 = Integer.parseInt("FF"); // NumberForamtException 발생
```

오토박싱 & 언박싱
-----

* int(기본형) -> Integer(래퍼클래스) (오토박싱)
* Integer(래퍼클래스) -> int(기본형) (언박싱)
```java
int i = 5;
Integer iObj = new Integer(7);

int sum = i + iObj;     // XX 
// => 컴파일 후의 코드 
int i = 5; 
Integer iObj = new Integer(7);
int sum = i + iObj.intValue();  // 자동 언박싱 
``` 
* 기본형의 값을 객체로 자동변환하는 것을 오토박싱, 그 반대는 언박싱 
```java
ArrayList<Integer> list = new ArrayList<Integer>();
list.add(10);
// list.add(new Integer(10));   // 오토박싱 
int value = list.get(0);    
// list.get(0).intValue();  // 언박싱 
``` 

```java
class Ex9_1{
    public static void main(String[] args){
        int i = 10;

        // 기본형을 참조형으로 형변환(생략가능)
        Integer intg = (Integer)i;  // Integer intg = Integer.valueOf(i);   -- 컴파일러 
        Object obj = (Object)i; // Object obj = (Object)Integr.valueOf(i);   -- 컴파일러 

        Long lng = 100L;    // long lng = new Long(100L);

        int i2 = intg + 10; // 참조형과 기본형간의 연산가능 
        long l = intg + lng;    // 참조형간의 덧셈도 가능 

        Integer intg2 = new Integer(20);
        int i3 = (int)intg2;    // 참조형을 기본형으로 형변환도 가능 
    }
}
``` 



