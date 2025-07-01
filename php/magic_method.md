# Magic Method trong PHP

## Magic method là gì?

Magic method là các phương thức đặc biệt trong PHP, có tên bắt đầu bằng hai dấu gạch dưới `__`. Chúng được PHP tự động gọi trong những tình huống nhất định như khởi tạo object, gọi thuộc tính không tồn tại, gọi hàm không tồn tại, ép kiểu object sang chuỗi, v.v.

## Danh sách các magic method phổ biến

| Tên method                          | Khi nào được gọi                  | Mục đích / Ý nghĩa               | Thường dùng |
| ----------------------------------- | --------------------------------- | -------------------------------- | ----------- |
| `__construct()`                     | Khi tạo object                    | Hàm khởi tạo                     | Có          |
| `__destruct()`                      | Khi object bị hủy                 | Dọn dẹp, đóng file, log          | Có          |
| `__get($name)`                      | Truy cập thuộc tính không tồn tại | Getter động                      | Có          |
| `__set($name, $value)`              | Gán cho thuộc tính không tồn tại  | Setter động                      | Có          |
| `__isset($name)`                    | Dùng `isset()` với thuộc tính ảo  | Kiểm tra tồn tại                 | Có thể      |
| `__unset($name)`                    | Dùng `unset()` với thuộc tính ảo  | Xóa thuộc tính                   | Có thể      |
| `__call($name, $args)`              | Gọi method không tồn tại          | Method động                      | Có          |
| `__callStatic($name, $args)`        | Gọi static method không tồn tại   | Static method động               | Có          |
| `__toString()`                      | Khi object bị ép sang chuỗi       | Hiển thị object                  | Có          |
| `__invoke()`                        | Khi object được gọi như hàm       | Cho phép callable object         | Có thể      |
| `__clone()`                         | Khi clone object                  | Tùy chỉnh clone                  | Có thể      |
| `__debugInfo()`                     | Khi `var_dump()` object           | Tùy chỉnh thông tin debug        | Có thể      |
| `__sleep()`                         | Trước khi serialize               | Xác định các thuộc tính được lưu | Ít          |
| `__wakeup()`                        | Khi unserialize object            | Phục hồi trạng thái              | Ít          |
| `__serialize()` / `__unserialize()` | PHP 7.4+                          | Thay thế `__sleep` / `__wakeup`  | Ít          |

## Ví dụ sử dụng

### `__get()` và `__set()`

```php
class User {
    private $data = [];

    public function __get($name) {
        return $this->data[$name] ?? null;
    }

    public function __set($name, $value) {
        $this->data[$name] = $value;
    }
}

$user = new User();
$user->name = 'Minh';
echo $user->name; // Minh
```

### `__call()`

```php
class Dynamic {
    public function __call($name, $args) {
        return "Gọi method $name với " . count($args) . " tham số";
    }
}

$obj = new Dynamic();
echo $obj->run(1, 2); // Gọi method run với 2 tham số
```

### `__toString()`

```php
class Book {
    public function __toString() {
        return "Đây là một cuốn sách";
    }
}

echo new Book(); // Đây là một cuốn sách
```

### `__construct()` và `__destruct()`

```php
class Loggable {
    public function __construct() {
        echo "Khởi tạo...\n";
    }

    public function __destruct() {
        echo "Kết thúc...\n";
    }
}

$obj = new Loggable();
```

## Tóm tắt magic method nên nhớ

| Method                           | Mục đích                     |
| -------------------------------- | ---------------------------- |
| `__construct()` / `__destruct()` | Tạo và hủy object            |
| `__get()` / `__set()`            | Truy cập/gán thuộc tính động |
| `__call()` / `__callStatic()`    | Gọi method động              |
| `__toString()`                   | In object ra chuỗi           |
| `__debugInfo()`                  | Tùy chỉnh var\_dump          |

## Ghi chú

* Nên dùng magic method có mục đích rõ ràng, tránh lạm dụng.
* Chỉ nên dùng khi cần xử lý dynamic logic, ví dụ: class DTO, dynamic property, dynamic service...
