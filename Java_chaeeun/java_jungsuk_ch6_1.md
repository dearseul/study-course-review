객체지향
=======
>   1. 캡슐화
>   2. 상속
>   3. 추상화
>   4. 다형성


클래스와 객체
======
* 클래스
    + 클래스란, 객체를 정의해 놓은 것
    + 클래스는 객체를 생성하는데 사용

* 객체
    + 실제로 존재하는 것. 사물 또는 개념 

* 객체의 구성요소
    + 객체 = 속성(변수) + 기능(메서드)

* 객체와 인스턴스(거의 ==)
    + 객체: 모든 인스턴스를 대표하는 일반적인 용어
    + 인스턴스: 특정 클래스로부터 생성된 객체(ex:tv인스턴스)
    ```
                  인스턴스화
    클래스 (설계도) ---------> 인스턴스(객체) (제품)
    ```
    
* 클래스가 왜 필요한가?
    + 객체를 생성하기 위해 

* 객체가 왜 필요한가?
    + 객체를 사용하기 위해 

* 객체를 사용한다는 것은?
    + 객체가 가진 속성과 기능을 사용하는 것 

객체의 생성과 사용
-----

* 객체의 생성
>   클래스 작성 
```java
Class Tv{
    String color;
    boolean power;
    int channel;

    void power(){
        power = !power;
    }
    void channelUp(){
        channel++;
    }
    void channelDown(){
        channel--;
    }
}
```
>   클래스명 변수명;            // 클래스의 객체를 참조하기 위한 참조변수 선언
>   변수명 = new 클래스명();    // 클래스의 객체를 생성 후, 객체의 주소를 참조변수에 저장

>   Tv t;
>   t = new Tv();

>   Tv t = new Tv(); 

* 객체의 사용

>   t.channel = 7;      //   Tv 인스턴스의 멤버변수 channl을 7로 한다.
>   t.channelDown();    //   Tv 인스턴스의 메서드 channelDown()을 호출한다.
>   System.out.println("현재의 채널은"+ t.channel + "입니다.");

객체 배열
-----

* 객체 배열 == 참조변수 배열 
    >   Tv[] tvArr = new Tv[3];
    >   tvArr[0] = new Tv();
    >   tvArr[1] = new Tv();
    >   tvArr[2] = new Tv();

    >   Tv[] tvArr = {new Tv(), new Tv(), new Tv()};

클래스의 정의 
-----

1. 클래스 == 설계도
2. 클래스 == 데이터 + 함수 
3. 클래스 == 사용자 정의 타입 

>   클래스 == 데이터 + 함수
>   
>   + 변수 - 하나의 데이터를 저장할 수 있는 공간
>   + 배열 - 같은 종류의 여러 데이터를 하나로 저장할 수 있는 공간
>   + 구조체 - 서로 관련된 여러 데이터(종류 관계X)를 하나로 저장할 수 있는 공간
>   + 클래스 - 데이터와 함수의 결합(구조체 + 함수)

>   클래스 == 사용자 정의 타입
>   + 원하는 타입을 직접 만들 수 있다. 


선언위치에 따른 변수의 종류 
-------

```java
class Variable{
    int iv;         // 인스턴스 변수
    static int cv;  // 클래스 변수(static변수, 공유변수)

    void method(){
        int lv = 0;     // 지역변수 
    }
}
```
>   1. 클래스 영역 - iv (인스턴스변수), cv (클래스변수 (static + iv))
>   2. 메서드 영역 - lv (지역변수)
>   >   + 생성시기
>   >    - 클래스변수 (클래스가 메모리에 올라갈 때) (객체 생성 필요X, 아무때나 사용 가능)
>   >    - 인스턴스변수 (인스턴스가 생성되었을 때)  (객체 생성해야 만들어짐)
>   >    - 지역변수 (변수 선언문이 수행되었을 때)  (메서드 종료 시 자동 제거)


클래스 변수와 인스턴스 변수
------

```java
class Card{
    // iv
    String kind;    // 무늬
    int number;     // 숫자

    // cv
    static int width = 80;   //   폭
    static int height = 120; // 높이
}
```
+ 클래스 사용
```java
Card c = new Card(); // 객체 생성
// iv 사용
c.kind = "HEART";
c.number = 5; 

// cv 사용
Card.width = 200;
Card.height = 300;

// 권장 안함 (cv)
~~c.width = 200;~~
~~c.height = 300;~~
```

메서드
-----
* 문장들을 묶어놓은 것
    - 작업단위로 문장들을 묶어서 이름 붙임. 
    - 값(입력)을 받아서 처리하고, 결과를 반환(출력)
    ```java
    int add(int x, int y){
        int result = x + y;
        return result; 
    }
    ```
    - 중복코드 제거, 관리 용이, 재사용 가능 
    - 반복적으로 수행되는 여러 문장을 메서드로 작성 
    - 하나의 메서드는 한 가지 기능만 수행하도록 작성 
    - 메서드 = 선언부 + 구현부
    ```java
    반환타입 메서드이름(타입 변수명, 타입 변수명, ...){   //(선언부)  
        // 메서드가 호출 시 수행될 코드                 (구현부)
    }
    ```
    - 지역변수(lv): 메서드 내에 선언된 변수 - x, y(매개변수), result

메서드의 호출 
-----
```java
print99danAll();        // void print99danAll()을 호출
int result = add(3,5);  // int add(int x, int y)를 호출하고, 결과를 result에 저장 
```

return 문
-----
* 실행 중인 메서드를 종료하고 호출한 곳으로 되돌아간다.
```java
void printGugudan(int dan){
    if(!(2 <= dan && dan <= 9)){
        return; // dan의 값이 2~9가 아닌 경우, 호출한 곳으로 그냥 되돌아간다. 
    }
    for(int i=1; i<=9; i++){
        // 
    }
    return;     // 반환티입이 void이므로 생략가능. 컴파일러가 자동 추가. 
}
```

* 반환타입이 void가 아닌 경우 반드시 return문 필요
```java
    int multiply(int x, int y){
        int result = x * y;
        return result;              // 타입이 일치하거나 자동형변환 가능해야 함 
    }

    ~~int max(int a, int b){~~
        ~~if(a > b)~~
            ~~return a;~~         // 조건식이 참일 때만 실행된다. => 에러 
    ~~}~~

    int max(int a, int b){
        if(a > b){
            return a;
        }else{
            return b;
        }
    }

    int add(int x, int y){
        return x + y;
    }
```


