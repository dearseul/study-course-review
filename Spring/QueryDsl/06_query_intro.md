## 쿼리 사용법
### from 절의 서브쿼리 한계
JPA JPQL 서브쿼리의 한계점으로 from 절의 서브쿼리(인라인 뷰)는 지원하지 않는다. 당연히 Querydsl 도 지원하지 않는다. 하이버네이트 구현체를 사용하면 select 절의 서브쿼리는 지원한다. Querydsl도 하이버네이트 구현체를 사용하면 select 절의 서브쿼리를 지원한다.
### from 절의 서브쿼리 해결방안
1. 서브쿼리를 join으로 변경한다. (가능한 상황도 있고, 불가능한 상황도 있다.)
2. 애플리케이션에서 쿼리를 2번 분리해서 실행한다.
3. nativeSQL을 사용한다.
### case문
    List<String> result = queryFactory
                .select(new CaseBuilder()
                    .when(member.age.between(0, 20)).then("0~20살") 
                    .when(member.age.between(21, 30)).then("21~30살") .otherwise("기타"))
                .from(member)
                .fetch();
### 복잡한 case문
    NumberExpression<Integer> rankPath = new CaseBuilder()
        .when(member.age.between(0, 20)).then(2)
        .when(member.age.between(21, 30)).then(1)
        .otherwise(3);
        
    List<Tuple> result = queryFactory
        .select(member.username, member.age, rankPath)
        .from(member)
        .orderBy(rankPath.desc())
        .fetch();
    
    for (Tuple tuple : result) {
            String username = tuple.get(member.username);
            Integer age = tuple.get(member.age);
            Integer rank = tuple.get(rankPath);
        
            System.out.println("username = " + username + " age = " + age + " rank = " + rank); 
        }

Querydsl은 자바 코드로 작성하기 때문에 rankPath 처럼 복잡한 조건을 변수로 선언해서 select 절, orderBy 절에서 함께 사용할 수 있다.