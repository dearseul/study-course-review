메서드에 예외 선언하기
-----

* 예외를 처리하는 방법
    1. try - catch 문 ( 직접 처리 )
    2. 예외 선언하기 ( 예외 떠넘기기 )
    
* 메서드가 호출 시 발생가능한 예외를 호출한 쪽에 알리는 것 
> 예외를 발생시키는 throw와 예외를 메서드에 선언할 때 쓰이는 throws를 잘 구별하자. 

```java
void method() throws Exception1, Exception2, ... ExceptionN {
    // ... 
}

void method() throws Exception {    // 모든 종류의 예외가 발생 가능 
    // 
}

static void startInstall() throws SpaceException, MemoryException { // 필수 예외만 적는 것이 정석 ,, (checked exception)
    if(!enoughSpace())
        throw new SpaceException("설치할 공간이 부족합니다.");
    if(!enoughMemory())
        throw new MemoryException("메모리가 부족합니다.");
}
```

사용자 정의 예외 만들기 
-----

* 우리가 직접 예외 클래스를 정의할 수 있다.
* 조상은 Exception과 RuntimeException 중에서 선택 
```java
class MyException extends Exception {
    MyException(String msg) {
        super(msg); // 조상인 Exception 클래스의 생성자 호출 
    }
}
```

예외 던지기 (exception re-throwing)
-----

* 예외를 처리한 후에 다시 예외를 발생시키는 것 
* 호출한 메서드와 호출된 메서드 양쪽 모두에서 예외처리 하는 것 

```java 
class Ex8_6{
    public static void main(String[] args){
        try{
            method1();
        }catch (Exception e){
            System.out.println("main메서드에서 예외가 처리되었습니다.");
        }
    }
    
    static void method1() throws Exception {
        try{
            throw new Exception();
        }catch(Exception e ){
            System.out.println("method1에서 예외가 처리되었습니다.");
            throw e;
        }
    }
}

// 결과 
// main메서드에서 예외가 처리되었습니다.
// method1에서 예외가 처리되었습니다.
```

연결된 에외 
-----

* 한 예외가 다른 에외를 발생시킬 수 있다. 
* 예외 A가 예외 B를 발생시키면, A는 B의 원인 예외(cause exception) 
> Throwable initCause(Throwable cause) 지정한 에외를 원인 예외로 등록
> Thrwoable getCause()

```java
void install() throws InstallException {    // InstallEXception throws 
    try{
        startInstall();     // spaceException 발생
        copyFiles();
    } catch(SpaceException e){
        InstallException ie = new InstallException("설치중예외발생");
        ie.initCause(e); // InstallException의 원인 에외를 SpaceException으로 지정  
        throw ie;   // InstallException을 발생시킨다. 
    }
}
```

* 이유1. 여러 예외를 하나로 묶어서 다루기 위해서
```java
try{
    install();
}catch(SpaceException e){
    e.printStackTrace();
}catch(MemoryException e){
    e.printStackTrace();
}catch(Exception e ){
    e.printStackTrace();
}

// ---- >
//  예외 연결시키기 
void istall() throws InstallException {
    try{
        startInstall();
        copyFiles();
    }catch(SpaceException e){
        InstallException ie = new InstallException("설치중예외발생");
        ie.initCause(e);
        throw ie;
    }catch(MemoryException me ){
        InstallException ie = new InstallException("설치중예외발생");
        ie.initCause(me);
        throw ie;

    }
}
// => catch블럭 줄이기 
try {
    install();
}catch(InstallException e){
    e.printStackTrace();
}catch(Exception e){
    e.printStackTrace();
}
```

* 이유2: checked예외를 unchecked예외로 변경하려 할때 (필수처리 예외를 선택처리 예외로)
```java
class SpaceException extends Exception{
    SpaceException(String msg){
        super(msg);
    }
}
static void startInstall() throws SpaceException, MemoryException {
    // SpaceException - ( 필수 처리 예외 )
    if(!enoughSpace())
        throw new SpaceException("설치공간부족")  ;
    if(!enoughMemory())
        throw new MemoryException("메모리부족");
}

// => memoryexception을 선택 처리 예외로 바꿈 
static void startInstall() throws SpaceException {  //SpaceException 만 선언
    // => RuntimeException(선택처리예외) 을 발생시킨다음에 그 안에 던짐 
    if(!enoughSpace())
        throw new SpaceException("설치할 공간이 부족");
    if(!enoughMemory())
        throw new RuntimeException(new MemoryException("메모리부족"))
}
```


