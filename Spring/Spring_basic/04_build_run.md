## 4차시 빌드하고 실행하기

## Build
    ./해당프로젝트폴더 gradlew build
    cd build/libs
    java -jar hello-spring-0.0.1-SNAPSHOT.jar
    실행확인

tip
>port강제종료
> ```
> lsof -i :포트번호
> lsof -i :8080
> COMMAND   PID   USER FD TYPE  DEVICE SIZE/OFF NODE NAME
> java 15530 seulgi 58u IPv6 0xe6 0t0 TCP *:http-alt (LISTEN)
> 
> kill -9 PID
> kill -9 15530
> ```
