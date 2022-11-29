# 웹 계층 개발

## 변경 감지와 병합(merge)

### 준영속 엔티티
```java
    @PostMapping("/items/{itemID}/edit")
    public String updateItem(@PathVariable String itemID, @ModelAttribute("form") BookForm form) {
        Book book = new Book();
        book.setIsbn(form.getIsbn());
        book.setPrice(form.getPrice());
        book.setName(form.getName());
        book.setStockQuantity(form.getStockQuantity());
        book.setId(form.getId());
        book.setAuthor(form.getAuthor());

        itemService.saveItem(book);
        return "redirect:/items";
    }
```
- 영속성 컨텍스트가 더는 관리하지 않는 엔티티 (위에서 Book 객체)
    - 이미 DB에 한번 저장되어서 식별자(id)가 존재함.
    - 임의로 만들어낸 엔티티도 기존 식별자를 가지고 있으면 준영속 엔티티라고 볼 수 있음.
    
### 준영속 엔티티를 수정하는 방법
- 변경 감지 기능 사용
- 병합(merge) 사용

### 변경 감지 기능 사용
```java
    @Transactional
    public void updateItem(Long id, Book param) {
        Item findItem = itemRepository.findOne(id); // 영속성
        findItem.setPrice(param.getPrice());
        findItem.setName(param.getName());
        findItem.setStockQuantity(param.getStockQuantity());
    }
```
- 영속성 컨텍스트에서 엔티티를 다시 조회한 후에 데이터를 수정하는 방법
- 트랜잭션 안에서 엔티티를 다시 조회, 변경할 값 선택 -> 트랜잭션 커밋 시점에 변경 감지(dirty checking)이
동작해서 데이터베이스에 update Sql 실행
  
### 병합 사용
- 준영속 상태의 엔티티를 영속 상태로 변경할 때 사용

> 주의
> 변경 감지 기능을 사용하면 원하는 속성만 선택해서 변경할 수 있지만, 병합을 사용하면 모든 속성이 변경됨. 
> 병합시 값이 없으면 ``null``로 업데이트 할 위험도 있음.

### 가장 좋은 방법
- 엔티티를 변경할 때에는 항상 변경 감지를 사용하기
    - 컨트롤러에서 어설프게 엔티티 생성 자제
    - 트랜잭션이 있는 서비스 계층에 식별자와 변경할 데이터를 명확히 전달
    - 트랜잭션이 있는 서비스 계층에서 영속 상태의 엔티티를 조회하고, 엔티티의 데이터를 직접 변경
    - 트랜잭션 커밋 시점에 변경 감지가 실행 됨
    ```java
        @PostMapping("/items/{itemID}/edit")
        public String updateItem(@PathVariable Long itemID, @ModelAttribute("form") BookForm form) {
        //        Book book = new Book();
        //        book.setIsbn(form.getIsbn());
        //        book.setPrice(form.getPrice());
        //        book.setName(form.getName());
        //        book.setStockQuantity(form.getStockQuantity());
        //        book.setId(form.getId());
        //        book.setAuthor(form.getAuthor());
        //
        //        itemService.saveItem(book);

        itemService.updateItem(itemID, form.getName(), form.getPrice(), form.getStockQuantity());
        return "redirect:/items";
    }
    ```
    
