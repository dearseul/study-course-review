Calendar 클래스
-----

* set()으로 날짜와 시간 지정하기
```java
void set(int field, int value)
void set(int year, int month, int date) // 연월일
void set(int year, int month, int date, int hourOfDay, int minute)
void set(int year, int month, int date, int hourOfDay, int second)
```
* 날짜 지정하는 방법.
	+ 월(Month)이 0부터 시작한다는 점에 주의 
```java
Calendar date1 = Calendar.getInstance();
date1.set(2017,7,15);	// 2017년 8월 15일 
// date1.set(Calendar.YEAR,2017)
// date1.set(Calendar.MONTH,7)
// date1.set(Calendar.DATE, 15);
```

* 시간 지정하는 방법
```java
Calendar time1 = Calendar.getInstnace();
time1.set(Calendar.HOUR_OF_DAY,10);
time1.set(Calendar.MINUTE,20);
time1.set(Calendar.SECOND,30);
```

```java
class Ex10_1{
	public static void main(String[] args){
		final String[] DAY_OF_WEEK = {“”,”일”,”월”,”화”,”수”,”목”,”금”,”토”}
		
		Calendar date1 = Calendar.getInstance();
		Calendar date2 = Calendar.getInstance();

		date1.set(2019,3,25);	// 2019년 4월 25일
		System.out.println(“(date1)은 “ + toString(date1) + DAY_OF_WEEK[date1.get(Calendar.DAT_OF_WEEK)]	+ “ 요일 이고, “)
		System.out.println(“오늘(date2)은 “ + toString(date2) + DAY_OF_WEEK[date1.get(Calendar.DAT_OF_WEEK)]	+ “ 요일 이고, “)

	// 두 날짜간의 차이를 얻으려면, getTImeInMillis() 천분의 일초 단위로 변환해야 한다. 
	long difference = (date2.getTimeInMillis() - date1.getTimeInMillis())/1000;
	
	System.out.println(“그 날 (date1) 부터 지금(date2) 까지 + difference  + “ 초가 남았습니다.”);
	System.out.println(“일(day)로 계산하면 “ + difference/(24*60*60)	+ “ 일 입니다.”);
	}
}
```

```java
	final int[] TIME_UNIT = {3600, 60, 1);
	final String[] TIME_UNIT_NAME = {“시간”,”분”,”초”};

	time1.set(Calendar.HOUR_OF_DAY, 10);
	time1.set(Calendar.MINUTE, 20);
	time1.set(Calendar.SECOND, 30);

	time2.set(Calendar.HOUR_OF_DAY, 20);
	time2.set(Calendar.MINUTE, 30);
	time2.set(Calendar.SECOND, 10);

	long difference = 
	Math.abs(time2.getTimeInMilis() - time1.getTimeInMillis())/1000;

	String tmp = “”;
	for(int i = 0; i < TIME_UNIT.length; i++){
		tmp += difference/TIME_UNIT[i] + TIME_UNIT_NAME[i];
		difference %= TIME_UNIT[i];
	}
	System.out.println(“시분초로변환하면  “ + tmp + “ 입니다.”);
```

* clear()는 Calendar 객채의 모든 필드를 초기화
```java
Calendar dt = Calendar.getInstance();

// Tue Aug 29 07:13:03 kst 2017
System.out.println(new Date(dt.getTimeInMillis()));

dt.clear();	// 초기화 
// Thu Jan 01 00:00:00 KST 1970 (EPOCH TIME = 1970년 1월 1일 00:00:00)
System.out.println(new Date(dt.getTimeInMillis()));
```

* clear(int field)는 Calendar 객체의 특정 필드를 초기화
```java
 
Calendar dt = Calendar.getInstance();

dt.clear(Calendar.SECOND);
dt.clear(Calendar.HOUR);
dt.clear(Calendar.HOUR_OF_DAY);
dt.clear(Calendar.MINUTE);
```
* clear() 안햇을 시 문제

