## 주문 검색 기능
	crateQuery(“select o from Order o join.)..
	.setParameter(“status”, orderSearch.getOrderStatus())
	.setMaxResult(1000); 최대 1000건까지만 가능하게
	.getResult();

동적으로 쿼리를 만들기 까다로움

publc List<Order> findAllByCriteria(OrderSearch orderSearch) {
	CriteriaBuilider
}

쿼리를 만들지 않고 Query dsl로 처리함.
