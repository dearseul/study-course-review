참조변수의 형변환
-----

* 사용할 수 있는 멤버의 갯수를 조절하는 것 
* 조상 자손 관계의 참조변수는 서로 형변환 가능 

```java
class Car{
    String color;
    int door;

    void drive(){
        System.out.println("drive,Brr~~");
    }
}
class FireEngine extends Car{
    void water(){
        System.out.println("water!!");
    }
}
// ********
FireEngine f = new FireEngine();

Car c = (Car)f;     // OK. 조상인 Car 타입으로 형변환(생략가능)
FireEngine f2 = (FireEngine)c;  // OK. 자손인 FireEngine타입으로 형변환(생략불가)
Ambulance a = (Ambulance)f; // ERROR.

```
```java
class Ex7_1{
    public static void main(String args[]){
        Car car = null;
        FireEngine fe = new FireEngine();
        FireEngine fe2 = null;

        fe.water();
        car = fe;   // car = (Car)fe; 
        car.water();    // 컴파일 에러. Car타입의 참조변수로는 water()를 호출할 수 없다. 
        fe2 = (FireEngine)car;
        fe2.water();
    }
}
```
```java
    Car c = new Car();
    FireEngine fe3 = (FireEngine)c; // 컴파일 오케이. 
    fe3.water();
    // but. 형변환 에러남 . 
    // 자손- 부모간 형변환은 컴파일 OK 이지만
    // 실행시 형변환에서는 실제 객체가 중요. 
```

instanceof 연산자
-----

* 참조변수의 형변환 가능여부 확인에 사용. 가능하면 true 반환

```java
void doWork(Car c){
    if(c intanceof FireEngine) {    // 1. 형변환이 가능한지 확인
        FireEngine fe = (FireEngine)c;  // 2. 형변환
        fe.water();
    }
}
```

매개변수의 다형성
-----
* 참조형 매개변수는 메서드 호출 시, 자신과 같은 타입 또는 자손타입의 인스턴스를 넘겨줄 수 있다. 

#### 다형성의 장점
1. 다형적 매개변수
2. 하나의 배열로 여러종류의 객체를 다룰 수 있다. 

> 다형적 매개변수

```java
class Product{
    int price;
    int bonusPoint; 
}
class Tv extends  Product{}
class Computer extends Product{}
class Audio extends Product{}

class Buyer{
    int money = 1000;
    int bonusPoint = 0;
}

void buy(Tv t){
    money -= t.price;
    bonusPoint += t.bonusPoint;
}

void buy(Computer c){   // 오버로딩
    money -= c.price;
    bonusPoint += c.bonusPoint;
}
// ... 
// => 다형적 매개변수 
void buy(Product p){
    money -= p.price;
    bonusPoint += p.bonusPoint;
}
```

```java
class Product{
    int price;
    int bonusPoint;

    Product(int price){
        this.price = price;
        bonusPoint = (int)(price/10.0);
    }
}
class Tv1 extends Product{
    Tv1(){
        super(100); // 조상클래스의 생성자 Product(int price)를 호출 
    }
    // Object 클래스의 toString()을 오버라이딩 한다. 
    Public String toString(){return "Tv";}
}
class Computer extends Product{
    Computer(){super(200);}
    public String toString(){return "Computer";}
}

class Buyer{
    int money = 1000;
    int bonusPoint = 0;

    void buy(Product p){
        if(money < p.price){
            System.out.println("잔액이 부족하여 물건을 살 수 없습니다.");
            return;
        }
        money -= p.price;
        bonusPoint += p.bonusPoint;
        System.out.println(p + "을/를 구입하였습니다.");
                        // p.toString()
                        // 참조변수 + 문자열 결합 => 참조변수.toString()
    }
}
class Ex7_2{
    public static void main(String args[]){
        Buyer b = new Buyer();

        b.buy(new Tv1());
        b.buy(new Computer());

        System.out.println("현재 남은 돈은 " + b.money +"만원입니다.");
        System.out.println("현재 보너스 점수는 " + b.bonusPoint + "원 입니다.");

    }
}
```

여러 종류의 객체를 배열로 다루기
-----

> 하나의 배열로 여러종류의 객체를 다룰 수 있다. 
```java
Product p = new Product[3];
p[0] = new Tv();
p[1] = new Computer();
p[2] = new Audio();
```

```java
class Buyer2{
    int money = 1000;
    int bonusPoint = 0;

    Product[] cart = new Product[10];

    int i =0;
    void buy(Product p){
        if(money < p.price){
            System.out.println("잔액부족");
            return;
        }

        money -= p.price;
        bonusPoint += p.bonusPoint;
        cart[i++] = p;
    }

    void summary(){
        int sum = 0;
        String itemList = "";

        for(int = 0; i < cart.length; i++){
            if(cart[i] == null)break;
            sum += cart[i].price;
            itemList += cart[i] + ", ";
        }
        System.out.println("구입물품 총금액: " + sum + "만원" );
        System.out.println("구입제품: " + itemList);
    }
}
```
```java
class Ex7_3{
    public static void main(String args[]){
        Buyer2 b = new Buyer2();

        b.buy(new Tv2());
        b.buy(new Computer2());
        b.buy(new Audio2());
        b.summary();
    }
}
```
* cf) Vector class => 모든 종류의 객체 저장 가능 (Object 배열이 있음)













