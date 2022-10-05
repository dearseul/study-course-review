인터페이스의 장점
-----

* 두 대상(객체) 간의 '연결, 대화, 소통'을 돕는 '중간 역할'을 한다. 
* ex) GUI(graphic user interface) 
* 선언(설게)와 구현을 분리시킬 수 있게 한다.
```java
class B {
    public void method(){
        System.out.printlnt("methodInB");
    }
}   // => 유연하지 않고 변경이 어렵다 

// 알맹이 <-> 껍데기 분리 
// 유연하고 변경에 유리한 코드 
interface I{
    public void method();   // 선언부만 떼어내기
}

class B implements I {
    public void method(){
        System.out.println("methodInB");    // 알맹이 
    }
}
``` 

* 직접적인 관계의 두 클래스 (A-B)
```java
class A {
    public void methodA(B b){
        b.methodB();
    }
}

class B {
    public void methodB(){
        System.out.println("methodB");
    }
}

class InterfaceTest{
    public static void main(String[] args){
        A a = new A();
        a.methodA(new B());
    }
}
// B를 C로 변경하면 A도 같이 변경해야함. 
```

* 간접적인 관계의 두 클래스(A-I-B)
```java
class A {
    public void method(I i){
        i.methodB();
    }
}

interface I {
    void methodB();
}

class B implements I    {
    public void methodB(){
        System.out.prinln("methodB()");
    }
}
 
class C implements I {
    public void methodB(){
        System.out.println("methodB() in C");
    }
}
// B를 C로 변경해도 A 는 변경 없음 
```

* 개발 시간을 단축할 수 있다. 
* 변경에 유리한 유연한 설계가 가능하다. 
* 표준화가 가능하다. 
    - ex) JDBC (인터페이스 집합)
    - Java Application -> JDBC --> DB1 , DB2, ... 

* 서로 관계없는 클래스들을 관계를 맺어줄 수 있다.