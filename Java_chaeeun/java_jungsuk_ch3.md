연산자
========

형변환 연산자
-----
+ 형변환이란?
	변수 또는 상수의 타입을 다른 타입으로 변환하는 것 
	- (타입)피연산자

	double d = 85.4; 
	int score = (int)d;
	=> int score = 85;

+ 형변환 연산자

	int -> char : char(65) => ‘A’
	char -> int: int(‘A’) => 65
	float -> int: (int)1.6f => 1 (반올림 되지 않고 버림)
	int -> float : (float)10 => 10.0 

+ 자동 형변환

	float f = 1234; // int 타입의 값을 float 타입의 변수에 저장
	=> 자동 형변환 
	int i = 3.14f; //	에러 
	=> 자동 형변환 X 
		float 범위가 더 넓으므로 자동 현변환 X (=>값 손실 발생)
	int i = (int)3.14f; // OK 
 
	1. byte -> int 
		byte b = 10;
		int i = b; // 생략 가능 
	2. int -> byte 
		int i2 = 300;
		byte b2 = (byte)i2; //	생략불가
> 기존의 값을 최대한 보존할 수 있는 타입으로 자동 형변환 된다. 


*****
>	byte b = 100; // OK. byte 타입의 범위 (-128~127)
> 	int i = 100; 
>	byte b = i;	// 에러 
>	*위에서는 100이 리터럴이지만 여기서는 i가 변수 이므로 자동형변환X*
>	byte b = (byte)i;	//OK
>	byte = 1000; //에러 
>	byte = (byte)1000; //OK. 그러나 값손실 발생 
*****

+ 산술 변환
> 연산 전에 피연산자의 타입을 이치시키는 것
1. 두 피연산자의 타입을 같게 일치시킨다.(보다 큰 타입으로 일치) 
2. 피연산자의 타입이 int보다 작은 타입이면 int로 변환된다. 
		
	byte + short -> int + int -> int 
	char + short -> int + int -> int 
	‘2’-‘o’ -> 50 - 48 -> 2

+ 반올림 - Math.round()
	
	long result = Math.round(4.52); //	result에 5가 저장된다.
	double pi = 3.141592;
	Math.round(pi * 1000)/ 1000.0 // 3142/1000 -> 3
	Math.round(3141.592)/ 1000.0 // 3142/1000.0 -> 3.142

> double pi = 3.141592; // 3.141로 바꾸려면? 
	
	int(pi*1000)	// 형변환 -> 날라감 => 3141
	3141/1000.0 // 3.141

+ 나머지 연산자 %
> 오른쪽 피연산자로 나누고 남은 나머지를 반환
> 정수만 허용, 부호는 무시됨 

+ 문자열의 비교 
> 문자열 비교에는 == 대신 equals()를 사용해야 한다. 

	String str1 = “abc”;
	String str2 = “abc”;
	System.out.println(str1==str2); 	//true
	System.out.println(str1.equals(str2)); //true

	String str1 = new String(“abc”);
	String str2 = new String(“abc”);
	System.out.println(str1==str2);	// false
	Ssytem.out.println(str2.equals(str2)); // true

+ 논리 연산자 
> && || 
- 문자 ch는 숫자(‘0’~’9’)이다.
	사용자로부터 입력된 문자가 숫자 (‘0’~’9’)인지 확인하는 식
	
	‘0’ <= ch && ch <= ‘9’

- 문자 ch는 대문자 또는 소문자이다. 
	
	(‘a’ <= ch && ch <= ‘z’) || ( ‘A’ <= ch && ch <=‘Z’)

+ 조건 연산자 ?: 
> result = (x>y) ? x : y; 
  
	
	