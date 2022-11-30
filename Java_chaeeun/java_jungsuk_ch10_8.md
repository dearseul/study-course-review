스택과 큐(Stack & Queue)
-----

* 스택(Stack): LIFO구조. 마지막에 저장된 것을 제일 먼저 꺼내게 된다. 
    + 저장(push), 추출(pop)
    + 배열로 구현하는게 적합
* 큐(Queue) : FIFO 구조. 제일 먼저 저장한 것을 제일 먼저 꺼내게 된다. 
    + 저장(offer), 추출(poll) 
    + linked list로 구현하는게 적합 


스택과 큐(Stack & Queue)의 메서드
-----

***** Stack 
* Stack st = new Stack();
* boolean empty() - Stack이 비어있는지 알려준다. 
* Object pop()  - 삭제
* Object push(Object item) - 추가
* Object peek() - 맨 위에 저장된 객체를 반환 (pop과 달리 꺼내지는 않음)
* int search(Object o) - Stack에서 주어진 객체(o)를 찾아서 위치 반환 (배열과 달리 인덱스는 1부터 시작)

***** Queue 
* boolean offer(Object o) - 추가 (예외 발생 X)
* Object pol()   - 삭제 (예외 발생 X, null 반환)
* Object remove() - 삭제 (예외 발생)
* Object peek() - 삭제없이 읽어온다 
* boolean add(Object o) - 추가(예외 발생) 
* Object element() (예외 발생)

> 자바에서 Queue는 인터페이스.  Queue 구현한 클래스 사용 
> ex) LinkedList 
> Queue q = new LinkedList(); 
> q.offer("a");

```java
Stack st = new Stack();
Queue q = new LinkedList();

st.push("0");
st.push("1");
st.push("2");

q.offer("0");
q.offer("1");
q.offer("2");

while(!st.empty()){
    System.out.println(st.pop());
}
// 2 1 0 
while(!q.isEmpty()){
    System.out.println(q.poll());
}
// 0 1 2
```