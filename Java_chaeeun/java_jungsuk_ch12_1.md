지네릭스(Generics)란
-----

* 컴파일 시 타입을 체크해 주는 기능
```java
// Tv객체만 저장할 수 있는 ArrayList를 생성
ArrayList<Tv> tvList = new ArrayList<Tv>();

tvList.add(new Tv()); 
tvList.add(new Audio());    // 컴파일 에러. Tv 외에 다른 타입 저장 불가 
// 지네릭스 덕분에 타입체크가 강화됨. 
```

* cf) 
```java
ArrayList list = new ArrayList();
// ArrayList<Object> list = new ArrayList<Object>();    

list.add(10);
list.add(20);
list.add("30");

Integer i = (Integer)list.get(2); //  컴파일 OK 
                     // String 
// ===> 실행 시 에러. ClasCastException (형변환에러)    
// 컴파일러의 한계 
``` 

* 객체의 타입 안정성을 높이고 형변환의 번거로움을 줄여줌 

> 지네릭스의 장점
> 1. 타입 안정성을 제공한다.
> 2. 타입체크와 형변환을 생략할 수 있으므로 코드가 간결해진다. 



* Exception
    + IOException
    + ClassNotFoundException
    + ...
    + RuntimeException ( 프로그래머 실수로 발생에러 )
        - ArithmeticException
        - ClassCastException
        - NullPointerException
        - ...
        - IndexOutOfBoundsException

> Runtime 에러보다는 Compile time 에러가 나야 수정 가능. 
> Runtime 에러를 Compile time 에러로 끌고 올 수 있는 방법 고민 
> * 지네릭스 - ClassCastException을 Compile time으로 끌고 올 수 있다. 
> ex) NullPointerException
> String str = null; 보다는 
> String str = ""; 가 좋은 코드. 
> str.length() => null 일 때는 NullPointerException
>              => "" 일 떄는 0. 
> Object[] objArr = null; 보다는
> Object[] objArr = new Object[0]; // 길이가 0인 배열 
> 또는 Object[] objArr = {}
> => NullPointerException 방지 
