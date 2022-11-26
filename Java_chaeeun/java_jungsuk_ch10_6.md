Collection 인터페이스의 메서드
-----

* List, Set 의 공통부분을 뽑아 낸 것 

* boolean add(Object o) 
    + 추가
* boolean addAll(Collection c)
    + 추가
* void clear()  
    + 전체 삭제
* boolean contains(Object o)
    + 검색
* boolean containsAll(COllection c)
    + 검색
* boolean remove(Object o)
    + 삭제
* boolean removeAll(Collection c)
    + 삭제
* boolean equals(Object o)
* int hashCode()
* boolean isEmpty()
    + 비어있는 지 확인
* int size()
* Object[] toArray()
* Object[] toArray(Object[] a)

List 인터페이스 - 순서 O, 중복 O
-----

* ArayList 
* LinkedList
* (Collection 인터페이스의 메서드는 모두 가지고 있음)
* void add(int index, Object element)
    + 추가
* boolean addAll(int index, Collection c)
* Object get(int index)
* Object set(int index, Object element)
* Object remove(int index)
* int indexOf(Object o)
* int lastIndexOf(Object o)
* void sort(Comparator c)
* List subList(int fromindex, int todindex)
* Listiterator listIterator()
* Listiterator listIterator(int index)


Set 인터페이스 - 순서 X, 중복 X 
-----


* set 인터페이스의 메서드 =  Collection 인터페이스와 동일 
* 집합과 관련된 메서드(Collection에 변화가 있으면 true, 아니면 false 반환)
    + 합집합, 부분집합, 차집합, 교집합


Map 인터페이스 - 순서 X, 중복(키X, 값O)
-----

* HashMap
* TreeMap
* LinkedHashMap (순서가 있음)

* Object put(Object key, Object value)
* Object putAll(Map t)
* Object remove(Object key)
* boolean containsKey(Object key)
* boolean containsValue(Object value)
* Set entrySet()
    + 모든 key-value 쌍을 set으로 반환
* Set keySet()
    + 모든 Key 반환
* Collection values()
    + 모든 value 객체 반환
    + 반환타입 Collection(순서,중복 상관없음)

