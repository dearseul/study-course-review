타입 변수
-----

* 클래스를 작성할 때, Object타입 대신 타입변수(E)를 선언해서 사용. 
```java 
public class ArrayList extends AbstractList{
    private transient Object[] elementData;
    public boolean add(Object o){
        // ... 
    }
    public Object get(int index){
        // ...
    }
}

// Object를 포함한 클래스는 다 지네릭클래스로 바뀜. (JDK1.5)
// ===> Object 대신  타입변수(<E>)로 바꿈. 
public class ArrayList<E> extends AbstractList<E> {
    private transient E[] elementData;
    public boolena add(E o){
        //...
    }
    public E get(int index){
        // ... 
    }
}
```

* 객체 생성 시, 타입 변수(E) 대신 실제 타입(Tv)을 지정(대입)
```java
// 타입변수 E 대신에 실제 타입 Tv를 대입
ArrayList<Tv> tvList = new ArrayList<Tv>(); 

// ====> 
public class ArrayList<Tv> extends AbstractList<Tv> {
    private transient Tv[] elementData;
    public boolena add(Tv o){
        //...
    }
    public Tv get(int index){
        // ... 
    }
}
```

* 타입 변수 대신 실제 타입이 지정되면, 형변환 생략가능 
```java
ArrayList<Tv> tvList = new ArrayList<Tv>();
tvList.add(new Tv());
Tv t = tvList.get(0);   // 형변환 불필요 
```

```java
import java.util.ArrayList;

class Tv{}

public class GenericTest{
    public static void main(String[] args){
        ArrayList<Tv> list = new ArrayList<Tv>();   
        list.add(new Tv()); 
        // list.add(new Audio()); ERROR

        // (기존 => ) Tv t = (Tv)list.get(0); // 형변환 필요 
        Tv t = list.get(0); // 형변환 불필요 
    }
}
```

* 지네릭스 용어
    + Box<T> : 지네릭 클래스. 'T의 Box' 또는 'T Box'라고 읽는다.
    + T : 타입 변수 또는 타입 매개변수.(T는 타입 문자)
    + Box : 원시 타입(raw type) (일반클래스 -> 지네릭 클래스)
    + class Box<T> {} : 지네릭 클래스 선언
    + Box<String> b = new Box<String>(); : 지네릭 타입 호출. 대입된 타입(String)


* 지네릭 타입과 다형성 
    + 참조 변수와 생성자의 대입된 타입은 일치해야 한다.
    + 자손 - 조상 관계도 안됨 .
    ```java
    ArrayList<Tv> list = new ArrayList<Tv>(); // OK
    ArrayList<Product> list = new ArrayList<Tv>(); // ERROR. 불일치
    ```
    + 지네릭 클래스 간의 다형성은 성립. (여전히 대입된 타입은 일치해야.)
    ```java
    List<Tv> list = new ArrayList<Tv>(); // OK. 다형성. ArrayList가 List를 구현.
    List<Tv> list = new LinkedList<Tv>();   // OK. 다형성. LinkedList가 List를 구현. 
    ```
    + 매개변수의 다형성도 성립. 
    ```java
    ArrayList<Product> list = new ArrayList<Product>();
    list.add(new Product());
    list.add(new Tv()); // OK.  Product 자손도 OK.
    list.add(new Audio()); // OK.  Product 자손도 OK.
    // boolean add(E e){// ... }
    // ===>
    // boolean add(Product e){ ... } ==> Product 자손들도 매개변수로 가능.
    // E get(int index){ ... }
    // ===>
    // Product get(int index){ ... }
    Product p = list.get(0); // 형변환 필요없음.
    // 자손은 형변환 해조야함. 
    Tv t = (Tv)list.get(1); 
    ```

```java
import java.util.*;

class Product {}
class Tv extends Product {}
class Audio extends Product {}

class Ex12_1{
    public static main (String[] args){
        ArrayList<Product> productList = new ArrayList<Product>();
        ArrayList<Tv> tvList = new ArrayList<Tv>();

        productList.add(new Tv());
        productList.add(new Audio());

        tvList.add(new Tv());
        tvList.add(new Tv());
        // tvList.add(new Audio()); // ERROR. 컴파일에러.

        printAll(productList);
        // printAll(tvList); // 컴파일에러. 
        // printAll 매개변수 타입 <Product> 만 가능. 
        // ArrayList<Product> list <=> new ArrayList<Tv>(); // 불일치. 
    }

    public static void printAll(ArrayList<Product> list){
        for(Product p : list)
            System.out.println(p);
    }
}







