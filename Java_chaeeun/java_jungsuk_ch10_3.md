Calendar 
-----

* add() 는 특정 필드의 값을 증가 또는 감소(다른 필드에 영향O)
```java
Calendar date = Calendar.getInstnace();
date.clear();
date.set(2020,7,31);

date.add(Calendar.DATE,1);  // 날짜에 1 을 더한다. 9월 1일 
date.add(Calendar.MONTH,-8);    // 월에 8을 뺀다. 1월 1일 
```

* roll()은 특정 필드의 값을 증가 또는 감소(다른 필드에 영향X)
```java
date.set(2020,7,31);

date.roll(Calendar.DATE,1); // 날짜에 1을 더한다. 8월 1일 (다른필드 영향X)
date.roll(Calendar.MONTH,-8);   // 2020년 12월 31일 
```

Date와 Calendar간의 변환
-----

* Date의 메서드는 대부분 Deprecated 되었지만 여전히 사용 
    1. Calendar를 Date로 변환
    ```java
    Calendar cal = Calendar.getInstance();
    ...
    date d = new Date(cal.getTimeInMillis();    // Date(long date)
    ```
    2. Date를 Calendar로 변환 
    ```java
    Date d = new Date();
    ...
    Calendar cal = Calendar.getIntance();
    cal.setTime(d);
    ```
    