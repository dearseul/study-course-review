## 회원 목록 조회
    List<Member> members = memberService.findMember();
    model.addAtrribute("meber", members);

객체를 직접 쓰는지, entity를 변환해서 쓰는지?
- 결국에는 실무에서는 entity는 화면과 달라야함. 변환이 필요
- Entity는 최소로 유지. dependency는 최소로 유지

### Api를 만들때는, 절대 Entity를 외부(front)로 반환하면 절대 X!
