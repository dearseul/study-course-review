## 상품 수정
- 병합(merge)가 아닌 변경감지를 이용하라.

    
    @Getmaping("items/{itemId}/edit")
    public String uodateItemForm(@PathVariable("itemId") Long itemId, Model model) {
        Book item = (Book) itemService.findOne(itemId);

        BookForm form = new BookFrom();
        form.set.....

        model.addAtrribute("form", form);
        return ""; 
    }

- command 두번 누르면 multiline select



    @PostMapping("items/{itemId}/edit")
    public String updateItem(@ModelAttribute("form") BookForm form, @PathVariable String itemId){

    new Book에 form set
    itemService.saveItem(book);
    }

- form의 Id값을 조심하라. 조작해서 넘어올수도 있다.
- 권한 체크 로직이 꼭 있어야 한다.

- saveItem을 하면 => Id값이 있으면 새로 등록 아니면 em.merge
- merge는 실무에서는 거의 쓰지 않음.