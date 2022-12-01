스택과 큐의 활용
------

* 스택의 활용 예
    + 수식계산, 수식괄호검사, 워드프로세서의 undo/redo
    + 웹브라우저의 뒤로/앞으로 
* 큐의 활용 예
    + 최근사용문서, 인쇄작업 대기목록, 버퍼(buffer)

```java

public class Ex11_1{
    public static void main(String[] args){
        Stack st = new Stack();
        String expression = "((3+5)*8-2)";

        System.out.println(expression);

        try{
            for(int i = 0; i < expression.length(); i++){
                char ch = expression.charAt(i);

                if(ch=='('){
                    st.push(ch + "");
                }else if(ch == ')'){
                    st.pop();
                }
            }

            if(st.isEmpty()){
                System.out.println("괄호가 일치합니다.");
            }else{
                System.out.println("괄호가 일치하지 않습니다.");
            }
        }catch (EmptyStackException e){
            System.out.println("괄호가 일치하지 않습니다.");
        }
    }
}
```

```java
clas Ex11_2{
    static Queue q = new LinkedList();  
    static final int MAX_SIZE = 5; // Queue에 최대 5개 까지만 저장되도록 한다.

    public static void main(String[] args){
        System.out.prinln("help - 도움말을 보여줍니다.");

        while(true){
            System.out.println(">>");
            try{
                // 화면으로부터 라인단위로 입력받는다. 
                Scanner s = new Scanner(System.in);
                String input = s.nextLine().trim();

                if("".equals(input)) continue;

                if(input.equalsIgnoreCase("q")){
                    System.exit(0);
                }else if(input.equalsIgnoreCase("help")){
                    System.out.println("help - 도움말을 보여줍니다.");
                    System.out.println("q or Q - 프로그램 종료.");
                    System.out.pritnln("history - 최근에 입력한 명령어 " + MAX_SIZE + "개 보여줌 ");
                }else if(input.equalsIgnoreCae("history")){
                    save(intput);   // 입력받은 명령어를 저장하고, 

                    // LinkedList의 내용을 보여준다. 
                    LinkedList list = (LinkeList)q;

                    final int SIZE = list.size();
                    for(int i = 0; i < SIZE; i++){
                        System.out.println((i+1) + "." + list.get(i)); 
                    }
                }else{
                    save(input);
                    System.out.pritnln(input);
                }
            }catch(Exception e){
                System.out.pritnln("입력오류입니다.");
            }
        }   // while 끝
    }// main() 끝

    public static void save(String input){
        // queue에 저장 
        if(!"".equals(input)){
            q.offer(input);
        }

        // queue의 최대크기를 넘으면 제일 처음 입력된 것을 삭제한다. 
        if(q.size() > MAX_SIZE)
            q.remove();
            // == q.poll();
    }
}
``` 


