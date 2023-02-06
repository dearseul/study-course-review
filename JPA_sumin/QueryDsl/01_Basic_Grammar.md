## 서브쿼리 9~21
### from절의 서브쿼리 한계
- JPA JPQL 서브쿼리의 한계점으로 from 절의 서브쿼리는 지원하지 않음.
### from절의 서브쿼리 해결방안
- 서브쿼리를 join으로 변경
- 애플리케이션에서 쿼리를 2번 분리해서 실행
- nativeSQL을 사용

## 상수, 문자 더하기
```java
List<String> result = queryFactory
        .select(member.username.concat("_").concat(member.age.stringValue()))
        .from(member)
        .where(member.username.eq("member1"))
        .fetch();
```
- member.age.stringValue() 부분이 중요한데, 문자가 아닌 다른 타입들은 stringValue()로 문자로 변환 가능함
- 이 방법은 ENUM을 처리할 때에도 자주 사용함