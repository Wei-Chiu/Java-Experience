# service 实现类

```java
package com.kuang.service;

import com.kuang.dao.BookMapper;
import com.kuang.pojo.Books;
import java.util.List;

public class BookServiceImpl implements BookService {

    // 调用dao层的操作，设置一个set接口，方便Spring管理
    // 这里如果报错 找不到匹配的 bean，但是 spring 又可以跳转，则检查 web.xml 设置的 dispatcherServlet 读取的配置文件是否有包含 BookMapper 注册的那个 bean
    private BookMapper bookMapper;

    public void setBookMapper(BookMapper bookMapper) {
        this.bookMapper = bookMapper;
    }
    
    public int addBook(Books book) {
        return bookMapper.addBook(book);
    }
    
    public int deleteBookById(int id) {
        return bookMapper.deleteBookById(id);
    }
    
    public int updateBook(Books books) {
        return bookMapper.updateBook(books);
    }
    
    public Books queryBookById(int id) {
        return bookMapper.queryBookById(id);
    }
    
    public List<Books> queryAllBook() {
        return bookMapper.queryAllBook();
    }
}
```

