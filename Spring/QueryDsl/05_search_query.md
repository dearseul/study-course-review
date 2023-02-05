## 검색 조건 쿼리
### 결과 조회
   - fetch() : 리스트 조회, 데이터 없으면 빈 리스트 반환 
   - fetchOne() : 단 건 조회
     - 결과가 없으면 : null 
     - 결과가 둘 이상이면 : com.querydsl.core.NonUniqueResultException 
   - fetchFirst() : limit(1).fetchOne()
   - fetchResults() : 페이징 정보 포함, total count 쿼리 추가 실행 
   - fetchCount() : count 쿼리로 변경해서 count 수 조회
### 정렬
- desc() , asc() : 일반 정렬
- nullsLast() , nullsFirst() : null 데이터 순서 부여
### 페이징
#### 조회 건수 제한
    @Test
    public void paging1() {
        List<Member> result = queryFactory
            .selectFrom(member)
            .orderBy(member.username.desc()) .offset(1) //0부터 시작(zero index) .limit(2) //최대 2건 조회
            .fetch();
        assertThat(result.size()).isEqualTo(2);
    }

주의: count 쿼리가 실행되니 성능상 주의!
> 참고: 실무에서 페이징 쿼리를 작성할 때, 데이터를 조회하는 쿼리는 여러 테이블을 조인해야 하지만, count 쿼리는 조인이 필요 없는 경우도 있다. 그런데 이렇게 자동화된 count 쿼리는 원본 쿼리와 같이 모두 조인을 해버리기 때문에 성능이 안나올 수 있다. count 쿼리에 조인이 필요없는 성능 최적화가 필요하다면, count 전용 쿼리를 별도로 작성해야 한다.