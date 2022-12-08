HashSet - 순서 X, 중복 X
-----

* HashSet 
    + Set 인터페이스를 구현한 대표젹인 컬렉션 클래스
    + 순서를 유지하려면, LinkedHashSet클래스를 사용하면 된다. 
* TreeSet
    + 범위 검색과 정렬에 유리한 컬렉션 클래스 
    + HashSet 보다 데이터 추가, 삭제에 시간이 더 걸림 


HashSet - 주요 메서드
-----

* Hashset() // 생성자
* HashSet(Collection c)
* HashSet(int initialCapacity)  // 초기용량
* HashSet(int initialCapacity, float ladFactor) // 얼만큼 가득찼을 때 늘릴건지. 
* boolean add(Object o)
* boolean addAll(Collection c)  // 합집합 
* boolean remove(Object o)  
* boolean removeAll(Collectio c)    // 교집합 
* boolean retainAll(Collectoin c)   // 조건부삭제(Collection c에 있는거 남기고 삭제 ) - 차집합 구할 때 씀 
* void clear() // 모두 삭제
* boolean contains(Object o)
* boolean containsAll(Collection c)
* iterator iterator()   

* boolean isEmpty()
* int size()
* Object[] toArray()
* Object[] toArray(Object[] a)

```java
class Ex11_4{
    public static void main(String[] args){
        Object[] objArr = {"1", new Integer(1), "2","2","3","3","4","4","4"};

        for(int i = 0; i < objArr.length; i++){
            set.add(ObjArr[i]); 
        }
        // [1, 1, 2, 3, 4]
        // "1"과 Integer(1) 은 다른 객체. 

        //  Iterator를 이용해 HashSEt에 저장된 요소들 출력하기 
        Iterator it = set.iterator();

        while(it.hasNext()){
            System.out.println(it.next());
        }
    }
}
```

```java
class Ex11_5{
    public static void main(String[] args){
        Set set = new HashSet();

        // set의 크기가 6보다 작은 동안 1~45 사이의 난수를 저장 
        for(int i =0; set.size()<6; i++ {
            int num = (int)(Math.random()*45) + 1;
            set.add(num);
        }
        // set은 정렬할 수 없음 (순서 유지가 안됨)
        // sort의 매개변수로 list만 될수 있다. 
        // set을 list로 옮기고 정렬해야 함. 
        List list = new LinkedList(set);    // Linkedlist(Collection c)
        Collections.sort(list); // Collections.sort(List list);
    }
}
```

* HashSet은 객체를 저장하기 전에 기존에 같은 객체가 있는지 확인 
* 같은 객체가 없으면 저장하고, 있으면 저장하지 않는다. 
* boolean add(Object o)는 저장할 객체의 equals()와 hashCode()를 호출 
* equals()와 hashCode()가 오버라이딩 되어 있어야 함. 
    ```java
    public boolean equals(Object obj){
        if(!(obj instanceof Person)) return false;

        Person tmp = (Person)obj;

        return name.equals(tmp.name) && age == tmp.age;
    }
    public int hashCode(){
        return Objects.hash(name + age);
    }
    ```

```java
Hash set = new HashSet();

set.add("abc");
set.add("abc");
set.add(new Person("david",12));
set.add(nwe Person("david",12));

System.out.println(set);
// [abc, david:12  , david:12]
// Person객체에 equals와 hashCode가 오버라이딩 안되어있으면 중복제거하지 못하고 다르게 동작. 

class Person{
    String name;
    int age;

    @Override
    public int hashCode(){
        // int hash(Object... values); // 가변인자
        return Objects.hash(name, age);
    }

    @Override
    public boolean equals(Object obj){
        if(!(obj intanceof Person)) return false;

        Person p = (Person)obj;

        return this.name.equals(p.name) && this.age == p.age;
    }

    Person(String name, int age){
        this.name = name;
        this.age = age;
    }

    public String toString(){
        return name + ":" + age
    }
}
```

```java
HashSet setA = new HashSet();
HashSet setB = new HashSet();
HashSet setHab = new HashSet();
HashSet setKyo = new HashSet();
HashSet setCha = new HashSet();

setA.add("1"); 
setA.add("2"); 
setA.add("3"); 
setA.add("4"); 
setA.add("5"); 

setB.add("4");
setB.add("5");
setB.add("6");
setB.add("7");
setB.add("8");

// 교집합
Iterator it = setB.iterator();
while(it.hasNext()){
    Object tmp = it.next();
    if(setA.contains(tmp))
        setKyo.add(tmp);
}
// === 교집합 
// setA.retainAll(setB);   // 교집합
                        // setA에 공통된 요소만 남기고 삭제 

// 차집합
it = setA.iterator();
while(it.hasNext()){
    Object tmp = it.next();
    if(!setB.contains(tmp))
        setCha.add(tmp)
}
// === 차집합  
// setA.removeAll(setB);   // 공통된 요소 제거 

// 합집합
it = setA.iterator();
while(it.hasNext())
    setHab.add(it.next());

it = setB.iterator();
while(it.hasNext())
    setHab.add(it.next());

// === 
// setA.addAll(setB);  // setB의 모든 요소 추가(중복 제외)
```

