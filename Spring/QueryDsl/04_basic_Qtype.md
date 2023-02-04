## 기본 Q타입 활용
### Q클래스 인스턴스를 사용하는 2가지 방법
    QMember qMember = new QMember("m"); //별칭 직접 지정
    QMember qMember = QMember.member; //기본 인스턴스 사용
### 기본 인스턴스를 static import와 함께 사용
    import static study.querydsl.entity.QMember.*;
    
    @Test
    public void startQuerydsl3() {
        //member1을 찾아라.
        Member findMember = queryFactory
            .select(member)
            .from(member)
            .where(member.username.eq("member1"))
            .fetchOne();
        
        assertThat(findMember.getUsername()).isEqualTo("member1");
        }
다음 설정을 추가하면 실행되는 JPQL을 볼 수 있다.

        spring.jpa.properties.hibernate.use_sql_comments: true
 