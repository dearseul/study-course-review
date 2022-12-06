Iterator, ListIterator, Enumeration
-----

* 컬렉션에 저장된 데이터를 접근하는 데 사용되는 인터페이스 
* Enumeration 은 Iterator 의 구버전 
    + boolean hasMoreElements()
    + Object nextElement()
* ListIterator 는 Iterator의 접근성을 향상시킨 것(단방향 -> 양방향) 
* Iterator
    + 컬렉션에 저장된 요소들을 읽어오는 방법을 표준화한 것 
    + boolean hasNext() - 읽어 올 요소가 있는지 확인 
    + Object next()  - 다음 요소를 읽어온다. 
    + 컬렉션에 iterator()를 호출해서 iterator를 구현한 객체를 얻어서 사용 
    ```java
    List list = new ArrayList();
    Iterator it = list.iterator();

    while(it.hasNext()){
        System.out.println(it.next());
    }
    ``` 

    ```java
    class Ex11_1{
        public static void main(String[] args){
            ArrayList list = new ArrayList();

            // cf 
            // HashSet c = new HashSet();
            // 위 코드 보다 
            // Collection c = new TreeSet();
            // 위 코드가 더 좋음. 유연한 코드 

            list.add("1");
            list.add("2");
            list.add("3");
            list.add("4");
            list.add("5");

            Iterator it = list.iterator();

            while(it.hasNext()){
                Object obj = it.next();
                Systemout.println(obj);
            }

            // 반복문을 한번 더 돌리면 다음에 읽어올 요소가 없어서 it.hasNesxt() === false -> 돌지 않음
            // iterator는 다음의 읽어올 요소를 가리키는 변수? 가 있음 
            // 끝까지 돌면 더이상 읽어올게 없기 때문에 false 나옴 
            while(it.hasNext()){
                Object obj = it.next();
                Systemout.println(obj);
            }

            // 한번 더 쓸라면 iterator 를 다시 얻어와야 함. 
            it = list.iterator(); // 새로운 iterator객체를 얻는다. 

            while(it.hasNext()){
                Object obj = it.next();
                Systemout.println(obj);
            }

            // iterator없이 이렇게 쓸수 있음 
            // 그러나 list를 new HashSet();으로 바꾸면 
            // 아래 코드는 동작하지 않지만 
            // iterator 는  변경하지 않고 동작 가능 
            for(int i = 0; i< list.size(); i++){
                Object obj = list.get(i);
                System.out.println(obj);
            }
        }
    }
    ``` 

Map과 Iterator
-----

* Map에는 iterator()가 없다 
    + Set 과 List는 Collection의 자손 이지만 
    + Map은 Collection의 자손이 아님. 
    + iterator() 없음.
* keyset(), entrySet(), values()를 호출해야
    + ...set => 반환타입이 set => collection의 자손 
```java
Map map = new HashMap();
...
Itertator it = map.entryset().iterator();
// == 
// set eSet = map.entrySet();
// Iterator it = eSet.iterator();
```



Arrays - 배열을 다루기 편리한 메서드(statc)제공 
-----

* cf) 비슷한거 - Math. Objects. Collections.. 클래스 
1. 배열의 출력 - toString()
    + static String toString(boolean[] a) 
    + static String toString(Object[] a)
    + static String toString(int[] a)
    + ..... 

2. 배열의 복사 - copyOf(), copyOfRange()    
    ```java
    int[] arr = {0,1,2,3,4};
    int[] arr2 = Arrays.copyOf(arr, arr.length);
    // arr 배열에서 5개를 복사해서 새로 만듬 
    // arr2 = {0,1,2,3,4}
    int[] arr3 = Arrays.copyOf(arr, 7);
    // 넘치는 건 0 으로 채움 

    int[] arr4 = Arrays.copyOfrange(arr, 2, 4);
    // from 2(범위 들어감) to 4(안들어감)
    // arr4 = {2, 3}
    ```
3. 배열 채우기 - fill(), setAll()
    ```java
    int[] arr = new int[5];
    Arrays.fill(arr, 9);    // arr = [9,9,9,9,9,9]
    Arrays.setall(arr, (i) -> (int)(Math.random()*5)+1); 
    // setAll(array, 람다식)
    // 난수로 채움 
    // arr = [1, 5, 2, 1,1]
    ```

4. 배열의 정렬과 검색 - sort(), binarySearch()
    ```java
    int[] arr = {3,2,0,1,4};
    int idx = Arrays.binarySearch(arr,2);
    // arr 배열에서 2 가 어디 있는지 찾음 
    // idx = -5가 나옴 => 잘못된 결과
    // binarySearch는 정렬된 배열에만 가능하다. 

    Arrays.sort(arr);   // {0,1,2,3,4}
    int idx = Arrays.binarySearch(arr,2);   // idx = 2 
    ```
    
> 순차 검색과 이진 검색(탐색)
> 7 1 6 9 5 3 8 4 10 2  (순차적으로 찾으면 앞에서 부터 10 까지 찾아야함 (10개 요소면 평균 5.5 회 찾아야함)) 
> 1 2 3 4 5 6 7 8 9 10 (이진 검색은 반으로 잘라서 찾음/ 또 반으로 짤라서 찾음(10 개 요소면 평균 3,4 번 ) )
>  이진 검색은 빠르지만 정렬해야 함. 

5. 다차원 배열의 출력 - deepToString()
    ```java
    int[] arr = {0,1,2,3,4};
    int[][] arr2D = {{11,22},{21,22}};

    System.out.println(Arrays.deepToString(arr2D));
    ```

6. 다차원 배열의 비교 - deepEquals()
    ```java
    String[][] str2D = new String[][]{{"aaa","bbb"},{"AAA","BBB"}};
    String[][] str2D2 = new String[][]{{"aaa","bbb"},{"AAA","BBB"}};

    System.out.println(Arrays.deepEquals(str2D,str2D2)); 
    ```

7. 배열을 List로 변환 - asList(Object... a)
    + 가변 매개변수 
    ```java
    List list = Arrays.asList(new Integer[]{1,2,3,4,5});    // list = [1,2,3,4,5]
    List list = Arrays.asList{1,2,3,4,5};   // list = [1,2,3,4,5]
    list.add(6);    // UnsupportedOperationException 예외 발생 
                    // list는 읽기 전용 

    List list = new ArrayList(Arrays.asList(1,2,3,4,5));    // 새로운 ArrayList를 만듬 => 변경가능
    ```

8. 람다와 스트림 관련 - parallelXXX(), spliterator(), stream()
