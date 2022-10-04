인터페이스(interface)
-----

##### 추상메서드의 집합
##### 구현된 것이 전혀 없는 설계도. 껍데기. (모든 멤버가 public)

```java
interface 인터페이스명 {
    public static final 타입 상수이름 = 값; // 변수는 가질 수 없음 iv x, cv x 
    public abstract 메서드이름(매개변수); 
}

interface PlayingCard{
    public static final int SPADE = 4;  // 상수
    final int DIAMOND = 3;  // public static final 생략가능 
    static int HEART = 2;   // 항상 public static final
    int CLOVER = 1;

    public abstract String getCardNumber(); // 항상 public static
    String getCardKine();   // public abstract 생략 가능 
}
```

* 인터페이스의 조상은 인터페이스만 가능(Object가 최고 조상 아님) 
* 다중 상속이 가능 (추상 메서드는 충돌해도 문제 없음)
```java
interface Fightable extends Movable, Attackable{}

interface Movable{
    void move(int x int y);
}

interface Attackable{
    void attack(Unit u);
}
```

인터페이스의 구현
-----

##### 인터페이스에 정의된 추상 메서드를 완성하는 것 
```java
class  클래스명 implements  인터페이스명 {
    // 인터페이스에 정의된 추상메서드를 모두 구현해야 한다. 
}

class Fighter implements Fightable{
    public void move(int x, int y){
        // 내용생략
    }
    public void attack(Unit u){
        // 내용생략 
    }
}
```
* 일부만 구현하는 경우, 클래스 앞에 abstract 붙여야 함.
```java
abstract class Fighter implements Fightable{
    public void move(int x, int y){
        // ... 
    }
}
```

>   추상 클래스와 인터페이스의 차이점은? 
>   - 인터페이스는 iv를 가질 수 없다. 


인터페이스를 이용한 다형성
-----

* 인터페이스도 구현 클래스의 부모가 될 수 있다. 

```java 
interface Fightable{
    void move(int x, int y);
    void attack(Fightagble f);
}
class Fighter extends Unit implements Fightable{
    public void move(int x, int y){
        //...
    }
    public void attack(Fightable f){
        // ... 
    }
} 
// 인터페이스로 다형성 구현 가능 
Unit u = new Fighter();
Fightable f = new Fighter();

// Fightable이 가진 멤버만 쓸 수 있음 
f.move(100,200);
f.attack(new Fighter());
```

>   매개변수 타입이 interface 라는 것은 
>   interface를 구현한 클래스의 인스턴스만 가능하다.     

*   인터페이스를 메서드의 리턴타입으로 지정할 수 있다. 
>   (Fightable) 인터페이스를 구현한 클래스의 인스턴스를 반환

```java
Fightable method(){
    //...
    Fighter f = new Fighter();
    return f;       // 인터페이스를 구현한 객체를 반환해야함
}
 
// => 
// Fightable로 형변환 가능. (다형성)
Fightable   f = method(); 
           // = new Fighter(); 

``` 

```java
abstract class Unit{
    int x,y;
    abstract viod move(int x, int y);
    void stop(){System.out.println("Stop")}

}

interface Fightable{    
    void move(int x, int y);    // public abstract
    void attack(Fightable f);   // public abstract
}

class Fighter extends Unit implements Fightable{
    // 오버라이딩 규칙: 조상(public) 보다 접근제어자가 좁으면 안된다.
    // public 안붙이면 default ==> ERROR
    public void move(int x, int y ){
        System.out.println(x + ", " + y + "로 이동");
    }
    public void attack(Fightable f){
        System.out.println(f + "를 공격");
    }

    // 리턴타입 interface
    Fightable getFightable(){
        Fighter f = new Fighter();  
        return f;   // (Fightable)f 
        // Fightable 인터페이스를 구현한 클래스의 인스턴스를 반환
    }
}

public class FighterTest{
    public static void main(String[] args){
        Fighter f = new Fighter();
        f.move(100,200);
        f.attack(new Fighter());
        Fightable f3 = f.getFightable();

        // 다형성
        Unit u = new Fighter();
        u.move(100,200);
        u.stop();
        //  u.attack(new Fighter());    // Unit객체에는 attack 없음 

        Fightable f2 = new Fighter();
        f2.move(100,200);
        f2.attack(new Fighter());
        // f2.stop();  // Fightable 에는 stop()이 없음 
    }
}
``` 


