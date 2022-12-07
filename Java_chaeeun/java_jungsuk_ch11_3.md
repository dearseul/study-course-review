Comparator 와 Comparable
-----

* 객체 정렬에 필요한 메서드(정렬기준 제공)를 정의한 인터페이스
    + Comparable : 기본 정렬기준을 구현하는데 사용
    + Comparator : 기본 정렬기준 외의 다른 기준으로 정렬하고자 할 때 사용 
    ```java
    public interface Comparator{
        int compare(Object o1, Object o2);  // o1, o2 두 객체 비교 
                                            // 양수: 왼쪽큰, 음수: 오른쪽 큼, 0: 같다
        boolean equals(Object obj); // equals를 오버라이딩 하라는 뜻 
    }
    public interface Comparable{
        int compareTo(Object o);    // 주어진 객체(o)를 자신과 비교 
    }

    // 정렬 sort() ? : 1. 두 대상 비교, 2. 자리 바꿈 
    ```

* compare()과 CompareTo()는 두 객체의 비교결과를 반환하도록 작성 
```java
public final class Integer extends Number implements Comparable{
    ...
    public int compareTo(Integer anotherInteger){
        int v1 = this.value;
        int v2 = anotherInteger.value;

        // 같으면 0, 오른쪽 크면 -1, 작으면 1 반환
        return (v1 < v2 ? -1 : (v1 == v2 ? 0 : 1));
    }
}
``` 

```java 
String[] strArr = {"cat", "Dog", "lion", "tiger"};
// static void sort(Object[] a) // 객체 배열에 저장된 객체가 구현한 Comparable에 의한 정렬 
// static void sort(Object[] a, Comparator c);  // 지정한 Comparator 에 의한 정렬 
Arrays.sort(strArr);    // String의 Comparable 구현에 의한 정렬
// [Dog, cat, lion, tiger]
Arrays.sort(strARr, String.CASE_INTENSIVE_ORDER); // 대소문자 구분 안함 
                    // 정렬기준 (String class에 있는 static 상수. (comprator() )
// cat, Dog, lion, tiger

Arrays.sort(strArr, new Descending());  // 역순 정렬
// tiger, lion, cat, Dog 

// 정렬기준 
class Descending implements Comparator{
    public int compare(Object o1, Object o2){
        if(o1 instanceof Comparable && o2 instanceof Comparable){
            Comparable c1 = (Comparable)o1;
            Comparable c2 = (Comparable)o2;
            return c1.compareTo(c2) * -1; // -1을 곱해서 기본 정렬방식의 역으로 변경한다. 
        }
        return -1;
    }
}
``` 


Integer와 Comprable
-----

```java
                                    //Integer ㅊ 기본 정렬 기준 제공 
public final class Intger extends Number implements Comparable{
    ... 
    public int compareTo(Object o){
        return compareTo((Integer)o);
    }

    public int compareTo(Integer anotherInteger){
        int thisVal = this.value;
        int anotherVal = anotherInteger.value;

        return (thisVal<anotherVal ? -1 : (thisVal == anotherVal ? 0 : 1));
    }
}

``` 

* 정렬 : 두 대상 비교, 자리 바꿈 비교 (불변)
* 정렬기준은 가변 (가변하는 정렬기준만 제공해 주면 된다. )
* ex) 버블 정렬 
```java
static void sort(int[] intArr){
    for(int i = 0; i< intArr.length-1; i++){
        for(int j= 0; j <intArr.length-1-i;j++){
            // 여기 까진 불변. 정렬기준. 
            int tmp = 0;

            // 정렬기준은 가변. 여기만 바꾸면 된다. 
            if(intArr[j] > intArr[j+1]){
                tmp = intArr[j];
                intArr[j] = intArr[j+1];
                intArr[j+1] = tmp;
            }
        }
    }
}

 