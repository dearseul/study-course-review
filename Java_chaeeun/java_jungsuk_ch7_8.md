디폴트 메서드와 static 메서드
-----

##### 인터페이스에 디폴트 메서드, static 메서드 추가 기능(JDK1.8부터)
* 인터페이스에 새로운 메서드(추상 메서드)를 추가하기 어려움. 
    -   새로운 메서드 (추상 메서드)를 추가 하면  interface를 구현한 모든 class가 새로운 메서드를 구현해야 함. 
    - 해결책 => defualt method
    - default method는 인스턴스 메서드(인터페이스 원칙 위반) 
    ```java
    interface MyInterface {
        void method();
        default void newMethod(){}  // default   
    }
    ```
    - default 메서드가 기존의 메서드와 충돌할 떄의 해결책 
        1. 여러 인터페이스의 디폴트 메서드 간의 충돌 
            - 인터페이스를 구현한 클래스에서 디폴트 메서드를 오버라이딩 해야 한다.
        2. 디폴트 메서드와 조상 클래스의 메서드 간의 충돌 
            - 조상 클래스의 메서드가 상속되고, 디폴트 메서드는 무시된다. 
    - => 걍 오버라이딩 하면 해결. 

내부 클래스(inner class)
-----

###### 클래스 안의 클래스 
```java
class A {       // 외부 클래스 
    // ...      
    class B {   // 내부 클래스
        // ... 
    }
}
```
###### 내부 클래스의 장점 
* 내부 클래스에서 외부 클래스의 멤버들을 쉽게 접근할 수 있다. 
* 코드의 복잡성을 줄일 수 있다.(캡슐화) 

```java
class A {
    int i = 100;
    B b = new B();
}
class B {
    void method(){
        A a = new A();
        System.out.println(a.i);
    }

}
class C {
    B b = new B();
}

public class InnerTest{
    public static void main(String[] args){
        B b = new B();
        b.method();
    }
}

// --> 내부 클래스 
class A { 
    int i = 100;
    class B {   // B는 A의 내부 클래스 
        void method(){
            // A a = new A();
            System.out.println(i);  // 객체 생성 없이 외부 클래스의 멤버 접근 가능 
        }
    }
}
class C {
    // B b = new B();   // ERROR 

}
public class InnerTest{
    public static void main(String[] args){
        // B b = new B(); // ERROR 
        // b.method();
    }
}
```

내부 클래스의 종류와 특징 
-----

* 내부 클래스의 종류와 유효범위(scope)은 변수와 동일 
```java
class Outer{
    class InstanceInner{}           // 1. 인스턴스 클래스 ( = iv ) 
    static class StaticInner{}      // 2. static 클래스 ( = cv )

    void myMethod(){
        class LocalInner{}          // 3. 지역 클래스 ( = lv )  
    }
}
// 4. 익명 클래스 - 클래스의 선언과 객체의 생성을 동시에 하는 이름없는 클래스(일회용)
```


내부 클래스의 제어자와 접근성 
-----

* 내부 클래스의 제어자는 변수에 사용 가능한 제어자와 동일 
* (원래 class 앞에는 default, public 만 가능)
```java
class Outer {
    private class InstanceInner{}
    protected static class StaticInner {}

    void myMethod(){
        class LocalInner{}
    }
}
```
```java 
class Outer {
    class InstanceInner {
        int iv = 100;
        static int cv = 100;    // ERROR !!! 
        // 인스턴스 class이므로 static 변수를 선언할 수 없다. 
        final static int CONST = 100; // final static은 상수이므로 허용
    }

    static class StaticInner {
        int iv = 200;
        static int cv = 200;        // static 클래스만 static 멤버를 정의할 수 있다. 
        // static 내부 클래스 에서는 외부 클래스의 인스턴스 멤버에 접근할 수 없다. 
    }
    void myMethod(){
        class LocalInner {
            int iv = 300;
            static int cv = 300;        // ERROR!! static 변수 선언 불가 
            final static int CONST = 300; // final static은 상수이므로 허용
        }
        // 지역 내부 클래스의 static 상수는 method 내에서만 사용 가능 
        int i = LocalInner.CONST;    // OK
    }
}
public static void main(String[] args){
    System.out.println(InstanceInner.CONST);
    System.out.println(StaticInner.cv);
    // System.out.println(LocalInner.CONST);    // ERROR
}
```

