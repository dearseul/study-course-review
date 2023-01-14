HashMap 과 Hashtable - 순서X, 중복(키X,값O)
-----

* Map 인터페이스를 구현. 데이터를 키와 값의 쌍으로 저장.
* HashMap(동기화X)은 HashTable(동기화O)의 신 버젼

* HashMap
    + Map인터 페이스를 구현한 대표적인 컬렉션 클래스
    + 순서를 유지하려면 LinkedHashMap 클래스를 사용하면 된다.

* TreeMap( TreeSet 과 같은 특성)
    + 범위 검색과 정렬에 유리한 컬랙션 클래스
    + HashMap 보다 데이터 추가, 삭제에 시간이 더 걸림

HashMap의 키(key)와 값(value)
-----

* 해싱(hashing) 기법으로 데이터를 저장. 데이터가 많아도 검색이 빠르다.
* Map인터페이스를 구현. 데이터를 키와 값의 쌍으로 저장 
    + key - 컬렉션 내의 key 중에서 유일해야 한다.
    + value - key와 달리 데이터의 중복을 허용한다.
```java
public class HashMap extends AbstractMap implements Map, Cloneable, Serializable{
    transient Entry[] table; // 배열  (Entry - key, value값 한쌍 )
    ...
    static class Entry implements Map.Entry{
        final Object key;
        Object value;
        ...
    }
}
```

해싱(hashing)
-----

* 해시함수(hash function)로 해시테이블(hash table)에 데이터를 저장, 검색 
* ex) key(ex 주민번호) 넣으면 hash code(저장 위치) 
* 해시 테이블은 배열과 링크드 리스트가 조합된 형태 
* 배열의 장점인 접근성 & 링크드 리스트의 장점인 변경에 유리 
* HashTable, HashMap, HashSet 

* Hash Table에서 저장된 데이터를 가져오는 과정
    1. 키로 해시함수를 호출해서 해시코드를 얻는다. 
    2. 해시코드(해시함수의 반환값)에 대응하는 링크드리스트를 배열에서 찾는다.
    3. 링크드리스트에서 키와 일치하는 데이터를 찾는다. 
    + 해시함수는 같은 키에 대해 항상 같은 해시코드를 반환해야 한다.
    + 서로 다른 키일지라도 같은 값의 해쉬코드를 반환할 수도 있다. 


HashMap - 주요 메서드
-----

* HashMap() - 생성자
* HashMap(int initialCapacity) - (해쉬테이블 = 배열 + 링크드리스트) 초기용량
* HashMap(int initialCapacity, float loadFactor)
* HashMap(Map m)
* Object put(Object key, Object value)
* void putAll(Map m)
* Object remove(Object key)
* Object replace(Object key, Object value) - 변경 
* boolean replace(Object key, Object oldValue, Object newValue)
* Set entrySet() -  entry(키 - 값) 쌍 
* Set keySet() - key 값들만 
* Collection values() - value값들만
* Object get(Object key) - key 에 대한 value 
* Object getOrDefault(Object key, Object defaultValue) - key 없을때 defaultvalue 반환
* boolean containsKey(Object key)
* boolean containsValue(Object value)

* int size()
* boolean isEmpty()
* void clear()
* Object clone()

```java
class Ex11_6{
    public static void main(String[] args){
        HashMap map = new HashMap();
        map.put("김자바", new Integer(90));
        map.put("김자바", new Integer(100));
        map.put("이자바", new Integer(100));
        map.put("강자바", new Integer(80));
        map.put("안자바", new Integer(90));

        Set set = map.entrySet();
        Iterator it = set.iterator();

        while(it.hasNex()){
            Map.Entry e = (Map.Entry)it.next();
            // Map interface
            // Entry interface
            // Entry - Map interface 내부의 interface 
            System.out.println("이름: " + e.getKey() + ", 점수 : " + e.getValue());
        }
        // 이름: 안자바, 점수: 90
        // 이름: 김자바, 점수: 100
        // 이름: 강자바, 점수: 80
        // 이름: 이자바, 점수: 100

        set = map.keySet();
        System.out.println("참가자 명단 : " + set);
        // 참가자 명단 : [안자바, 김자바, 강자바, 이자바]   

        Collection values = map.values();
        it = values.iterator();

        int total = 0; 

        while(it.hasNex()){
            int i = (int)it.nex();
            total += i;
        }

        System.out.println("총점: " + total);
        System.out.println("평균: " + (float)total/set.size());
        System.out.println("최고점수: " + Collections.max(values));
        System.out.println("최저점수: " + Collections.min(values));


    }
}
```

```java
class Ex11_7{
    public static void main(String[] args){
        String[] data = {"A","K","A","K","D","K","A","K","K","K","Z","D"};

        HashMap map = new HashMap();

        for(int i = 0; i < data.length; i++){
            if(map.containsKey(datap[i])){
                int value = (int)map.get(data[i]);
                map.put(data[i], value + 1);
            }else{
                map.put(data[i], 1);
            }
        }

        Iterator it = map.entrySet().iterator();

        while(it.hasNex()){
            Map.Entry entry = (Map.Entry)it.next();
            int value = (int)entry.getValue();
            System.out.println(entry.getKey() + ":" + printBar('#', value) + " " + value);
        }
        /*
        A : ### 3
        D : ## 2
        Z : # 1
        K : ###### 6 
        */
    }
}



 



