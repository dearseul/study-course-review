join()과 StringJoiner
-----

* join()은 여러 문자열 사이에 구분자를 넣어서 결합한다. 
```java
String animals = "dog,cat,bear";
String[] arr = animals.split(",");  
String str = String.join("-",arr);
System.out.println(str);    // dog-cat-bear
```

문자열과 기본형 간의 변환
-----

* 숫자를 문자열로 바꾸는 방법
```java
int i = 100;
String str1 = i + "";   // "100"                (편리)
String str2 = String.valueOf(i);    // "100"    (빠름)
```
* 문자열을 숫자로 바꾸는 방법 
```java
int i = Integer.parseInt("100");    // 100
int i2 = Integer.valueOf("100");    // 100
Integer i2 = Integer.valueof("100"); // 원래는 반환 타입이 Integer
```

StringBuffer 클래스
-----

* String 처럼 문자형 배열(char[])을 내부적으로 가지고 있다. 
```java
public final class StringBuffer implements java.io.Serializable {
    private char[] value;
    ...
}
```
* 그러나, String과 달리 내용을 변경할 수 있다.(mutable)
```java
StringBuffer sb = new StringBuffer("abc");
sb.append("123") ;   // sb 뒤에 "123"추가. 내용 변경 가능 
```

StringBuffer의 생성자
-----
* 배열은 길이 변경불가. 공간이 부족하면 새로운 배열 생성해야.
* StringBuffer는 저장할 문자열의 길이를 고려해서 적절한 크기로 생성해야 함. 
```java
public StringBuffer(int length){
    value = new char[length];
    shared = false;
}
public StringBuffer(){
    this(16);   // 버퍼의 크기를 지정하지 않으면 버퍼의 크기는 16이 된다. 
}
public StringBuffer(String str){
    this(str.length()+16);  // 지정한 문자열의 길이보다 16이 더 크게 버퍼를 생성한다.
    append(str);
}
```

* StringBuffer는 String과 달리 내용 변경이 가능하다. 
```java
StringBuffer sb = new StringBuffer("abc");
sb.append("123");   // 내용 추가 
// StringBuffer의 메서드 
// append();
// delete();
// insert();
// 반환타입이 StringBuffer
```
* append()는 지정된 내용을 StringBuffer에 추가 후, StringBuffer의 참조를 반환
```java
StringBuffer sb2 = sb.append("ZZ");
System.out.println(sb); // abc123ZZ 
System.out.println(sb2); // abc123ZZ
``` 
```java
StringBuffer sb = new StringBuffer("abc");
sb.append("123");
sb.append("zz");
// == 
StringBuffer sb = new StringBuffer("abc");
sb.append("123").append("ZZ");
```

* StringBuffer는 equals()가 오버라이딩 되어 있지 않다.(주소비교)
```java
StringBuffer sb = new StringBuffer("abc");
StringBuffer sb2 = new StringBuffer("abc");
System.out.println(sb==sb2); // false
System.out.println(sb.equals(sb2)); // false
```
* StringBuffer를 String으로 변환 후 equals()로 비교해야 한다.
```java
String s = sb.toString();
String s2 = sb2.toString();
System.out.println(s.equals(s2));   //true

