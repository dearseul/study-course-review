## 수정, 삭제 벌크 연산
### 쿼리 한번으로 대량 데이터 수정
    long count = queryFactory
            .update(member)
            .set(member.username, "비회원")
            .where(member.age.lt(28))
            .excute();
### 기존 숫자에 1더하기
    long count = queryFactory
            .update(member)
            .set(member.age, member.age.add(1))
            .execute();

>곱하기: multiply(x)
        
    long count = queryFactory
            .delete(member)
            .where(member.age.gt(18))
            .execute();

>  주위: JPAL배치와 마찬가지로, 영속석 컨텍스트에 있는 엔티티를 무시하고 실행되기 떄문에 배치 쿼리를 실행하고 나면 영속성 컨텍스트를 초기화 하는 것이 안전하다.

## SQL function 호출하기
SQL function은 JPA와 같이 Dialect에 등록된 내용만 호출할 수 있다.

member -> M으로 변경하는 replace 함수 사용

    String result = queryFactory
            .select(Expressions.stringTemplete("function('replace', {0}, {1},
            {2}", member.username, "member", "M"))
                .from(member)
                .fetchFirst();

### 소문자로 변경해서 비교해라
    .select(member.username)
    .from(member)
    .where(member.username.eq(Expressions.stringTemplete("function('lower', {0})", member.username)))

### lower 같은 ansi 표준 함수들은 querydsl 상당부분 내장하고 있다. 따라서 다음과 같이 처리해도 결과는 같다
    .where(member.username.eq(member.username.lower()))


