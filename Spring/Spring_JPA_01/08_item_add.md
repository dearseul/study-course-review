## 상품 추가

    @Getmapping("items/new")
    public String createForm(Model model) {
        model.attribute("form", new Bookform());
        return "페이지";
    }
    
    @PostMapping("/items/new")
    public String create(BookForm form) {
        Book book = new Book();
        여러 속성 넣어주기
        
        itemService.saveItem(book)
        return "redirect:/";
    }

- setter는 쓰지 않도록 하자.
