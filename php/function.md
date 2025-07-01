# Các hàm quan trọng trong PHP

## 1. Hàm thao tác chuỗi

| Hàm                              | Mô tả                           |
| -------------------------------- | ------------------------------- |
| `strlen()`                       | Độ dài chuỗi                    |
| `strpos()`                       | Tìm vị trí chuỗi con            |
| `substr()`                       | Cắt chuỗi                       |
| `str_replace()`                  | Thay thế chuỗi con              |
| `trim()` / `ltrim()` / `rtrim()` | Xóa khoảng trắng                |
| `explode()`                      | Chuyển chuỗi thành mảng         |
| `implode()`                      | Ghép mảng thành chuỗi           |
| `sprintf()` / `printf()`         | Định dạng chuỗi                 |
| `strtolower()` / `strtoupper()`  | Chuyển chuỗi về thường / in hoa |

## 2. Hàm thao tác mảng

| Hàm                  | Mô tả                                        |
| -------------------- | -------------------------------------------- |
| `count()`            | Đếm phần tử trong mảng                       |
| `array_merge()`      | Gộp 2 mảng                                   |
| `array_diff()`       | Lấy phần tử khác nhau giữa mảng              |
| `array_intersect()`  | Lấy phần tử chung                            |
| `array_filter()`     | Lọc mảng theo điều kiện                      |
| `array_map()`        | Biến đổi từng phần tử                        |
| `array_reduce()`     | Gộp mảng thành 1 giá trị                     |
| `in_array()`         | Kiểm tra phần tử có trong mảng               |
| `array_key_exists()` | Kiểm tra key có tồn tại                      |
| `array_column()`     | Trích xuất giá trị theo key từ mảng đa chiều |

## 3. Hàm làm việc với file và thư mục

| Hàm                                          | Mô tả                      |
| -------------------------------------------- | -------------------------- |
| `file_get_contents()`                        | Đọc nội dung file          |
| `file_put_contents()`                        | Ghi dữ liệu vào file       |
| `fopen()`, `fread()`, `fwrite()`, `fclose()` | Mở/đọc/ghi/đóng file       |
| `unlink()`                                   | Xóa file                   |
| `is_file()`, `is_dir()`                      | Kiểm tra file hoặc thư mục |
| `scandir()`                                  | Đọc danh sách file/thư mục |

## 4. Hàm xử lý ngày giờ

| Hàm                        | Mô tả                            |
| -------------------------- | -------------------------------- |
| `date()`                   | Lấy ngày giờ hiện tại            |
| `strtotime()`              | Chuyển chuỗi thành timestamp     |
| `time()`                   | Lấy timestamp hiện tại           |
| `DateTime`, `DateInterval` | Class mạnh hơn để xử lý ngày giờ |
| `date_diff()`              | Tính khoảng cách giữa 2 ngày     |
| `date_format()`            | Định dạng ngày giờ               |

## 5. Hàm bảo mật và mã hóa

| Hàm                  | Mô tả                                   |
| -------------------- | --------------------------------------- |
| `password_hash()`    | Hash password (bcrypt)                  |
| `password_verify()`  | So sánh password                        |
| `md5()` / `sha1()`   | Băm dữ liệu (đã lỗi thời, dùng hạn chế) |
| `htmlspecialchars()` | Tránh XSS                               |
| `filter_var()`       | Validate dữ liệu đầu vào                |

## 6. Hàm xử lý HTTP / server

| Hàm                                        | Mô tả                    |
| ------------------------------------------ | ------------------------ |
| `header()`                                 | Gửi header HTTP          |
| `setcookie()` / `$_COOKIE`                 | Làm việc với cookie      |
| `session_start()` / `$_SESSION`            | Session                  |
| `$_GET`, `$_POST`, `$_REQUEST`, `$_SERVER` | Truy cập dữ liệu request |

## 7. Hàm kiểm tra và xử lý lỗi

| Hàm                                         | Mô tả                                 |
| ------------------------------------------- | ------------------------------------- |
| `isset()`                                   | Kiểm tra biến đã tồn tại và khác null |
| `empty()`                                   | Kiểm tra biến rỗng                    |
| `is_array()`, `is_string()`, `is_numeric()` | Kiểm tra kiểu                         |
| `error_log()`                               | Ghi log lỗi                           |
| `try { ... } catch (Exception $e)`          | Bắt lỗi                               |

## 8. Một số hàm tiện dụng khác

| Hàm                               | Mô tả              |
| --------------------------------- | ------------------ |
| `json_encode()` / `json_decode()` | Làm việc với JSON  |
| `sleep()`                         | Dừng chương trình  |
| `die()` / `exit()`                | Dừng script        |
| `uniqid()`                        | Sinh ID ngẫu nhiên |
| `var_dump()` / `print_r()`        | In debug           |

## 9. Các hàm chuyên dùng để gọi hàm khác (Dynamic Function Call)

| Hàm                      | Mô tả                                       |
| ------------------------ | ------------------------------------------- |
| `call_user_func()`       | Gọi hàm theo tên dưới dạng chuỗi            |
| `call_user_func_array()` | Gọi hàm với danh sách tham số là mảng       |
| `$funcName()`            | Gọi hàm trực tiếp thông qua biến tên        |
| `[$object, 'method']`    | Gọi phương thức của một object              |
| `function() {}`          | Định nghĩa hàm vô danh (anonymous function) |

## Gợi ý: Các nhóm nên học kỹ tùy vào mục đích

| Mục tiêu      | Nhóm nên ưu tiên                            |
| ------------- | ------------------------------------------- |
| API backend   | Chuỗi, mảng, file, HTTP, JSON               |
| Xử lý dữ liệu | Mảng, chuỗi, ngày giờ                       |
| Bảo mật       | Mã hóa, kiểm tra đầu vào                    |
| Tối ưu code   | `array_map`, `filter`, `reduce`, `DateTime` |
