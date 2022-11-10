날짜와 시간
-------

* java.util.Date
	+ 날짜와 시간을 다룰 목적으로 만들어진 클래스
	+ Date의 메서드는 거의 deprecated 되었지만, 여전히 쓰이고 있다. 

* java.util.Calendar
	+ Date 클래스를 개선한 새로운 클래스. 여전히 단점이 존재 (JDK1.1)

* java.time 패키지 
	+ Date와 Calendar의 단점(날짜와 시간을 같이 다룸) 을 개선한 새로운 클래스들을 제공(JDK1.8)
	+ 날짜와 시간을 따로 다룸 
	+ LocalDate, LocalTime, LocalDateTime
	
Calendar 클래스
-----

* 추상클래스이므로 getInstance()를 통해 구현도니 객체를 얻어야 한다. 
```java
Calendar cal = new Calendar();	// 에러.  추상클래스는 인스턴스를 생성할 수 없다. 

Calendar cal = Calendar.getInstance();
// OK. getInstance()메서드는 Calendar클래스를 구현한 클래스의 인스턴스를 반환한다. 

// 아래처럼 작성하면 코드가 유연하지 못함. 
Calendar cal = new GregorianCalendar();

```

* get()으로 날짜와 시간 필드 가져오기 - int get(int field)
```java
Calendar cal = Calendar.getInstance();	// 현재 날짜와 시간으로 셋팅됨.
int thisYear = cal.get(Calendar.YEAR);	// 올해가 몇년인지 알아낸다. 
int lastDayOfMonth = cal.getActualMaximum(Calendar.DATE);	// 이 달의 마지막 날 
```

* Calendar에 정의된 필드
	+ YEAR : 년
	+ MONTH : 월(0부터 시작)
	+ DATE : 일 
	+ WEEK_OF_YEAR : 그 해의 몇번째 주 
	+ WEEK_OF_MONTH : 그 달읜 몇번째 주
	+ DAY_OF_MONTH : 그 달읜 몇번째 일 
	+ DAY_OF_YEAR : 그 해의 몇번째 일 
	+ DAY_OF_WEEK 	: 요일 
	+ HOUR : 시간(0~11)
	+ HOUR_OF_DAY : 시간(0~23)
	+ MINUTE
	+ SECOND
	+ MILLISECOND
	+ ZONE_OFFSET : GMT기준 시차(천분의 일초 단위)
	+ AM_PM

