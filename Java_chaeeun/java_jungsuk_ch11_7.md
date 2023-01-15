Collections - 컬렉션을 위한 메서드(static)를 제공 
-----

* ex) Objects, Arrays, Colletions 
1. 컬렉션 채우기, 복사, 정렬, 검색 - fill(), copy(), binarySearch()
2. 컬렉션의 동기화 - synchronizedXXX()
    + static Collection synchronizedCollection(Collection c)
    + static List synchronizedList(List list)
    + static set synchronizedSet(Set s)
    + static Map synchronizedMap(Map m)
    + static SortedSet synchronizedSortedSet(SortedSet s)
    + static SortedMap synchronizedSortedMap(SortedSet s)
* cf) (배열기반) Vector(동기화 O), ArrayList(동기화 X) - 필요할때만 동기화 가능 
* Collection을 동기화 할때 위 메서드 들을 쓴다. 
    + List syncList = Collections.synchronizedList(new ArrayList(...));
    
3. 변경불가(readOnly) 컬렉션 만들기 - unmodifiableXXX()
    + static Collection unmodifiableCollection(Collection c)
    + static List unmodifiableList(List list)
    + static Set unmodifiableSet(Set s)
    + static Map unmodifiableMap(Map m)
    + static NavigableSet unmodifiableNavigableSet(NavigableSet s)
    + static SortedSet unmodifiableSortedSet(SortedSet s)
    + static NavigableMap unmodifiableNavigableMap(NavigableMap m)
    + static SortedMap unmodifiableSortedMap(SortedMap m)

4. 싱글톤 컬렉션 만들기 - singletonXXX()
    + 객체 1개만 저장하는 컬렉션
    + static List singletonList(Object o)
    + static Set singleton(Object o) - singletonSet 아님. 
    + static Map singletonMap(Object key, Object value)

5. 한 종류의 객체만 저장하는 컬렉션 만들기 - checkedXXX()
    + static Collection checkedCollection(Collection c, Class type)
    + static List checkedList(List list, Class type)
    + static Set checkedSet(Set s, Class type)
    + static Map checkedMap(Map m, Class type)
    + static Queue checkedQueue(Queue queue, Class type)
    + static NavigableSet checkedNavigableSet(NavigableSet s, Class type)
    + static SortedSet checkedSortedSet(SortedSet s, Class type)
    + static NavigableMap checkedNavigableMap(NavigableMap m, Class type)
    + static SortedMap checkedSortedMap(SortedMap m, Class type)
    ```java
    List list = new ArrayList();
    List checkedList = checkedList(list, String.class); // String 한 가지 타입만 저장 가능 
    checkedList.add("abc");
    checkedList.add(new Integer(3));    // 에러. ClassCastException 발생
    ```

```java
import java.util.*;
import static java.util.Collectionss.*; 

class Ex11_9{
    public static vid main(String[] args){
        List list = new ArrayList();
        System.out.println(list);
        // []

        addAll(list,1,2,3,4,5);
        System.out.println(list);
        // [1,2,3,4,5]

        rotate(list,2); // 반시계방향으로 두번 회전
        System.out.println(list);
        // [ 4,5,1,2,3];

        swap(list,0,2); // 첫번째와 세번째 교환
        // [1,5,4,2,3]

        shuffle(list); // 섞음

        sort(list,reverseOrder())   // 역순 정렬  reverse(list);
        // [5,4,3,2,1]

        sort(list);
        // [ 1,2,3,4,5]

        int idx = binarySearch(list,3); // 3 이 저장된 위치
        // index of 3 = 2 

        System.out.println("max = " + max(list));
        System.out.println("min = " + min(list));
        System.out.println("min = " + max(list, reverseOrder()));

        fill(list, 9);  // list를 9로 채움
        // [9,9,9,9,9]

        // list와 같은 크기의 새로운 List를 생성하고 2로 채운다. 단, 결과는 변경불가
        List newList = nCopies(list.sizse(), 2);
        // newList = [2,2,2,2,2]

        System.out.println(disjoint(list,newList)); // 공통 요소가 없으면 true
        // true

        copy(list,newList);
        // newList = [2,2,2,2,2]
        // list = [2,2,2,2,2]

        replaceAll(list,2,1);
        // [ 1,1,1,1,1]

        // iterator와 같음 
        Enumeration e = enumeration(list);
        ArrayList list2 = list(e);
        System.out.println("list2 = " + list2);
        // list2 = [1,1,1,1,1]        
    }
}
```

컬렉션 클래스 정리 & 요약 
-----

* ArrayList, Vector (배열기반)
    + (Vector을 가지고 ) Stack 구현 
* LinkedList(추가, 삭제 기능 향상 )
    + Queuer 구현. 
* ArrayList + LinkedList
    + HashMap(검색기능향상. 배열과 LinkedList 결합)
    + HashTable
    + 배열의 장점 + LinkedList의 장점 결합 
        - HashSet - HashMap 가지고 만듬 
        - Properties(HashMap의 변형) - (String, String)
            - key와 value를 String으로만 저장
            - 파일의 읽기와 쓰기가 용이하다. 
        - LinkedHashMap(순서유지 기능 향상)  (<- HashMap)
        - LinkedHashSet (순서유지 기능 향상)  (<- HashSet)
* LinkedList 에서 연결 기반 변형 (tree 구조)
    + TreeMap(범위 검색, 정렬기능 향상) 
    + 최대 2개까지 연결 
        - TreeSet - TreeMap 가지고 만듬 
        
         

