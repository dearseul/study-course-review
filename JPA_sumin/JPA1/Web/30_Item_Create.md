# 웹 계층 개발

## 상품 목록

### Tip
- setter 사용 자제하기
```java
    @PostMapping("/items/new")
    public String create(BookForm form) {
        Book book = new Book();
        book.setName(form.getName());
        book.setPrice(form.getPrice());
        book.setStockQuantity(form.getStockQuantity());
        book.setAuthor(form.getAuthor());
        book.setIsbn(form.getIsbn());

        itemService.saveItem(book);
        return "redirect:/items";
    }
```
- 위 코드보다 createBook(String name, int price, ...) 등의 메서드를 만들어서 호출하는 게 더 좋은 설계방식
