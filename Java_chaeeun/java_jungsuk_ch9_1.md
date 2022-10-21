Object 클래스
-----

* 모든 클래스의 최고 조상. 오직 11개의 메서드만을 가지고 있다. 
* notify(), wait() 등은 쓰레드와 관련되 메서드이다. 
* Object 클래스의 메서드
    + public boolean equals(Object obj)
    + protected Object clone()
        - protected 메서드는 오버라이딩 해서 public으로 변경해서 사용해야함 
    + public Class getClass()   (설계도객체(Class) 반환)
        - 객체의 클래스 정보(설계도 정보)를 담고 있는 Class인스턴스를 반환한다.
    + public int hashCode()
    + public String toString()

equals(Object obj)
-----

* 객체 자신(this)과 주어진 객체(obj)를 비교한다. 
* Object클래스의 equals()는 객체의 주소를 비교(참조변수 값 비교)
```java
public boolean equals(Object obj){
    return (this == obj);
}

class Value{
    int value;

    value(int value){
        this.value = value;
    }
}

class Ex9_1{
    public static void main(String[] args){
        Value v1 = new Value(10);
        Value v2 = new Value(10);

        System.out.println(v1.equals(v2)); // false
    }
}
```

equals(Object obj)의 오버라이딩
-----

* 인스턴스 변수(iv)의 값을 비교하도록 equals()를 오버라이딩 해야한다. 
```java
class Person{
    long id;

    public boolean equals(Object obj)  {
        if(obj instanceof Person){
            return id == ((Person)obj).id;  // obj가 Object타입이므로 id값을 참조하기 위해서는 Person타입으로 형변환 필요 
        }else{
            return false;   
        }
    }

    Person(long id){
        this.id = id;
    }
}

Person p1 = new Person(84444444222L);
Person p2 = new Person(84444444222L);

p1.equals(p2);   // true
```





hashCode()
-----

* 객체의 해시코드(hash code)를 반환하는 메서드
* Object 클래스의 hashCode()는 객체의 주소를 int로 변환해서 반환 

* equals()를 오버라이딩 하면, hashCode()도 오버라이딩 해야 한다.
* equals()의 결과가 true인 두 객체의 해시코드는 같아야 하기 때문
```java
String str1 = new String("abc");
String srr2 = new String("abc");
System.out.println(str1.equals(str2)); // true
System.out.println(str1.hashCode());    // 96345
System.out.println(str2.hashCode());    // 96345
```
* cf) System.identityHashCode(Object obj)는 Object클래스의 hashCode()와 동일
```java
System.out.println(System.itendityHashCOde(str1)); // 235353
System.out.println(System.itendityHashCOde(str1)); // 765321
```


toString(), toString()의 오버라이딩
-----

* toString(): 객체를 문자열(String)으로 변환하기 위한 메서드
```java
public String toString(){   // Object 클래스의 toString()
    return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

