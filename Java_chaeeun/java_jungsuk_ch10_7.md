ArrayList
-----

* ArrayList는 기존의 Vector를 개선한 것으로 구현원리와 기능적으로 동일
* ArrayList와 달리 Vector는 자체적으로 동기화처리가 되어 있다. 
* List 인터페이스를 구현하므로, 저장순서가 유지되고 중복을 허용한다. 
* 데이터의 저장공간으로 배열을 사용한다.(배열기반) 


ArrayList의 메서드
-----

+ 생성자
    * ArrayList()   
    * ArrayList(Collection c)
    * ArrayList(int initial Capacity)

+ 추가 메서드 
    * boolean add(Object o)
    * void add(int index, Object element)
    * boolean addAll(Collection c)
    * boolean addAll(int index, Collection c)

+ 삭제 메서드
    * boolean remove(Object o)
    * Object remove(int index)
    * boolean removeAll(Collection c)
    * void clear() - 모든 객체 삭제

+ 검색
    * int indexOf(Object o)
    * int lastIndexOf(Object o)
    * boolean contains(Object o)
    * Object get(int index)
    * Object set(int index, Object element)

 * List subList(int fromIndex, itn toIndex)
 * Object[] toArray()   - ArrayList의 객체배열을 반환
 * Object[] toArray()(Object[] a)
 * boolean isEmpty()
 * void trimToSize()    - 빈공간 제거
 * int size() - 저장된 갯수 반환 

 ```java
 ArrayList list1 = new ArrayList(10);
 list1.add(new Integer(5));
 list1.add(new Integer(4));
 list1.add(new Integer(2));
 list1.add(new Integer(0));
 list1.add(new Integer(1));
 list1.add(new Integer(3));

 ArrayList list2 = new ArrayList(list1.subList(1,4));
 // list1: [5, 4, 2, 0, 1, 3]
 // list2: [4, 2, 0]

 Collections.sort(list1);   // 오름차순 정렬
 Collections.sort(list2);   
 // 0 1 2 3 4 5
 // 0 2 4

 System.out.println(list1.containsAll(list2));
 // list1이 list2의 모든 요소 포함?  true 

 list2.add("b");
 list2.add("c");
 // 0 2 4 b c
 list2.add(3,"a");
 // 0 2 4 a b c
 
 list2.set(3,"aa");
 // 0 2 4 aa b c

 list1.add(0, "1");
 // 1   0      1     2 3 4 5 
 // "1"   (Integer)
 System.out.pritnln(list1.indexOf("1"));
 // 0 
 System.out.println(list1.indexOf(1));
 // 2 

 list1.remove(0); 
 // 0 1 2 3 4 5 
 
 list1.remove(new Integer(1));  // Integer  1 삭제
 // 1 0 2 3 4 5 

// list1.remove(1); // index 1 삭제 

System.out.println(list1.retainAll(list2));
// list1에서 list2와 겹치는 부분을 삭제 

// list2에서 list1에 포함된 객체들을 삭제한다.
for(int i = list2.size()-1; i >=0; i--){
    if(list1.contains(list2.get(0))){
        list2.remove(i);
    }
}
```


ArrayList에 저장도니 객체의 삭제과정 
-----

* ArrayList에 저장된 세 번째 데이터(data[2])를 삭제하는 과정. list.remove(2); 호출
> data[0] data[1] data[2] data[3] data[4] data[5] data[6]
>   0       1       2       3       4       null    null 
1. 삭제할 데이터 아래의 데이터를 한칸 씩 위로 복사해서 삭제할 데이터를 덮어쓴다. 
 * System.arraycopy(data, 3, data, 2, 2)    - data[3]에서 data[2]로 2개의 데이터를 복사 
>   0       1       3       4       4       null    null
2. 데이터가 모두 한 칸씩 이동했으므로 마지막 데이터는 null로 변경
 * data[size-1] = null;
>   0       1       3       4       null    null    null
3. 데이터가 삭제되어 데이터의 갯수가 줄었으므로 size 값을 감소시킨다. 
 * size--; 

+ 마지막 데이터를 삭제하는 경우, 1번의 과정(배열의 복사)는 필요없다. 
+ 1번 과정은 부담이 많이 가는 작업. 일어나지 않도록 하는 것이 좋다. 
```java
// 배열 복사 발생 
for(int i = 0; i < list.size(); i++){
    list.remove(i);
}

// 배열 복사 발생안함 
for(int i = list.size(); i >=0; i--){
    list.remove(i)
}
```

LinkedList - 배열의 장단점
-----

* 장점 : 배열은 구조가 간단하고, 데이터를 읽는데 걸리는 시간(접근시간, access time) 이 짧다.

* 단점 : 크기를 변경할 수 없다. 
    + 크기를 변경해야 하는 경우 새로운 배열을 생성 후 데이터를 복사해야 함. 
    + 크기 변경을 피하기 위해 충분히 큰 배열을 생성하면, 메모리가 낭비됨. 
* 단점2 : 비순차적인 데이터의 추가, 삭제에 시간이 많이 걸린다.
    + (배열 중간의 요소 추가, 삭제)
    + 데이터를 추가하거나 삭제하기 위해, 다른 데이터를 옮겨야 함. 
    + 그러나 순차적인 데이터 추가(끝에 추가) 와 삭제(끝부터 삭제)는 빠르다. 

LinkedList - 배열의 단점을 보완
-----

* 배열과 달리 LinkedList는 불연속적으로 존재하는 데이터를 연결(Link)
* 노드의 연결 ( 다음 노드의 주소를 가지고 있다. )
* 데이터의 삭제 : 단 한 번의 참조변경만으로 가능 
* 데이터의 추가 : 한 번의 Node객체 생성과 두 번의 참조변경만으로 가능 


LinkedList - 이중 연결 리스트
-----

* linked list - 연결 리스트. 데이터 접근성이 나쁨
* doubly linked list - 이중연결리스트, 접근성 향상 
* 다음 요소, 이전 요소 두 개 참조를 가지고 있음. 
* doubly circular linked list - 이중 원형 연결리스트
    + 양 끝 마지막 요소 연결 


ArrayList(배열기반) vs LinkedList(연결기반) - 성능 비교
-----

1. 순차적으로 데이터를 추가/삭제 - ArrayList가 빠름
2. 비순차적으로 데이터를 추가/삭제 - LinkedList가 빠름 
3. 접근시간(access time) - ArrayList가 빠름 