```java 
Calendar date1 = Calendar.getInstance();
Calendar date2 = Calendar.getIntance();

 // date1 과 date2 의 밀리세컨드 차이가 발생함 
date1.set(year1,month1,day1);
date1.set(year2,month2,day2);
// 1.99999
System.out.println(date1.getTimeInMillis() - date2.getTimeInMillis());

// 1 
diff = (int)((date1.getTimeInMillis() - date2.getTimeInMillist()));
```


Calendar 클래스
-----

* set()으로 날짜와 시간 지정하기
```java
void set(int field, int value);
void set(int year, int month, int date); // 연월일
void set(int year, int month, int date, int hourOfDay, int minute);
void set(int year, int month, int date, int hourOfDay, int second);
```
* 날짜 지정하는 방법.
	+ 월(Month)이 0부터 시작한다는 점에 주의 
```java
Calendar date1 = Calendar.getInstance();
date1.set(2017,7,15);	// 2017년 8월 15일 
// date1.set(Calendar.YEAR,2017)
// date1.set(Calendar.MONTH,7)
// date1.set(Calendar.DATE, 15);
```

* 시간 지정하는 방법
```java
Calendar time1 = Calendar.getInstnace();
time1.set(Calendar.HOUR_OF_DAY,10);
time1.set(Calendar.MINUTE,20);
time1.set(Calendar.SECOND,30);
```

```java
class Ex10_1{
	public static void main(String[] args){
		final String[] DAY_OF_WEEK = {“”,”일”,”월”,”화”,”수”,”목”,”금”,”토”}
		
		Calendar date1 = Calendar.getInstance();
		Calendar date2 = Calendar.getInstance();

		date1.set(2019,3,25);	// 2019년 4월 25일
		System.out.println(“(date1)은 “ + toString(date1) + DAY_OF_WEEK[date1.get(Calendar.DAT_OF_WEEK)]	+ “ 요일 이고, “)
		System.out.println(“오늘(date2)은 “ + toString(date2) + DAY_OF_WEEK[date1.get(Calendar.DAT_OF_WEEK)]	+ “ 요일 이고, “)

	// 두 날짜간의 차이를 얻으려면, getTImeInMillis() 천분의 일초 단위로 변환해야 한다. 
	long difference = (date2.getTimeInMillis() - date1.getTimeInMillis())/1000;
	
	System.out.println(“그 날 (date1) 부터 지금(date2) 까지 + difference  + “ 초가 남았습니다.”);
	System.out.println(“일(day)로 계산하면 “ + difference/(24*60*60)	+ “ 일 입니다.”);
	}
}
```


* clear()는 Calendar 객채의 모든 필드를 초기화
```java
Calendar dt = Calendar.getInstance();

// Tue Aug 29 07:13:03 kst 2017
System.out.println(new Date(dt.getTimeInMillis()));

dt.clear();	// 초기화 
// Thu Jan 01 00:00:00 KST 1970 (EPOCH TIME = 1970년 1월 1일 00:00:00)
System.out.println(new Date(dt.getTimeInMillis()));
```


* clear()는 Calendar 객채의 모든 필드를 초기화
```java
Calendar dt = Calendar.getInstance();

// Tue Aug 29 07:13:03 kst 2017
System.out.println(new Date(dt.getTimeInMillis()));

dt.clear();	// 초기화 
// Thu Jan 01 00:00:00 KST 1970 (EPOCH TIME = 1970년 1월 1일 00:00:00)
System.out.println(new Date(dt.getTimeInMillis()));
```


* clear() 안햇을 시 문제

```java 
Calendar date1 = Calendar.getInstance();
Calendar date2 = Calendar.getIntance();

 // date1 과 date2 의 밀리세컨드 차이가 발생함 
date1.set(year1,month1,day1)
date1.set(year2,month2,day2)
// 1.99999
System.out.println(date1.getTimeInMillis() - date2.getTimeInMillis());

// 1 
diff = (int)((date1.getTimeInMillis() - date2.getTimeInMillist()));
```