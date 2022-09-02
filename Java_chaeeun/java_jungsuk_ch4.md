조건문
=========

+ if문 
+ switch문 
    - 처리해야하는 경우의 수가 많을 때 유용한 조건문 
    
        switch(조건식){
            case 값1: 
                // 
                break;
            case 값2: 
                //
                break;
            default:
                //
        }
    
    - switch문의 제약조건
        1. switch문의 조건식 결과는 정수 또는 문자열이어야 한다.
        2. case문의 값은 정수, 상수(문자 포함), 문자열만 가능하며, 중복되지 않아야 한다. 

+ 임의의 정수 만들기 

    0.0 <= Math.random() < 1.0

반복문
=======

+ for 문 
    반복 횟수를 알 때 적합 

+ while 문 
    반복 횟수를 모를 때 적합 

+ do-while 문
    최소한 한 번 이상 반복 - 사용자 입력받을 때 유용 


break문 
--------

+ 자신이 포함된 하나의 반복문을 벗어난다. 

    public static void main(String[] args){
        int sum = 0;
        int i = 0;

        while(true){
            if(sum > 100)
                break;
            ++i;
            sum += i;
        }
    }


continue문
------

+ 자신이 포함된 반복문의 끝으로 이동  (다음 반복으로 넘어감)
    전체 반복 중에서 특정 조건 시 반복을 건너뛸 때 유용


이름붙은 반복문
------

+ 반복문에 이름을 붙여서 하나 이상의 반복문ㅇ르 벗어날 수 있다. 

    public static void main(String[] args){
        // for문에 Loop1이란 이름을 붙였다.
        Loop1: for(int i=2; i<=9; i++){
            for(int j=1; j<=9; j++){
                if(j==5)
                    break Loop1;
                    // break; => 하나의 반복문만 벗어남
                System.out.println(i + "*" + j + "=" + i+j);
            }   // end of for i
            System.out.println();
        }// end of Loop1 
    }