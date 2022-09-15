상속
-----

* 기존의 클래스로 새로운 클래스를 작성하는 것 (코드의 재사용)
* 두 클래스를 부모와 자식으로 관계를 맺어 주는 것 .
* class 자식클래스 extends 부모클래스 { }
* 자손은 조상의 모든 멤버를 상속받는다. (생성자, 초기화 블럭 제외)
* 자손의 멤버 개수는 조상보다 적을 수 없다. 
```java
class Parent{
    int age;
}
class Child extends Parent{}    // 멤버 1개 
```
* 자손의 변경은 조상에 영향을 미치지 않는다. 
```java
class Parent{   // 멤버 1개 
    ing age;
}
class Child extends Parent{ // 멤버 2개 
    void play(){
        System.out.println("놀자~");
    }
}
```
```java
class Point{
    int x;
    int y;
}
class Point3D { // 기존의 point와는 관계없는 클래스 
    int x;
    int y;
    int z;
}
class Point3D extends Point{    // 상속관계.
    int z;
}
```

포함 관계
-----

* 포함(composite)이란?
    + 클래스의 멤버로 참조변수를 선언하는 것
```java
class Circle{
    int x;
    int y;
    int x;
}
class Circle{
    Point c = new Point();  // Circle이 Point를 포함관계 
    int r;
}
```

* 작은 단위의 클래스를 만들고, 이 들을 조합해서 클래스를 만든다.
```java
class Car{
    Engine e = new Engine();
    Door[] d = new Door[4];
    // ... 
}
```

클래스 간의 관계 결정하기
-----
* 상속관계: '~은 ~이다.'
* 포함관계: '~은 ~를 가지고 있다.'  

