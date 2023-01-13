TreeSet - 범위 탐색, 정렬
-----

* 이진 탐색 트리(binary search tree)로 구현. 범위 탐색과 정렬에 유리 
* 이진 트리는 모든 노드가 최대 2개의 하위 노드를 갖음 
* 각 요소(node)가 나무(tree) 형태로 연결(LinkedList의 변형) 
```java
class TreeNode{
    TreeNode left; // 왼쪽 자식 노드
    Object element; // 저장할 객체
    TreeNode right; // 오른쪽 자식 노드 
}

// cf) LinkedList
class Node{
    Node next; // 다음 요소의 주소를 저장
    Object obj; // 데이터를 저장 
}
```

이진 탐색 트리(binary search tree)
-----

* 부모보다 작은 값은 왼쪽, 큰 값은 오른쪽에 저장 
* 데이터가 많아질 수록 추가, 삭제에 시간이 더 걸림(비교 횟수 증가) (단점)
    + 요소를 하나 저장할 때마다 root부터 부모보다 큰지 작은지 계속 비교해야함 

TreeSet - 데이터 저장과정 boolean add(Object o)
-----

* boolean add(Object o)
    + add 메서드가 1. equals(), 2. hashCode()  호출
    + 중복 X, 같은게 있으면 저장 실패(false) 


TreeSet - 주요 생성자와 메서드
-----

* collection 인터페이스에 있는 메서드
    +  add(), size(), remove(), isEmpty(), iterator()
* TreeSet() - 기본 생성자
* TreeSet(Collection c) - 주어진 컬렉션을 저장하는 TreeSet을 생성
* TreeSet(Comparator comp) - 주어진 정렬기준으로 정렬하는 TreeSet 을 생성
    + 없으면 저장하는 객체의 Comparable (기본 비교 기준) 이용 
* Object first() - 제일 작은거 
* Object last() - 제일 큰거
* Object ceiling(Object o) - 저장 된 객체 중 같거나 큰 값  (제일 가까운 값의 객체)
* Object floor(Object o) - 같거나 작은 값  (제일 가까운 값의 객체)
* Object higher(Object o) - 저장 된 객체 중 큰 거  (제일 가까운 값의 객체)
* Object lower(Object o )- 작은 거 (제일 가까운 값의 객체)
* SortedSet subSet(Object fromElement, Object toElement) - 범위 검색의 결과 반환 
* SortedSet headSet(Object toElement) - 지정된 객체보다 작은 값의 객체들을 반환
* SortedSet tailSet(Objct fromElement) - 지정된 객체보다 큰 값의 객체들을 반환 

```java 
class Ex11_1{
    public static void main(String[] args){
        Set set = new TreeSet(); //범위 검색과 정렬. 정렬 필요 없음 
        // Set set = new HashSet();    // 정렬 필요 

        for(int i = 0; set.size() < 6; i++){
            int num = (int)(Math.random() * 45) + 1;
            set.add(num);
            // set.add(new Test()) // 에러. 비교 기준이 없어서
            // => testComp 추가 
        }

        Set set2 = new TreeSet(new TestComp()); // 정렬 기준 제공 
        set2.add(new Test()); // OK 

        System.out.println(set);
        // 9 16 20 29 31 35 
        // 정렬 따로 안해도 정렬 되어서 나옴. 

    }
}

class Test{}    

class TestComp implements Comparator{
    @Override
    public int compareTo(Object o1, Object o2){
        return 1;
    }
}

```

```java
 class Ex11_2{
    public static void main(String[] args){
        TreeSet set = new TreeSet();
        int[] score = [80,95,50, 35, 45, 65, 10,100];

        for(int i = 0; i < score.length; i++){
            set.add(new Integer(score[i]));
        }

        System.out.println("50보다 작은값: " + set.headSet(new Integer(50)));
        // 10 35 45
        System.out.println("50보다 큰값: " + set.tailSet(new Integer(50)));
        // 50 65 80 95 100
        System.out.println("40 ㄱ허 80 사이 값: " + set.subSet(new Integer(50)));
        // 45 50 65
    }
 }
 ```


TreeSet - 범위 검색 subSet(), headSet(), tailSet()
-----

* 50 보다 큰값 ( 50의 왼쪽가지 아래 이외의 값들 )
* 50 보다 작은값 ( 50 왼쪽 가지 아래)
* => 범위 검색에 유리 


> * 트리 순회(tree traversal)
>   + 이진 트리의 모든 노드를 한번씩 읽는 것을 트리 순회라고 한다.
>   + preorder(전위순회) - 부모를 먼저 읽고 자식들을 읽음
>   + postorder(후위 순회) - 부모를 나중에 읽음 
>   + inorder(중위 순회) - 왼 - 부모 - 오른 (부모를 사이에 둠 )
>   + levelorder(레벨 순회) - 층 순서 대로 
> * 중위 순회 
>    + 중위 순회 하면 오름차순으로 정렬된다. 
>  * TreeSet이 정렬에 유리하다.  


