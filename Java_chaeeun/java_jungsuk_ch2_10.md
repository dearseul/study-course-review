변수(variable)
========

Java 프로그램 만들기
-----------
+ javac.exe - w자바컴파일러. 사람이 작성한 문장을 기계어로 번역
소스파일(*.java)을 클래스파일(*.class) 로 변환

+ java.exe - 자바 인터프리터. 자바프로그램(클래스 파일)을 실행
+ 클래스 - 자바 프로그램 단위. 자바 프로그램은 클래스들로구성 
+ main 메서드 - 자바 프로그램의 시작점. 이 메서드 없이 실행 불가 
	class className{
		public static void main(String[] args){
			/* 문장 */ 
		}
	}

변수란(variable)란?
————
+ 하나의 값을 저장할 수 있는 메모리 공간! 
	
변수의 선언
———
+ 변수의 선언 이유
	* 값(data)을 저장할 공간을 마련하기 위해서
+ 변수의 선언 방법
	변수 타입 변수이름; 
	int age;	// 정수(int)타입의 변수 age를 선언 
	=> age라는 이름의 저장공간이 마련된다. 

변수에 값 저장하기 
———
+ 변수에 값 저장하기
	int age; 
	age = 25; 

변수의 타입
———-
+ 변수의 타입은 저장할 값의 타입에 의해 결정된다. 
+ 저장할 값의 타입과 일치하는 타입으로 변수를 선언 

값의 타입
———
+ 문자
	- char 
+ 숫자 
	- 정수 - byte, short, int, long
	- 실수	- float, double
+ 논리 - boolean 

변수, 상수, 리터럴
————
+ 변수(variable) - 하나의 값을 저장하기 위한 공간 (변경 o)
+ 상수(constant) - 한 번만 값을 젖아 가능한 변수 ( 변경 x)
	final int MAX = 100; // MAX는 상수 
+ 리터럴(literal) - 그 자체로 값을 의미하는 것 
	- = 기존의 상수 
	
리터럴의 접두사와 접미사
————
+ 정수형 int (123,OB0101(접두사OB -> 이진수) ,077) 
+ 정수형 + 접미사 L => long 
	long l = 10_000_000_000L; (L : 생략불가) 
	long l = 100; ( 리털러 Int -> 허용) 
+ 실수형 + 접미사d(double->생략가능) / 접미사f(float) 
+ 문자형 (‘A’) 
+ 문자열 (“a”) 


변수와 리터럴의 타입 불일치 
———
+ 범위가 변수 > 리터럴 인 경우 OK 
	int i =‘A’  // int > char (O)
	long l = 123; (O)
	double d.  3.14f; // double> float (O)

+ 범위가 변수 < 리터럴인 경우 에러 
	int I = 30_0000_0000; // int 범위(+-20억) 벗어남 
	long l = 3.14f;  // long < float
	float f = 3.14;  // float < double 
+ byte, short 변수에 int 리터럴 저장 가능 
	byte b = 100; // OK -127~128
	byte b = 128; // 에러 . 


문자와 문자열 
———
char ch = ‘A’;
char ch = ‘AB’; //에러 
String s = “ABC” // 문자열 
	String s1 = “AB”;
	String s2 = new String(“AB”); 
String s = “”; // 빈 문자열
Char ch = ‘’/ 에러 


*****
*****

기본형과 참조형 
—————
+ 값의 타입
	- 기본형 
		문자 - char 
		숫자 - 정수 - byte, short, int ,long
			실수 - float, double
		논리 - boolean

	

+ 기본형과 참조형
	- 기본형(primitive type)
		* 오직 8개
		* 실제 값을 저장 
	- 참조형(reference type)
		* 기본형을 제외한 나머지(String, System 등) 
		* 메모리 주소를 저장(4byte 또는 8byte)
	Date today;  	//참조형 변수 today
	today = new Date(); //객체 생성, today에 객체의 주소를 저장 


