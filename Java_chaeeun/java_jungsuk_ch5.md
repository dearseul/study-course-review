배열
=======

배열이란?
-------

* 배열은 같은 타입의 여러 변수를 하나의 묶음으로 다루는 것 

배열읜 선언과 생성
------

* 배열의 선언 - 배열을 다루기 위한 참조변수 선언
    + 타입[] 변수이름; 
    ```java
    int[] score;
    String[] name;
    
    int[] score;            // 배열을 선언(참조변수)
    score = new int[5];     // 배열을 생성(실제 저장공간을 생성)

    int[] score = new int[5];    // 배열의 선언과 생성 
    ```
    + 타입 변수이름[];
    ```java
    int score[];
    String name[];
    // C언어 
    ```

* 배열의 길이 
    + 배열이름.length 
    + 배열은 한번 생성하면 그 길이를 바꿀 수 없다. 
        
* 배열의 초기화
    ```java
    int[] score = {50, 60, 70, 80, 90};
    ```

* 배열의 출력 
    ```java 
    int[] iArr = {30,40,50,60,70};
    System.out.println(iArr); // [I@13145b] 와 같은 형식으 ㅣ문자열 출력 
    // char[] chArr = {'a','b','c'} -> abcd 출력

    // [30,40,50,60,70] 출력
    System.out.println(Arrays.toString(iArr)); 
    ```

* 배열의 활용

    + 최댓값과 최솟값
    ```java
    class Ex5_1{
        public static void main(String[] args){
            int[] score = {79, 88, 33, 100, 55, 95};

            int max = score[0];
            int min = score[0];

            for(int i=0; i < score.length; i++){
                if(score[i] > max){
                    max = score[i];
                }else if(score[i] < min>){
                    min = score[i];
                }
            }
            System.out.println("max: " + max);
            System.out.println("min: " + min);
        }
    }
    ```

    + 섞기(shuffle)
    ```java
    import java.util.Arrays;

    class Ex5_2{
        public static void main(String[] args){
            int[] numArr = {0,1,2,3,4,5,6,7,8,9};
            System.out.println(Arrays.toString(numArr));

            for(int i=0; i < 100; i++){
                int n = (int)(Math.random()*10);
                int tmp = numArr[0];
                numArr[0] = numArr[n];
                numArr[n] = tmp;
            }
            System.out.println(Arrays.toString(numArr));
        }
    }
    ```

* String 배열의 선언과 생성

    + String[] name = new String[3];

* 커맨드 라인을 통해 입력받기
    ```java
    class Ex5_3{
        public static void main(String[] args){
            System.out.println("매개변수의 갯수:" + args.length);
            for(int i = 0; i < args.length; i++){
                System.out.println("args[" + i + "]=\"" + args[i] + "\"");
            }
        }
    }
    ```
    ```
    // 결과
    C\jdk1.8\work\ch5>java Ex5_3 abc 123 "Hello World"
    매개변수의 갯수:3
    args[0] = "abc"
    args[1] = "123"
    args[2] = "Hello World"

    C\jdk1.8\work\ch5>java Ex5_3
    매개변수의 갯수:0
    ```

* 2차원 배열 

    + 테이블 형태의 데이터를 저장하기 위한 배열 
    ```java
    int[][] score = new int[5][3];
    ```
    + 2차원 배열의 초기화
    ```java
    int[][] arr = {
        {100,100,100},
        {20,20,20},
        {40,40,50}
    };
    ```

* String 클래스 
    + String 클래스는 char[] 와 메서드(기능)을 결합한 것 
        > String 클래스 = char[] + 메서드(기능)
    + String 클래스는 내용을 변경할 수 없다.(read only)
        ```
        String a = "a";
        String b = "b";
        a = a + b; 
        // 문자열 "a" 가 "ab"로 바뀌는게 아니고, 참조 변수 a가 새로운 문자열 ab를 가리킨다.
        ```
    + String클래스의 주요 메서드 
        - char charAt(int index) // 문자열에서 해당위치(index)에 있는 문자를 반환한다.
            ``` 
            String str = "ABCDEF";
            char ch = str.charAt(3);    // 'D'를 ch에 저장 
            ```
        - int length()  // 문자열의 길이 
        - String substring(int from, int to)    // 해당 범위 문자열 반환
            ```
            str.substring(1,4); // "123" 출력
            ```
        - boolean equals(Object obj)    // 문자열의 내용이 같은지 
        - char[] toCharArry()       //문자열을 문자배열(charp[])로 변환해서 반환한다.

* Arrays로 배열 다루기
    
    + 배열의 비교와 출력 - equals(), toString()
    ```java
    int[] arr = {0,1,2,3,4};
    int[][] arr2D = {{12,34},{56,78}};

    System.out.println(Arrays.toString(arr));
    System.out.println(Arrays.deepToString(arr2D));

    String[][] str2D = new String[][]{{"aaa","bbb"},{"ccc","ddd"}};
    String[][] str2D2 = new String[][]{{"aaa","bbb"},{"ccc","ddd"}};

    System.out.println(Arrays.equals(str2D,str2D2));    // false
    System.out.println(Arrays.deepEquals(str2D,str2D2));    // true
    ```

    + 배열의 복사 - copyOf(), copyOfRange()
    ```java
    int[] arr = {0,1,2,3,4};
    int[] arr2 = Arrays.copyOf(arr, arr.length); // 배열 요소 5개 그대로 복사 arr2 = [0,1,2,3,4]
    int[] arr3 = Arrays.copyOf(arr, 3); // arr3 = [0,1,2]
    int[] arr4 = Arrays.copyOf(arr,7);  // arr4 = [0,1,2,3,4,0,0]
    int[] arr5 = Arrays.copyOfRange(arr,2,3);   // arr5 = [2,3]
    int[] arr6 = Arrays.copyOfRange(arr,0,7);   // arr6 = [0,1,2,3,4,0,0]
    ```

    + 배열의 정렬 - sort()
    ```java
    int[] arr = {3,2,9,4,5};
    Arrays.sort(arr);   // 배열 arr 정렬 {2,3,4,5,9}
    ```

    