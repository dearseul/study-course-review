래퍼(wrapper) 클래스
-----

* 기본형 값을 감싸는 클래스
* 8개의 기본형을 객체로 다뤄야할 때 사용하는 클래스
```java
public final class Integer extends Number implements Comparable{
    ...
    private int value;  // <- 기본형을 감싸고 있음
    ...
}
```

* 기본형 - 래퍼클래스
* boolean - Boolean
* char - Character
* byte - Byte
* short - Short
* int - Integer
* long - Long
* float - Float
* double - Double
```java
Boolean(boolean value)
Boolean(String s)
Boolean b = new Boolean(true);
Boolean b2 = new Boolean("true");

Character c = new Character('a');

Integer i = new Integer(100);
Integer i2 = new Integer("100");
...
```

```java
class Ex9_1{
    public static void main(String[] args){
        Integer i = new Integer(100);
        Integer i2 = new Integer(100);

        System.out.println(i == i2); // false 
        System.out.println(i.equals(i2)); // true
        System.out.println(i.compareTo(i2)); // 0
        // compareTo : 같으면 0, 작으면 양수, 크면 음수 (정렬에 사용)
        System.out.println(i.toString());   // 100 

        System.out.println(Integer.MAX_VALUE);  // 20억 ( 상수값 )
        System.out.println(Integer.MIN_VALUE);  // -20억 ( 상수값 )
        System.out.println(Integer.SIZE + "bits");   // 32 bits
        System.out.println(Integer.BYTES + "bytes");  // 4 bytes
        System.out.println(Integer.TYPE);   // int 
    }
}
```

Number 클래스
-----
* 모든 숫자 래퍼 클래스의 조상 
* Object
* Object - boolean Character Number
* Number - byte Short Integer Long FLoat Double Biginteger(아주 큰 정수) BigDecimal(아주 큰 실수)
```java
public abstract class Number implements java.io.Serializable{ // 추상 클래스 
    public abstract int intValue() // 래퍼 객체 값을 기본형으로 바꾸는 메서드를 가지고 있다. 
    public abstract long longValue();
    public abstract float floatValue();
    public abstract double doubleValue();

    public byte byteValue(){
        return (byte)intValue();
    }

    public short shortValue(){
        return (short)intValue();
    }
}
```
 