기본형의 종류와 크기
————
+ 논리형 - boolean (true/false)
+ 문자형 - char (하나의 문자만 저장가능)
+ 정수형 - byte, short, int, long 
+ 실수형 - 실수 값을 저장하는데 사용된다. 
(단위: Byte) 	cf)1bit = 2진수 1자리 ( 1byte = 8bit)
논리형 boolean 1byte 
문자형 		     char 2byte ( 유니코드 2byte) 
정수형 byte(1byte)  short(2byte) int(4byte) long(8byte)		default type : int
실수형				     float(4byte) double(8byte)	default type: double


기본형의 표현 범위 
———
* byte b; 
 1 byte = 1bit(2진수) * 8 
B = 3; => 00000011 (1byte)
	n bit 로 표현할 수 있는 값의 개수: 2의 n제곱
	n bit 로 표현할 수 있는 부호 없는 정수의 범위: 0 ~ 2n - 1(0을 범위에 포함)  => 8bit => 0 ~ 255
	n bit로 표현할 수 있는 부호있는 정수의 범위 : -2(n-1) ~ 2(n-1) - 1 => 8bit => -128~ 127 ( 1byte) 

* 1byte 
    - 전체 8비트 중 맨 앞 1비트 => 부호비트(sign bit) 0:양수 / 1: 음수

* short 2byte = 16bit => -2의15 ~ 2의15-1 (-32768~32767)
* char 2byte => 0 ~ 2의 16(0~65535)  (char는 양수만 표현하면 되므로 short와 범위가 다름) 

* int 4byte = 32bit ( -2의31~ 2의31-1)  ( -20억~20억) 
* long 8byte - 64bit(-2의 63 ~ 2의63 -1) ( -800경 ~ 800경) (cf) > 800 : BigInteger (class)) 

* float 4byte (1.4E ~ 3.4E38)/ 정밀도(몇자리까지 오차없이 표현가능): 7자리 
	- float는 int와 같은 4byte이지만 훨씬 많은수 저장 가능 
	- s(부호), e(지수)(8), m(가수)(23) => 형식으로 저장하기 때문 
	- 3.4(가수)e38(지수) 
* double 8byte : 정밀도15자리 
	-s, e(11), m(52) 

printf()
-------
+ println()출력의 단점 
    - 실수의 자리수 조절 불가
    - 10진수로만 출력된다. 
+ printf()로 출력형식 지정 가능 
    - System.out.printf("%.2f",10.0/3);     // 3.33
    - System.out.printf("%d",0x1A);         // 26 

+ 지시자
    - %b (boolean)
    - %d (10진) 정수
    - %o (8진) 정수
    - %x, %X(16진) 정수 
    - %f 부동 소수점 형식으롳 출력
    - %e, %E 지수 표현식으로 출력
    - %g : %f, %e 중 간략한 형식
    - %c 문자
    - %s 문자열
    System.out.printf("age:%d year:%d\n",14,2017);
    - 8진수, 16진수에 접두사 붙이려면 지시자앞에 # 붙이면 됨 "(%#o")
    - 지시자 앞에 숫자를 붙이면 출력할 자릿수 지정 가능 
        - 앞에 - : 왼쪽 정렬
        - 앞에 0 : 0으로 채움 
        - %5d, 1234567 => 1234567
        - %.5s, "www.codechobo.com" => www.c

화면에서 입력받기 - Scanner
-----
+ Scanner
    - 화면으로부터 데이터를 입력받는 기능을 제공하는 클래스
1. import문 추가 
    import java.util.*
2. Scanner 객체 생성 
    Scanner scanner = new Scanner(System.in);
3. Scanner 객체를 사용
    int num = scanner.nextInt(); //  화면에서 입력받은 정수를 num에 저장 
    String input = Scanner.nextLine(); //한 행 
    int num = Integer.parseInt(input)   // 문자열을 숫자로 변환 


정수형의 overflow
---------
+ 최댓값 + 1 => 최솟값
+ 최솟값 - 1 => 최댓값