``` java
class Ex7_1{
    class InstanceInner{}
    static class StaticInner{}

    InstanceInner iv = new InstanceInner(); // OK. 인스턴스 멤버끼리는 직접 접근 가능
    static StaticInner cv = new StaticInner();  // OK. static 멤버끼리는 직접 접근 가능
    // static StaticInner cv = new InstanceInner(); // ERROR
    static void staticMethod(){
        // static 멤버는 인스턴스멤버에 접근 불가
        // IntanceInner obj1 = new InstanceInner();    //ERROR
        StaticInner obj2 = new StaticInner();

        Ex7_1 outer = new Ex7_1(); //    인스턴스클래스는 외부클래스를 먼저 생성해야 생성가능 
        InstanceInner obj1 = outer.new InstanceInner();
    }
    void instanceMethod(){  // 인스턴스 메서드에서는 인스턴스 멤버와 static 멤버 모두 접근 가능
        InstanceInner obj1 = new InstanceInner();
        StaticInner obj2 = new StaticInner();
    }

    void myMethod(){
        class LocalInner{}
        LocalInner lv = new LocalInner();
    }
}
```

```java
class Outer2 { 
    private int outerIv = 0; 
    static int outerCv = 0;

    class InstanceInner {
        int iiv = outerIv;      // 외부 클래스의 private멤버도 접근 가능 
        int iiv2 = outerCv;
    }
    
    static class StaticInner {
        // int siv  = outerIv; // ERROR. static 클래스는 외부클래스의 인스턴스멤버에 접근 불가
        static int scv = outerCv;
    }

    void myMethod(){
        int lv = 0;     // 변수
        final int LV = 0;   // 상수 

        class LocalInner { 
            int liv = outerIv;
            int liv2 = outerCv; // JDK1.8 부터 final 생략 가능 .. 
                                // lv 의 값이 바뀐 적이 없으면 상수로 침 .. 

            int liv3 = lv;  // ERROR. 지역변수 접근 X (JDK1.8 부터 lv가 바뀐적이 없으면 상수로 취급해서 에러아님)
            // method 지역변수는 method종료와 함게 소멸 
            // 내부클래스 객체가 method의 지역변수보다 오래 존재 가능 

            int liv4 = LV; // OK. 상수는 OK 
        }
    }
}
```
```java
class Ex7_2{
    public static void main(String[] args){
        Outer2 oc = new Outer2();   // 왜부클래스의 인스턴스를 먼저 생성해야 
        Outer2.InstanceInner ii = oc.new IntaceInner(); // 인스턴스 클래스의 인스턴스를 생성 가능
        
        // static 내부 클래스의 인스턴스는 외부클래스를 먼저 생성하지 않아도 된다.
        Outer2.StaticInner si = new Outer2.StaticInner();
                                // 외부클래스이름.static class명 
        System.out.println("si.iv : " + si.iv);
    }
}
```

> cf) 
> 예제를 컴파일하면 class 다섯개 만들어짐 
> Ex7_1.class
> Outer2.class
> Outer2$InstanceInner.class   (내부 클래스 앞에 $ 붙음)
> Outer2$StaticInner.class 
> Outer2$1LocalInner.class (지역 내부클래스는 $숫자 붙음)

```java
class Outer3{
    int value = 10;     // Outer3.this.value (외부클래스의 iv)

    class Inner { 
        int value = 20; // this.value (내부클래스의 iv)

        void method1(){
            int value = 30;     // lv
            System.out.println("            value: " + value);
            System.out.println("       this.value: " + this.value);
            System.out.println("Outer3.this.value: " + Outer3.this.value);
        }
    }
}
class Ex7_4{
    public static void main(String[] args){
        Outer3 outer = new Outer3();
        Outer3.Inner inner = outer.new Inner();
        inner.method1();
    }
}
```

익명클래스 (anonymous class)
-----

#### 이름이 없는 일회용 클래스. 정의와 생성을 동시에.
```java
new 조상클래스이름(){
    // 멤버선언
}
new 구현인터페이스이름(){
    // 멤버 선언
}
```
```java
class Ex7_5{
                // 조상클래스이름
    Object iv = new Object(){   // 익명클래스
        void mtehod(){}
    }
    static Object cv = new Object(){   void method(){}  }; //익명클래스 

    void myMethod(){
        Object lv = new Object(){ void method(){} };    // 익명 클래스 
    }
}
```

```java
// AWT (Java의 윈도우 프로그래밍)
class Ex7_6{
    public static void main(String[] args){
        Button b = new Button("Start");
        b.addActionListener(new EventHandler());
    }
}
class EventHandler implements ActionListener{   // => 일회성 
    public void actionPerformed(ActionEvent e){
        System.println("ACtionEvent ocurred!!");  
    }
}

// -> 익명 클래스로 만듬 
b.addActionListner(new ActionListner(){ // 조상 또는 interface 이름 (익명클래스)
    public void actionPerformed(ActionEvent e){
        System.println("ACtionEvent ocurred!!");  
    }

});
```
