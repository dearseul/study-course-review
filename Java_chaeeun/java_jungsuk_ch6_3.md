오버로딩
-----
* 한 클래스 안에 같은 이름의 메서드 여러개 정의하는 것  
* ex) void println() 
* 오버로딩이 성립하기 위한 조건
    + 메서드 이름이 같아야 한다.
    + 매개변수의 개수 또는 타입이 달라야 한다. 
    + 반환 타입은 영향 없다. 

생성자(constructor)
-----
* 인스턴스가 생성될 때마다 호출되는 '인스턴스 초기화 메서드'
```java
Time t = new Time();    // 기본 생성자 
t.hour = 12;
t.minute = 34;
t.second = 56;
// ==> 
Time t = new Time(12,34,56);    // 생성자 정의 
```
* 생성자의 이름은 클래스 이름과 같아야 한다. 
* 리턴값이 없다. (void 안붙임.)
```java
class Card{
    ...
    Card(){ // 매개변수 없는 생성자
        // 인스턴스 초기화 작업
    }
    Card(String kind, int number){  // 매개변수 있는 생성자 (생성자 오버로딩)
        // 인스턴스 초기화 작업
    }
}
```
기본 생성자(default constructor)
-----
* 매개변수 없는 생성자
* 클래스이름(){}    // 기본 생성자 
* 생성자가 하나도 없을 때만, 컴파일러가 자동 추가

매개변수가 있는 생성자
-----
```java
class Car{
    String color;
    String gearType;
    int door;

    Car(){} // 기본 생성자
    Car(String c, String g, int d){ // 매개변수 있는 생성자
        color = c;
        gearType = g;
        door = d;
    }
}

Car c = new Car("white","auto",4);
```

생성자 this()
-----
* 생성자에서 다른 생성자 호출할 때 사용 
* 다른 생성자 호출 시 첫 줄에서만 사용 가능 
```java
Class Car2{
    String color;
    String gearType;
    int door;

    Car2(){
        this("white","auto",4);
    }

    Car2(String color){
        this(color, "auto", 4);
    }

    Car2(String color, String gearType, int door){
        this.color = color;
        this.gearType = gearType;
        this.door = door;
    }
}
```

참조변수 this
-----
* 인스턴스 자신을 가리키는 참조변수 
* 인스턴스 메서드(생성자 포함)에서 사용가능.
* 지역변수(lv)와 인스턴스 변수(iv)를 구별할 때 사용 
```java
Car(String color, String gearType, int door){
    // this.color는 iv, color는 lv
    this.color = color;
    this.gearType = gearType;
    this.door = door;
}
```

변수의 초기화
-----

* 지역변수(lv)는 수동 초기화 해야함(사용 전 꼭)
```java
class InitTest{
    int x;      // 인스턴스 변수. 자동 초기화
    int y = x;  // 인스턴스 변수. 자동 초기화

    void method1(){
        int i;      // 지역변수. 수동 초기화 해야함.
        int j = i;  // 에러. 지역변수를 초기화 하지 않고 사용
    }
}
```

멤버변수(iv, cv)의 초기화
-----

1. 명시적 초기화(=) (간단 초기화)
```java
class Car{
    int door = 4;               // 기본형 변수의 초기화
    Engine e = new Engine();    // 참조형 변수의 초기화
}
```

2. 초기화 블럭 (복잡한 초기화)
    + (iv) 인스턴스 초기화 블럭 {} 
    + (cv) 클래스 초기화 블럭 static {}
```java
class StaticBlockTest{
    static int[] arr = new int[10]; // 명시적 초기화 (간단 초기화)

    static {    //  클래스 초기화 블럭 - cv 복잡 초기화 
        for(int i = 0; i < arr.length; i++){
            arr[i] = (int)(Math.random()*10) + 1;
        }
    }
}
```
3. 생성자 (iv 초기화)
```java
Car(String color){
    this.color = color;
}
```

멤버변수의 초기화
-----

* 클래스 변수 초기화 시점 : 클래스가 처음 로딩될 때 단 한번(메모리에 올라갈 때) 
* 인스턴스 변수 초기화 시점 : 인스턴스가 생성될 때마다 
* 초기화 순서 : cv -> iv , 자동 -> 간단 -> 복잡 







