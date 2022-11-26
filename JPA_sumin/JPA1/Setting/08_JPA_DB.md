## JPA와 DB 설정, 동작확인

### 쿼리 파라미터 로그 남기기
- 로그에 ``org.hibernate.type`` : SQL 실행 파라미터를 로그로 남김
```java
2022-11-24 21:18:01.011 DEBUG 11096 --- [           main] org.hibernate.SQL                        : 
    insert 
    into
        member
        (username, id) 
    values
        (?, ?)
2022-11-24 21:18:01.011 TRACE 11096 --- [           main] o.h.type.descriptor.sql.BasicBinder      : binding parameter [1] as [VARCHAR] - [memberA]
2022-11-24 21:18:01.011 TRACE 11096 --- [           main] o.h.type.descriptor.sql.BasicBinder      : binding parameter [2] as [BIGINT] - [1]
```
- 외부 라이브러리 사용
    - ``implementation 'com.github.gavlyukovskiy:p6spy-spring-boot-starter:1.5.6'`` build.gradle에 추가
    ```
    insert into member (username, id) values (?, ?)
    insert into member (username, id) values ('memberA', 1);
    ```
