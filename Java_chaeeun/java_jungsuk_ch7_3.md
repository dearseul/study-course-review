import 문
-----

* 클래스를 사용할 때 패키지 이름을 생략할 수 있다. 
* 컴파일러에게 클래스가 속한 패키지를 알려준다. 
* ctrl + shift + O 

* java lang 패키지의 클래스는 import 하지 않고도 사용할 수 있다. 
    + String, Object, System, Thread ... 

import 문 선언
-----

* import 패키지명.클래스명;
* import 패키지명.* 

static import 문
-----

### static 멤버를 사용할 때 클래스 이름을 생략할 수 있게 해준다. 
```java
import static java.lang.Integer.*;  // Integer클래스의 모든 static 메서드
import static java.lang.Math.random;        // Math.random()만.
import static java.lang.System.out;     // System.out을 out만으로 참조가능. 

out.println(random());
```

제어자(modifier)
-----

* 클래스와 클래스의 멤버(멤버 변수, 메서드)에 부가적인 의미 부여 
* 접근제어자 : public, protected, (default), private
* 그 외    : static, final, abstract, native, transient, synchronized, volatille, strictfp

* 하나의 대상에 여러 제어자를 같이 사용 가능 (접근제어자는 한개만)
```java
public class ModifierTest{
    public static final int WIDTH = 200;

    public static void main(String[] args){
        System.out.println("WIDTH = " + WIDTH);
    }
}
```

static - 클래스의, 공통적인
-----
### static 
+ 멤버변수
    - 모든 인스턴스에 공통적으로 사용되는 클래스 변수가 된다.
    - 클래스 변수는 인스턴스를 생성하지 않고도 사용 가능하다.
    - 클래스가 메모리에 로드될 때 생성된다.
+ 메서드
    - 인스턴스를 생성하지 않고도 호출 가능한 static 메서드가 된다.
    - static 메서드 내에서는 인스턴스 멤버들을 직접 사용할 수 없다. 
```java
class StaticTest{
    static int width = 200;     // 클래스 변수(static 변수)
    static int height = 300;    // 클래스 변수(static 변수)

    static{

    }

    static int max(int a, int b){   // 클래스 메서드 (static 메서드)
        return a > b ? a : b;
    }
}
```

final - 변경될 수 없는, 마지막의
-----

### final
+ 클래스
    - 변경될 수 없는 클래스, 확장될 수 없는 클래스가 된다.
    - 그래서 Final로 지정된 클래스는 다른 클래스의 조상이 될 수 없다.
+ 메서드
    - 변경될 수 없는 메서드.
    - final로 지정된 메서드는 오버라이딩을 통해 재정의 될 수 없다. 
+ 멤버변수
+ 지역변수
    - 변수 앞에 final이 붙으면, 값을 변경할 수 없는 상수가 된다. 

```java
final class FinalTest{
    final int MAX_SIZE = 10;

    final void getMaxSize(){
        final int LV = MAX_SIZE;
        return MAX_SIZE;
    }
} 
```

abstract - 추상의, 미완성의
-----

### abstract
+ 클래스
    - 클래스 내에 추상메서드가 선언되어 있음을 의미한다.
+ 메서드
    - 선언부만 작성하고 구현부는 작성하지 않은 추상 메서드임을 알린다.

```java
abstract class AbstractTest{    // 추상 클래스(추상 메서드를 포함한 클래스) 
    abstract void move();   // 추상메서드(구현부가 없는 메서드)
}
```
* 미완성 설계도 => 제품 생성 불가
```java
AbstractTest a = new AbstractTest();    // 에러. 추상클래스의 인스턴스 생성 불가. 

// 추상클래스를 상속받아서 완전한 클래스(구상클래스)를 만든 후에 객체 생성 가능 
```

접근제어자(access modifier)
-----
* private 같은 클래스 내에서만 접근 가능하다.
* (default) 같은 패키지 내에서만 접근이 가능하다. 
* protected 같은 패키지 + 다른패키지의 자손클래스에서 접근이 가능하다. 
* public 접근 제한이 전혀 없다. 

캡슐화와 접근 제어자
-----

### 접근제어자를 사용하는 이유
*   외부로부터 데이터를 보호하기 위해서 
*   외부에는 불필요한, 내부적으로만 사용되는 부분을 감추기 위해서 

```java
public class Time{
    private int hour;
    private int minute;
    private int second;     // 접근제어자를 private으로 하여 외부에서 직접 접근하지 못하도록 한다. 

    public int getHour(){
        return hour;
    }

    // 메서드는 public 
    public void setHour(int hour){
        if(hour < 0 || hour > 23) return;
        this.hour = hour;
    }

    // ==> 데이터를 보호한다. 
}
```
```java
private boolean isNotValidHour(int hour){   // 외부에는 불필요한, 내부적으로만 사용되는 함수. private 
    return hour < 0 || hour > 23;
}

public void setHour(int hour){
    if(idsNotValidHour(hour)) return;

    this.hour = hour;
}
```

다형성(polymorphism)
-----

* 여러가지 형태를 가질 수 있는 능력 
* 조상 타입 참조변수로 자손 타입 객체를 다루는 것 

```java
class Tv{
    boolean power;  
    int channel;

    void power(){   power = !power  }
    void channelUp(){ ++channel; }
    void chanelDown(){  --channel;  }
}
class SmartTv extends Tv{
    String text;
    void caption(){}

}

Tv t = new SmartTv();   // OK 
```

* 객체와 참조변수의 타입이 일치하지 않을 때의 차이? 
```java
SmartTv s = new SmartTv();  // 참조변수와 인스턴스의 타입이 일치 
Tv t = new SmartTv();       // 조상타입 참조변수로 자손 타입 인스턴스 참조
// smartTv s 리모컨으로는 버튼 7개(smartTv  class 멤버) 다 사용 가능 
// tv t 리모컨으로는 버튼 5개(tv class 멤버) 사용가능
```

* 자손타입의 참조변수로는 조상 타입의 객체를 가리킬 수 없다. 
```java 
Tv t = new SmartTv();   // OK
SmartTv s = new Tv();   // error 
```






