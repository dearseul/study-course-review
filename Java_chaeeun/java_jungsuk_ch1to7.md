자바의 정석 ch1-7
=====================

자바의 특징
---------------------

+ 배우기 쉬운 객체지향 언어
+ 자동 메모리 관리
	- garbage collector
+ 멀티쓰레드 (하나의 프로그램에서 동시에 여러 작업 가능)
+ 풍부한 라이브러리
+ 운영체제에 독립적
	- 자바 가상 머신(JVM) 위에서 실행되기 때문에 OS 상관없이 실행 가능 

자바의 설치 및 실행 (for mac) 
-----------------------

+ SDKMAN 설치
	- 자바 버전 별로 설치 및 자동 환경변수 설정 가능 
	```
	$ curl -s "https://get.sdkman.io" | bash 
	$ source "$HOME/.sdkman/bin/sdkman-init.sh"
	$ sdk version 		// sdk 버전 출력
	$ sdk list java		// 설치가능한 java 버전 출력
	$ sdk install java 8.0.292-zulu // 지정 버전 설치
	$ sdk use java 8.0.292-zulu 	// 사용할 java버전을 변경(현재 쉘에만 적용)  
 	$ sdk current java 	// 현재 사용중인 java버전 출력  
 	$ echo $JAVA_HOME	// JAVA_HOME으로 지정된 경로 출력
	```

+ Java API 문서 설치 
	- java API란? 
		* java로 프로그램을 만드는데 필요한 주요 기능을 미리 만들어서 제공 
	- java API 문서란?
		* java API가 제공하는 기능에 대한 상세한 정보 제공 
	- java API 문서의 설치 
		* [Oracle][https://www.oracle.com]

+ Java 파일 실행하기
	1. 텍스트 편집기에서 Java파일 생성 (Hello.java)
	```java
	public static class Hello{
		public static void main(String[] args){
			System.out.println(“Hello World!”);
		}
	}
	```
	2. 터미널에서 java 파일 컴파일
	```
	$ cd [경로]
	$ javac Hello.java. // 컴파일 
	```
	3. java 파일 실행
	```
	$ java Hello 	// Hello World! 가 출력되는 것을 볼 수 있다.
	```