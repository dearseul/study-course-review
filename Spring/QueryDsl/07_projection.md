## 프로젝션과 결과 반환 - 기본
### 프로젝션과 결과 반환 - 기본
- 프로젝션: select 대상 지정

#### 프로젝션 대상이 하나

    List<String> result = queryFactory
        .select(member.username)
        .from(member)
        .fetch()

- 프로젝션 대상이 하나면 타입을 명확하게 지정할 수 있음 
- 프로젝션 대상이 둘 이상이면 튜플이나 DTO로 조회


### 튜플 조회
 프로젝션 대상이 둘 이상일 때 사용
>com.querydsl.core.Tuple

    List<Tuple> result = queryFactory
        .select(member.username, member.age)
        .from(member)
        .fetch();

        for (Tuple tuple : result) {
            String username = tuple.get(member.username);
            Integer age = tuple.get(member.age);

            System.out.println("username=" + username);
            System.out.println("age=" + age);
        }

### 프로젝션과 결과 반환 - DTO 조회 순수 JPA에서 DTO 조회
- 순수 JPA에서 DTO를 조회할 때는 new 명령어를 사용해야함 
- DTO의 package이름을 다 적어줘야해서 지저분함 
- 생성자 방식만 지원함

### Querydsl 빈 생성(Bean population) 
결과를 DTO 반환할 때 사용
#### 다음 3가지 방법 지원
  
- 프로퍼티 접근 
- 필드 직접 접근 
- 성자 사용