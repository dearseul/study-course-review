프로그램 오류
-----

* 컴파일 에러(compile-time error): 컴파일 할 때 발생하는 에러 
* 런타임 에러(runtime error): 실행 중 발생하는 에러
* 논리적 에러(logical error): 작성 의도와 다르게 동작 

> java의 런타임 에러
> * 에러(error) - 프로그램 코드에 의해서 수습될 수 없는 심각한 오류 
> * 예외(exception) - 프로그램 코드에 의해서 수습될 수 있는 다소 미약한 오류 

* 예외처리(exception handling)의 정의와 목적 
    - 정의 : 프로그램 실행 시 발생할 수 있는 예외의 발생에 대비한 코드를 작성하는 것 
    - 목적 : 프로그램의 비정상 종료를 막고, 정상적인 실행상태를 유지하는 것 

* Exception 과 RuntimeException
    - Exception 클래스들 - 사용자의 실수와 같은 외적인 요인에 의해 발생하는 예외 
    - RuntimeException 클래스들 - 프로그래머의 실수로 발생하는 예외 
>   Exception
>       - IOException
>       - ClassNotFoundException
>       - RuntimeException  
>           - ArithmethicException
>           - ClassCastException
>           - NullPointerException
>           - ...
>           - IndexOutOfBoundsException


예외 처리하기
-----

```java
class Ex8_1{
    public static void main(String[] args){
        System.out.println(1);
        try{
            System.out.println(2);
            System.out.println(3);
        }catch(Exception e){
            System.out.println(4);
        }
        System.out.println(5);
    }
}
// 결과: 1 2 3 5

class Ex8_2{
    public static void main(String[] args){
        System.out.println(1);
        try{
            System.out.println(2);
            System.out.println(0/0);
            System.out.println(3);
        }catch (ArithmeticException ae){
            System.out.println(4);
        }
        System.out.println(5);
    }
}
// 결과: 1 2 4 5 
```

printStackTrace() 와 getMessage()
-----

> printStackTrace()
>   - 예외 발생 당시의 호출스택(Call Stack)에 있었던 메서드의 정보와 예외 메세지를 화면에 출력한다. 
> getMessage()
>   - 발생한 예외클래스의 인스턴스에 저장된 메시지를 얻을 수 있다.

```java
class Ex8_3{
    public static void main(String[] args){
        System.out.println(1);
        System.out.println(2);
        try{
            System.out.println(3);
            System.out.println(0/0);
            System.out.println(4);
        }catch(ArighmeticException ae){
            ae.printStackTrace();
            System.out.println("예외메시지: " + ae.getMessage());
        }
        System.out.println(6);
    }
}
// 결과
// 1 2 3 
// java.lang.ArithmeticException : / by zero 
//  at Ex8_3.main(Ex8_3.java:8)             // (8번째줄)
// 예외메시지: by zero
// 6
```

멀티 catch 블럭
-----

* 내용이 같은 catch 블럭을 하나로 합친 것 
```java
try { 
    /// ... 
}catch (ExceptionA e ){
    e.printStackTrace();
}catch (ExceptionB e2) {
    e2.printStackTrace();
}

// --> 

try {
    // ... 
}catch(ExceptionA | ExceptionB e){
    e.printStackTrace();
}
```

* 주의 
```java
try { 
    // ... 
// } catch(ParentException | ChildException e) { // 부모 자식 관계 X => 컴파일 에러 
}catch (ParentException e){     // OK. 위의 라인과 의미상 동일
    e.printStackTrace();
}
```

```java
try { 
    // ... 
}catch (ExceptionA | ExceptionB e){
    e.methodA(); // 에러. ExceptionA에만 선언된 methodA()는 호출불가 
    // ExceptionA 와 ExceptionB 공통멤버만 사용 가능 
    if(e instanceof ExceptionA){
        ExceptionA e1 = (ExceptionA)e;
        e1.methodA();       // 체크해서 형변환 후 사용은 OK 
    }else{
        // ... 
    }
}
```

예외 발생시키기
-----

> 1. 연산자 new를 이용해서 발생시키려는 에외 클래스의 객체를 만든 다음
>   Exception e = new Exception("고의로 발생시켰음");
> 2. 키워드 throw를 이용해서 예외를 발생시킨다. 
>   throw e; 

```java
class Ex8_4{
    public static void main(String[] args){
        try {
            Exception e = new Exception("고의로 발생시켰음");
            throw e;    // 예외를 발생 시킴 
            // throw new Exception("고의로 발생시켰음");
        }catch(Exception e){
            System.out.prinln("에러 메시지: " + e.getMessage());
            e.printStackTrace();
        }
        System.out.println("프로그램이 정상 종료되었음");
    }
}
```

checked 예외, unchecked 예외
-----

* checked 예외 : 컴파일러가 예외 처리 여부를 체크(예외 처리 필수)   (Exception 클래스와 자손)
* unchecked 예외 : 컴파일러가 예외 처리 여부를 체크 안함(예외 처리 선택) (RuntimeExcepion 클래스와 자손)

```java
class Ex8_5{
    public static void main(String[] args){
        throw new Exception();  // 컴파일 에러 
        // checked 예외 - 예외 처리 필수 
    }
}

class Ex8_6{
    public static void main(String[] args){
        throw new RuntimeException();   // 컴파일 OK
        // unchecked 예외 - 예외 처리 선택 
    }
}
// 실행 = > 런타임 에러 
```









