String 클래스
-----

* String 클래스 = 데이터(char[]) + 메서드(문자열 관련)
```java
public final class String implements java.io.Serializable, Comparable{
    private char[] value;
    ...
}
```
* 내용을 변경할 수 없는 불변(immutable)클래스 
```java
String a = "a";
String b = "b";
a = a + b;
// 완전히 새로운 문자열 "ab"가 생기고 
// a 참조변수가 "ab"를 가리키게 된다. 
```
* 덧셈 연산자(+)를 이용한 문자열 결합은 성능이 떨어짐.
* 문자열의 결합이나 변경이 잦다면, 내용을 변경가능한 StringBuffer를 사용 


문자열의 비교
-----

* String str = "abc" 와 str = new String("abc"); 의 비교
```java
String str1 = "abc";            // 문자열 리터럴 "abc"의 주소가 str1에 저장됨
String str2 = "abc";            // 문자열 리터럴 "abc"의 주소가 str2에 저장됨
String str3 = new String("abc");    // 새로운 String 인스턴스 생성
String str4 = new String("abc");    // 새로운 String 인스턴스 생성 

str1 == str2 // true    
str3 == str4 // true    
str1.equals(str2) // true
str3.equals(str4) // true 
// 문자열은 내용 변경 불가이므로 여러 참조변수가 공유해도 문제 없다. 
```

문자열 리터럴
-----

* 문자열 리터럴은 프로그램 실행 시 자동으로 생성된다.(constant pool에 저장)
```java
class Ex9_2{
    public static void main(String[] args){
        String s1 = "AAA";
        String s2 = "AAA";
        String s3 = "AAA";
        String s4 = "BBB";
    }
}
// s1, s2, s3 모두 문자열 리터럴 "AAA"를 가리킨다. 
```

빈 문자열("", empty string)
-----

* 내용이 없는 문자열. 크기가 0인 char형 배열을 저장하는 문자열 
```java
String str = ""; // str을 빈 문자열로 초기화
```
* 크기가 0인 배열을 생성하는 것은 어느 타입이나 가능 
```java
char[] chArr = new char[0]; // 길이가 0인 char배열 
int[] iArr = {};            // 길이가 0인 int 배열 
```

* 문자(char)와 문자열(String)의 초기화
```java
String s = null;                            
char c = '\u0000';  // 유니코드 첫번째 문자 

// 위 코드 보다 아래 코드로 초기화 하는게 좋음 
String s = "";  //  빈 문자열로 초기화
char c = ' '; // 공백으로 초기화 
```

String 클래스의 생성자와 메서드
-----

* String(String s)  (잘 안씀)
    - 생성자. 주어진 문자열(s)을 갖는 String인스턴스를 생성한다. 
* String(char[] value)
    - 캐릭터 배열을 String으로 바꿔줄 때 쓰는 생성자 
    ```java
    char[] = {'H','e','l','l','o'};
    String s = new String(c);
    s = "Hello"
    ```
    - 반대로 바꿀 때는 toCharArray()
* String(StringBuffer buf)
    - StringBuffer: 내용 변경가능한 문자열 
    - String으로 바꿔줄 때 쓰는 생성자 
    - 반대로 바꿀때는 StringBuffer 생성자 사용 
* char charAt(int index)
    - 지정된 index의 문자 한개 반환 
    ```java
    String s = "Hello";
    String n = "012345";
    char c = s.charAt(1);   // c = 'e'
    char c2 = n.charAt(1);  // c2 = '1'
    ```
* int compareTo(String str)
    - 문자열(str)과 사전순서로 비교한다. 
    - 같으면 0, 사전순서 이전이면 음수, 이후이면 양수 반환 
    ```java
    int i = "aaa".compareTo("aaa"); // i = 0
    int i2 = "aaa".compareTo("bbb");// i2 = -1
    int i3 = "bbb".compareTo("aaa");// i3 = 1
    ```
    - 정렬할 때 사용 
* String concat(String str)
    - 문자열 붙임 
    ```java
    String s = "Hello";
    String s2 = s.concat(" World"); // s2 = "Hello World"
    ```
* boolean contains(CharSequence s)
    - 지정된 문자열(s)가 포함되어있는지 검사한다. 
    ```java
    String s = "abcdefg";
    boolean b = s.contains("bc");   // b = true
    ```
    - cf) Interface CharSequence (인터페이스 장점: 서로 관계없는 클래스들의 관계를 맺어줄 수 있다.)x
    - CharSequence라는 인터페이스를 구현한 클래스들: 
    - CharBuffer, Segment, String, StringBuffer, StringBuilder
    - CharSequence를 매개변수로 해놨으므로 얘네들을 다 매개변수로 쓸 수 있음
* boolean endsWith(String suffix)
    - 지정된 문자열(suffix로 끝나는지 검사한다.)
    ```java
    String file = "Hello txt";
    boolean b = file.endsWith("txt");   // true
    ```
    - 반대로 startsWith 도 있다. 
* boolean equals(Object obj)
* boolean equalsIgnoreCase(String str)
    - 대소문자 구분 없이 비교 
    ```java
    String s = "Hello";
    s.equalsIgnoreCase("HELLO");    // TRUE
    ```
* int indexOf(int ch)
    - 주어진 문자(ch)가 문자열에 존재하는지 확인하여 위치(Index)를 알려준다. 
    - 없으면 -1, 있으면 index 반환

* int indexOf(int ch, int pos)
    - pos: 검색 시작 위치 
    ```java
    String s = "Hello";
    int idx1 = s.indexOf('e',0);    // 1
    int idx1 = s.indexOf('e',2);    // -1
    ```
* int indexOf(String str)
    - 문자열 찾기
    ```java
    String s = "ABCDEFG";
    int idx = s.indexOF("CD");  // 2 
    ```
* int lastIndexOf(int ch)
    - 뒤에서 부터 찾음 
    - index는 앞에서 부터. 

* int lastIndexOf(String str)
* int length()
    - 문자열의 길이 


* String[] split(string regex)
    - 문자열을 지정된 분리자(regex)로 나누어 문자열 배열에 담아 반환한다.
    ```java
    String animals = "Dog,Cat,Bear";
    String[] arr = animals.split(",");  // arr[0] = "Dog", arr[1] = "Cat", .. 
    ```
* String[] split(String regex, int limit)
    - 지정된 수 까지만 짜른다.
    ```java
    String[] arr = animals.split(",",2); // arr[0] = "Dog", arr[1] = "Cat,Bear" 
    ```
* boolean startsWith(String prefix)
    - prefix로 시작하는지 검사.
* String substring(int begin)
* String substring(int begin, int end)
    - begin부터 end까지 자름 
    - end 없으면 문자열 길이까지 
    - end 인덱스 위치 문자는 포함되지 않음 

* String toLowerCase()
    - 소문자로 바꿈
* String toUpperCase()
* String trim()
    - 양쪽 끝 공백 제거 
* static String valueOf(boolean b)  
* static String valueOf(char c)  
* static String valueOf(int i)  
* static String valueOf(long l)  
* static String valueOf(float f)  
* static String valueOf(double d)  
* static String valueOf(Object o)
    - String 문자열로 변환 
    
















