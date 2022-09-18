단일상속
-----

* java는 단일 상속만을 허용한다. 
* 비중이 높은 클래스 하나만 상속관계로, 나머지는 포함관계로 한다. 

Object 클래스 - 모든 클래스의 조상 
-----

* 부모가 없는 클래스는 자동적으로 Object클래스를 상속받게 된다. 
* 모든 클래스는 Object클래스에 정의된 11개의 메서드를 상속받는다. 
    + toString(), equals(Object obj), hashCode(), ... 


오버라이딩
-----

* 상속받은 조상의 메서드를 자신에게 맞게 변경하는 것 
```java
class Point{
    int x;
    int y;

    String getLocation(){
        return "x; " + x;
    }
}
class Point3D extends Point{
    int z;
    
    String getLocation(){   // 오버라이딩
        return "x: " + x + ", z : " + z;
    }
}
```
* 오버라이딩의 조건
    + 선언부가 조상 클래스의 메서드와 일치해야 한다. 
    + 접근 제어자를 조상클래스의 메서드보다 좁은 범위로 변경할 수 없다. 
    + 예외는 조상클래스의 메서드보다 많이 선언할 수 없다. 

참조변수 super
-----

* 객체 자신을 가리키는 참조변수. 인스턴스 메서드(생성자) 내에만 존재. static 메서드에서 사용 불가.
* 조상의 멤버를 자신의 멤버와 구별할 때 사용 
* this(lv, iv 구별할 때 사용)
```java
class Ex7_1{
    public static viod main(String[] args){
        Child c = new Child();
        c.method();
    }
}
class Parent{   int x = 10;     } // super
class Child extends Parent{
    int x = 20;
    void method(){
        System.out.println("x=" + x);
        System.out.println("this.x=" + this.x);
        System.out.println("super.x=" + super.x);
    }
}
```
```
// 결과
x = 20
x = 20
x = 10
```

```java
class Ex7_2{
    public static void main(String[] args){
        Child2 c = new Child2();
        c.method();
    }
}
class Parent2{  int x = 10; }   // super.x this.x 둘다 가능 
class Child2 extends Parent2{
    void method(){
        System.out.println("x=" + x);
        System.out.println("this.x=" + this.x);
        System.out.println("super.x=" + super.x);

    }
}
```
```
// 결과
x = 10
x = 10
x = 10
```

super() - 조상의 생성자
-----

* 조상의 생성자를 호출할 때 사용 
* 조상의 멤버는 조상의 생성자를 호출해서 초기화 

```java
class Point{
    int x, y;
    Point(int x , int y){
        this.x = x;
        this.y = y;
    }
}
class Point3D extends Point{
    int z;
    Point3D(int x , int y, int x){
        super(x,y); // 조상클래스의 생성자 Point(int x, int y)를 호출
        this.z = z; // 자신의 멤버를 초기화 
    }
}
```

>   * 생성자의 첫 줄에 반드시 생성자를 호출해아 한다. 
>   * 그렇지 않으면 컴파일러가 생성자의 첫 줄에 super();를 삽입.

```java
class Point{
    int x;
    int y;
    // 기본생성자 선언 필수 Point(){}
    Point(int x, int y){
        this.x = x;
        this.y = y;
    }
}
class Point3D extends Point{
    int z;
    Point3D(int x, int y, int z){
        // 컴파일러가 자동 삽입 super();    ==> 기본생성자가 Point class에 존재하지 않음 ==> 에러 
        // 생성자의 첫 줄에 반드시 생성자를 호출해야 한다. 
        this.x = x; 
        this.y = y;
        this.z = z;
    }
}

// 에러 
class PointTest{
    public static void main(String[] args){
        Point3D p3 = new Point3D();
    }
}
```

패키지
-----

* 서로 관련된 클래스의 묶음
* 클래스는 클래스 파일(*.class), 패키지는 폴더. 하위패키지는 하위 폴더. 
* 클래스의 실제이름(full name)은 패키지를 포함.(java.lang.String)
* rt.jar (runtime.) 실행할 때 필요한 클래스파일들을 묶어논 파일) JDK설치경로₩jre₩lib에 위치

패키지의 선언
-----

* 패키지는 소스파일의 첫번쨰 문장으로 단 한번 선언
* 같은 소스 파일의 클래스들은 모두 같은 패키지에 속하게 된다.
* 패키지 선언이 없으면 이름없는(unnamed)패키지에 속하게 된다. (default package)

클래스 패스(classpath)
-----

* 클래스 파일(*.class) 의 위치를 알려주는 경로(path)
* 환경변수 classpath로 관리하며, 경로간의 구분자는 ':'를 사용 
* classpath(환경변수)에 패키지의 루트를 등록해줘야 함. 

