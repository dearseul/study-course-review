## Query Dsl 검증과 설정
- Gradle IntelliJ 사용법 
- Gradle Tasks build clean 
- Gradle Tasks other compileQuerydsl

#### Gradle 콘솔 사용법
- ./gradlew clean compileQuerydsl

#### Q 타입 생성 확인
build generated querydsl
study.querydsl.entity.QHello.java 파일이 생성되어 있어야 함

> 참고: Q타입은 컴파일 시점에 자동 생성되므로 버전관리(GIT)에 포함하지 않는 것이 좋다. 
> 앞서 설정에서 생성 위치를 gradle build 폴더 아래 생성되도록 했기 때문에 이 부분도 자연스럽게 해결된다. (대부분 gradle build 폴더를 git에 포함하지 않는다.)

## 라이브러리 살펴보기
- gradle 의존관계 보기 
- ./gradlew dependencies --configuration compileClasspath
#### Querydsl 라이브러리 살펴보기
- querydsl-apt: Querydsl 관련 코드 생성 기능 제공 querydsl-jpa: querydsl 라이브러리
#### 스프링 부트 라이브러리 살펴보기
- spring-boot-starter-web spring-boot-starter-tomcat: 톰캣 (웹서버) spring-webmvc: 스프링 웹 MVC
- spring-boot-starter-data-jpa spring-boot-starter-aop