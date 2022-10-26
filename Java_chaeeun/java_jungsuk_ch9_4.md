StringBuffer의 생성자와 메서드
-----

* StringBuffer()
    - StringBuffer sb = new StringBuffer();
    - 길이가 16인 배열
* StringBuffer(int length)
    - length + 16 배열 
* StringBuffer(String str)
* StringBuffer append(boolean b)
* StringBuffer append(char c)
* StringBuffer append(char[] str)
* StringBuffer append(double d)
* StringBuffer append(float f)
* StringBuffer append(int i)
* StringBuffer append(long l)
* StringBuffer append(Object obj)
* StringBuffer append(String str)
```java
StringBuffer sb = new StringBuffer("abc");
StringBuffer sb2 = sb.append(true);
sb.append('d').append(10.0);

StringBuffer sb3 = sb.append("ABC").append(123);

// sb = "abctrued10.0ABC123"
// sb2 = "abctrued10.0ABC123"
// sb3 = "abctrued10.0ABC123"
```
* int capacity()
    + StringBuffer의 버퍼크기(char[])를 알려준다. 
    + length()는 버퍼에 담긴 문자열의 길이를 알려준다. 
```java
StringBuffer sb = new StringBuffer(100);
sb.append("abcd");
int bufferSize = sb.capacity();
int stringSize = sb.length();
// bufferSize = 100
// stringSize = 4 (sb에 담긴 문자열 "abcd")
```
* char charAt(int index)
```java
StringBuffer sb = new StringBuffer("abc");
char c = sb.charAt(2);
// c = 'c'
```
* StringBuffer delete(int start, int end)
    + 시작위치(start)부터 끝 위치(end) 사이에 있는 문자를 제거한다.
    + 단, 끝 위치 문자는 제외 
```java
StringBuffer sb = new StringBuffer("0123456");
StringBuffer sb3 = new sb.delete(3,6);
// sb = "0126"
// sb2 = "0126"
```
* StringBuffer deleteCharAt(int index)
    + 문자 한개 제거
```java
StringBuffer sb = new StringBuffer("0123456");
sb.deleteCharAt(3);
// sb = "012456"
```

* StringBuffer insert(int pos, boolean b)
* StringBuffer insert(int pos, char c)
* StringBuffer insert(int pos, char[] str)
* StringBuffer insert(int pos, double d)
* StringBuffer insert(int pos, float f)
* StringBuffer insert(int pos, int i)
* StringBuffer insert(int pos, long l)
* StringBuffer insert(int pos, Object obj)
* StringBuffer insert(int pos, String str)
```java
StringBuffer sb = new StringBuffer("0123456");
sb.insert(4,'.');
// sb = "0123.456"
```

* int length()
* StringBuffer replace(int start, int end, String str)
    + 지정된 범위(start ~ end)의 문자들을 주어진 문자열로 바꾼다. 
```java
StringBuffer sb = new StringBuffer("0123456");
sb.replace(3,6,"AB");
// sb = "012AB6"
```

* StringBuffer reverse()
    + 문자열 뒤집기
```java
StringBuffer sb = new StringBuffer("0123456");
sb.reverse();
sb = "6543210"
```

* void setCharAt(int index, char ch)
    + 지정된 위치의 문자를 주어진 문자로 바꾼다.
```java
StringBuffer sb = new StringBuffer("0123456");
sb.setCharAt(5,'o');
// sb = "01234o6"   
```

* void setLength(int newLength);
    + 문자열 길이 변경
```java
StringBuffer sb = new StringBuffer("0123456");
sb.setLength(5);

StringBuffer sb2 = new StringBuffer("0123456");
sb2.setLength(10);
String str = sb2.toString().trim();
// sb = "01234"
// sb2 = "0123456    "
// str = "0123456"
```

* String toString()
    + StringBuffer 인스턴스의 문자열을 String으로 반환

* String substring(int start)
    + start 부터 끝까지
* String substring(int start, int end)
```java
StringBuffer sb = new StringBuffer("0123456");
String str = sb.substring(3);
String str2 = sb.subString(3,5);
// str = "3456"
// str2 = "34"
```

