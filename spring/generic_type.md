# Tổng quan về Generic trong Java

## Generic là gì?

Generic là một tính năng trong Java giúp viết code tổng quát (generic), có thể tái sử dụng với nhiều kiểu dữ liệu khác nhau mà vẫn đảm bảo an toàn kiểu (type safety).

## Vì sao cần dùng Generic?

Không dùng generic:

```java
List list = new ArrayList();
list.add("Hello");
list.add(123);  // Không báo lỗi lúc compile
```

Dùng generic:

```java
List<String> list = new ArrayList<>();
list.add("Hello");
list.add(123);  // Lỗi lúc compile
```

Ưu điểm:

* Phát hiện lỗi kiểu ngay khi biên dịch
* Không cần ép kiểu khi truy xuất phần tử
* Dễ đọc, dễ bảo trì hơn

## Cách sử dụng Generic

### 1. Generic với class

```java
public class Box<T> {
    private T value;
    public void set(T value) { this.value = value; }
    public T get() { return value; }
}

// Sử dụng:
Box<String> box = new Box<>();
box.set("Hello");
System.out.println(box.get());
```

### 2. Generic với method

```java
public class Util {
    public static <T> void print(T input) {
        System.out.println(input);
    }
}

// Gọi method
Util.print("Xin chào");
Util.print(123);
```

### 3. Generic với interface

```java
public interface Repository<T> {
    T findById(int id);
}
```

### 4. Ký hiệu thường dùng

| Ký hiệu  | Ý nghĩa                              |
| -------- | ------------------------------------ |
| `T`      | Type (kiểu bất kỳ)                   |
| `E`      | Element (thường dùng với Collection) |
| `K`, `V` | Key, Value (Map)                     |
| `?`      | Wildcard (bất kỳ kiểu nào)           |

## Bounded Type (Giới hạn kiểu)

```java
public class NumericBox<T extends Number> {
    public void printDouble(T value) {
        System.out.println(value.doubleValue());
    }
}
```

> Chỉ cho phép T là `Number` hoặc subclass của `Number` (Integer, Float,...)

## Wildcard: `?`

```java
public void printList(List<?> list) {
    for (Object item : list) {
        System.out.println(item);
    }
}
```

> Dùng khi không cần biết chính xác kiểu nhưng vẫn muốn thao tác đọc dữ liệu.

## Lưu ý khi dùng Generic

| Hạn chế                                                                                                  |
| -------------------------------------------------------------------------------------------------------- |
| Không thể tạo object kiểu generic trực tiếp: `new T()` ❌                                                 |
| Không thể dùng generic với kiểu nguyên thủy (`int`, `char`) — phải dùng wrapper (`Integer`, `Character`) |
| Không thể kiểm tra kiểu bằng `instanceof T`                                                              |

## Ví dụ thực tế

```java
public class Response<T> {
    private T data;
    private String status;

    public Response(T data, String status) {
        this.data = data;
        this.status = status;
    }

    public T getData() { return data; }
}

// Sử dụng:
Response<String> res = new Response<>("OK", "success");
```
