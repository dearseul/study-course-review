추상클래스(abstract class)
-----

##### 미완성 설계도. 미완성 메서드를 갖고 있는 클래스

```java
abstract class Player{  // 추상 클래스(미완성 클래스)
    abstract void play(int pos);    //추상 메서드
    abstract void stop();       // 추상 메서드 
}
```

##### 다른 클래스 작성에 도움을 주기 위한 것. 인스턴스 생성 불가. 
```java
Player p = new Player();    // 에러. 
```

##### 상속을 통해 추상 메서드를 완성해야 인스턴스 생성 가능.
```java
class AudioPlayer extends Player{
    void play(int pos){/*내용 생략*/}   // 추상 메서드를 구현 
    void stop(){/*내용 생략*/}          // 추상 메서드를 구현 
}

AudioPlayer ap = new AudioPlayer(); // OK
```

추상메서드(abstract method)
-----

* 미완성 메서드. 구혀부(몸통{}) 없는 메서드
* abstract 리턴타입 메서드이름();
* 꼭 필요하지만 자손마다 다르게 구현될 것으로 예상되는 경우 
```java
abstract class Player{
    abstract void play(int pos);
    abstract void stop();
}

class AudioPlayer extends Player{       // 완전 클래스 
    void play(int pos){ /*내용생략*/ }
    void stop(){/*내용생략*/}
}

abstract class AbstractPlayer extends Player{      // 미완성 클래스 
    void play(int pos){/*내용생략*/}        // 추상 메서드 중 1개만 구현 
}
```

##### 추상 메서드 호출 가능(호출할 때는 선언부만 필요)

```java
abstract class Player{
    boolean pause;
    int currentPos;

    Player(){
        pause = false;
        currentPos = 0;
    }

    // 추상 메서드 만들어놓으면 쓰도록 강제하는 효과가 있다. 
    abstract void play(int pos);    // 추상 메서드
    abstract void stop();           // 추상 메서드 

    void play(){    // 인스턴스 메서드 
        play(currentPos);   // 추상메서드를 사용할 수 있다. 
    }                       // 1. 상속을 통해서 자손이 몸통 완성 가능
}                           // 2. 자손 객체 생성 
                            // 3. 자손객체 참조변수.play(); 
```

추상클래스의 작성 
-----

##### 여러 클래스에 공통적으로 사용될 수 있는 추상클래스를 바로 작성하거나
##### 기존클래스의 공통 부분을 뽑아서 추상클래스를 만든다. 

```java 
class Marine{
    int x, y;
    void move(int x, int y){}
    void stop(){}
    void stimPack(){}
}
class Tank {
    int x, y;
    void move(int x, int y){}
    void stop(){}
    void changeMode(){}
}
class Dropship{
    int x, y;
    void move(int x, int y){}
    void stop(){}
    void load(){}
    void unload(){}
}

// ==> 공통부분 추출 (선언부만 뽑아냄)
abstract class Unit{
    int x, y;
    abstract void move(int x, int y);
    void stop(){}
}

class Marine extends Unit{
    void move(int x, int y){}
    void stimPack(){}
}
class Tank extends Unit{
    void move(int x, int y){}
    void changeMode(){}
}
class Dropship extends Unit{
    void move(int x, int y){}
    void load(){}
    void unload(){}
}

// ==> 다형성 
// Unit[] group = {new Marine(), new Tank(), new Dropship()};
Unit[] group = new Unit[3];
group[0] = new Marine();
group[1] = new Tank();
group[2] = new Dropship();

for(int i = 0; i < group.length; i++){
    group[i].move(100,200);
}
``` 

#### 객체지향에서 추상화 라는 것은 추상클래스 이상의 의미가 있다. 
##### 추상화 <--> 구체화 
* 추상화된 코드는 구체화된 코드보다 유연하다. 변경에 유리.
```java
GregorianCalendar cal = new GregorianCalender(); // 구체적
Calender cal = Calender.getInstance();       // 추상적 
// 추상클래스        // Calender (자손)객체를 반환 (불분명) 

public static Calendar getInstance(Locale aLocale){
    return createCalendar(TimeZone.getDefault(), aLocale);
}
private static Calendar createCalendar(TimeZone zone, Locale aLocale){
    // ... 
    if(caltype != null){
        switch(caltype){
            case "buddhis":
                car = new BuddhistCalendar(zone, aLocale);
                break;
            case "japanese":
                cal = new JapanesImperialCalendar(zone, aLocale);
                break;
            case "gregory":
                cal = new GregorianCalendar(zone, aLocale);
                break;
        }
    }
}
```



