## 동적 쿼리
동적 쿼리를 해결하는 두가지 방식
1. BooleanBuilder 
2. Where 다중 파라미터 사용

### BooleanBuilder
     @Test
    public void 동적쿼리_BooleanBuilder() throws Exception {
        String usernameParam = "member1";
        Integer ageParam = 10;

        List<Member> result = searchMember1(usernameParam, ageParam);
            Assertions.assertThat(result.size()).isEqualTo(1);
        }

        private List<Member> searchMember1(String usernameCond, Integer ageCond) {
            BooleanBuilder builder = new BooleanBuilder();
            if (usernameCond != null) {
                builder.and(member.username.eq(usernameCond));
            }
            if (ageCond != null) {
                builder.and(member.age.eq(ageCond));
            }
        return queryFactory
            .selectFrom(member)
            .where(builder)
            .fetch();
    }

### Where 다중 파라미터 사용

    @Test
    public void 동적쿼리_WhereParam() throws Exception { 
        String usernameParam = "member1";
        Integer ageParam = 10;
        List<Member> result = searchMember2(usernameParam, ageParam);
        Assertions.assertThat(result.size()).isEqualTo(1);
    }

        private List<Member> searchMember2(String usernameCond, Integer ageCond) {
            return queryFactory
                .selectFrom(member)
                .where(usernameEq(usernameCond), ageEq(ageCond))
                .fetch();
        }

        private BooleanExpression usernameEq(String usernameCond) {
            return usernameCond != null ? member.username.eq(usernameCond) : null;
        }

        private BooleanExpression ageEq(Integer ageCond) {
            return ageCond != null ? member.age.eq(ageCond) : null;
        }

- where 조건에 null 값은 무시된다.
- 메서드를 다른 쿼리에서도 재활용 할 수 있다.
- 쿼리 자체의 가독성이 높아진다.