형식화 클래스
-----

* java.text 패키지의 DecimalFormat, SimpleDataFormat
* 숫자와 날짜를 원하는 형식으로 쉽게 출력 가능(숫자,날짜 -> 형식 문자열)
```java
double number = 1234567.89; // 10진수
DecimalFormat df = new DecimalFormat("#.#E0");
String result = df.format(number);  // result = "1.2E6" 
```

* 형식 문자열에서 숫자와 날짜를 뽑아내는 기능(형식 문자열 -> 숫자, 날짜)
```java
DecimalFormat df = new DecimalFormat("#,###.###");
Number num = df.parse("1,234,567.89");
double d = num.doubleValue();   // 1234567.89
```

DecimalFormat
-----

* 숫자를 형식화할 때 사용(숫자 -> 형식 문자열) 
* 특정 형식의 문자열을 숫자로 변환할 때도 사용(형식 문자열 -> 숫자)
* cf) Integer.parseInt()는 콤마(,)가 포함된 문자열을 숫자로 변환 못함 

SimpleDateFormat
-----

* 날짜와 시간을 다양한 형식으로 출력할 수 있게 해준다. 
```java
Date today = new Date();
SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd");

// 오늘 날짜를 yyyy-MM-dd 형태로 변환하여 반환한다. 
String result = df.format(today);
```

* 특정 형식으로 되어 있는 문자열에서 날짜와 시간을 뽑아낼 수도 있다.
```java
DateFormat df = new SimpleDateFormat("yyyy년 MM월 dd일");
DateFormat df2 = new SimpleDateFormat("yyyy/MM/dd");
Date d = df.parse("2015년 11월 23일");  // 문자열을 date로 변환
String result = df2.format(d);  // 날짜를 다시 문자열로 바꿈 
```

