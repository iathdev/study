## Kỹ thuật Proxy Runtime là gì?
Proxy runtime (ủy quyền thời gian chạy) là kỹ thuật trong đó một “proxy object” (đối tượng trung gian) được tạo khi ứng dụng đang chạy, để chen ngang logic trước/sau/khi gọi đến method thật của một object gốc.

## Giải thích dễ hiểu
Ví dụ: bạn có class thật UserService:
```java
public class UserService {
    public void createUser() {
        System.out.println("Tạo user");
    }
}
```
→ Nếu bạn muốn log khi gọi createUser(), thay vì sửa trực tiếp, bạn tạo một proxy object như sau:
```java
public class UserServiceProxy extends UserService {
    @Override
    public void createUser() {
        System.out.println("Log: trước khi tạo user");
        super.createUser();
        System.out.println("Log: sau khi tạo user");
    }
}
```
Nhưng thay vì bạn tự viết thủ công, Spring AOP sẽ tự động tạo proxy đó vào thời gian chạy nhờ kỹ thuật "runtime proxy"

## Cơ chế trong spring
| Kỹ thuật              | Khi nào dùng?                     | Cơ chế                                  |
| --------------------- | --------------------------------- | --------------------------------------- |
| **JDK Dynamic Proxy** | Nếu object implement interface    | Dùng `java.lang.reflect.Proxy`          |
| **CGLIB Proxy**       | Nếu object **không có interface** | Dùng thư viện CGLIB để tạo subclass mới |

## Lợi ích của Proxy Runtime

- Không cần sửa code gốc (_non-invasive_)
- Tái sử dụng logic (ví dụ: logging, bảo mật, validation,...)
- Tách biệt concern (phù hợp với mô hình AOP, Decorator)
- Kết hợp dễ dàng với Spring IoC Container

## Hạn chế

- Khó debug hơn vì gọi thông qua proxy, không phải object gốc
- Không áp dụng được cho các method gọi nội bộ trong cùng class
- Có thể ảnh hưởng nhẹ đến hiệu năng do thêm lớp trung gian



