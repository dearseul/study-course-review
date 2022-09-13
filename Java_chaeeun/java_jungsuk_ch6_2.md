호출 스택
=======

* 스택(stack) : 밑이 막힌 상자. 위에 차곡차곡 쌓인다. 
* 메서드 수행에 필요한 메모리가 제공되는 공간
* 메서드가 호출되면 호출스택에 메모리 할당, 종료되면 해제 

기본형 매개변수
=======

* 기본형 매개변수 - 변수의 값을 읽기만 할 수 있다.(read only)
* 참조형 매개변수 - 변수의 값을 읽고 변경할 수 있다.(read & write)

```java
class Ex6_1{
    public static void main(String[] args){
        Data d = new Date();
        d.x = 10;
        System.out.println("main(): x = " + d.x);

        change(d.x);
        System.out.println("After change(d.x)");
        System.out.println("main(): x = " + d.x);

    }

    static void change(int x){
        x = 10000;
        System.out.println("change() : x = " + x);
    }
}
```
* 결과
```
main() : x = 10
change() : x = 10000
AFter change(d.x)
main() : x = 10
```

참조형 매개변수
=====

```java
class Ex6_2{
    public static void main(String[] args){
        Data2 d = new Data2();
        d.x = 10;
        System.out.println("main() : x = " + d.x);

        change(d);
        System.out.println("After change(d)");
        System.out.println("main(): x = " + d.x);
    }

    static void change(Data2 d){
        d.x = 1000; 
        System.out.println("change(): x = " + d.x);
    }
}
```

* 결과
```
main() : x = 10
change() : x = 1000
After change(d)
main() : x = 1000
```

참조형 반환타입
=====

```java
class Ex6_3{
    public static void main(String[] args){
        Data3 d = new Data3();
        d.x = 10;

        Data3 d2 = copy(d);
        System.out.println("d.x = " + d.x);
        System.out.println("d2.x = " + d2.x);
    }

    static Data3 copy(Data3 d){
        Data3 tmp = new Data3();    // 새로운 객체 tmp를 생성한다.
        tmp.x = d.x;        // d.x의 값을 tmp.x에 복사한다. 

        return tmp;         // 복사한 객체의 주소를 반환한다.
    }
}
```
* 결과
```
d.x = 10
d2.x = 10
```

static 메서드와  인스턴스 메서드 
========

* 인스턴스 메서드
    + 인스턴스 생성 후, '참조변수.메서드()'이름으로 호출
    + 인스턴스 멤버(iv,im)와 관련된 작업을 하는 메서드
    + 메서드 내에서 인스턴스 변수(iv) 사용가능

* static 메서드(클래스 메서드)
    + 객체 생성 없이 '클래스이름.메서드이름()' 으로 호출
    + 인스턴스 멤버(iv,im)와 관련없는 작업을 하는 메서드
    + 메서드 내에서 인스턴스 변수(iv) 사용 불가 


```java
class MyMath2{
    long a, b;

    long add(){ // 인스턴스 메서드
        return a + b;
    }

    static long add(long a, long b){    // 클래스메서드(static 메서드)
        return a + b;
    }
}
class MyMathTest2{
    public static void main(String[] args){
        System.out.println(MyMath2.add(200L, 100L));    // 클래스 메서드 호출
        MyMath2 mm = new MyMath2();     // 인스턴스 생성 
        mm.a = 200L;
        mm.b = 100L;
        System.out.println(mm.add());   // 인스턴스메서드 호출 
    }
}
```
>   * static을 언제 붙여야 할까? 
>       + 속성(멤버변수) 중에서 공통 속성에 static을 붙인다.
>       + 인스턴스 멤버(iv,im)을 사용하지 않는 메서드에 static을 붙인다. 

메서드 간의 호출과 참조
=======

* static 메서드는 인스턴스 변수(iv)를 사용할 수 없다. 
```java
class TestClass2{
    int iv; // 인스턴스 변수 . 객체 생성 후 사용 가능.
    static int cv;  // 클래스 변수. 언제나 사용 가능.

    void intanceMethod(){       // 인스턴스 메서드
        System.out.println(iv); 
        System.out.println(cv);
    }

    static void statcMethod(){     // static 메서드
        System.out.println(iv); // 에러!! 인스턴스 변수를 사용할 수 없다.
        System.out.println(cv); // 클래스 변수는 사용할 수 있다.
    }
}
```
* static 메서드는 인스턴스 메서드(im)를 호출할 수 없다.
```java
class TestClass{
    void intanceMethod(){}
    static void staticMethod(){}

    static void staticMethod2(){
        instanceMethod();   // 에러!! 인스턴스 메서드를 호출할 수 없다.
        staticMethod();     // static메서드는 호출할 수 있다.
    }
}
```


