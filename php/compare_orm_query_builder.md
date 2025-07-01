# So sánh ORM và Query Builder trong PHP (Laravel)

## Tổng quan

| Tiêu chí                 | ORM (Eloquent)                                       | Query Builder (DB::table)                           |
| ------------------------ | ---------------------------------------------------- | --------------------------------------------------- |
| **Khái niệm**            | Là công cụ ánh xạ dữ liệu giữa bảng DB và object PHP | Là công cụ giúp xây dựng câu lệnh SQL động bằng PHP |
| **Phong cách lập trình** | Hướng đối tượng (OOP), thao tác qua model            | Thao tác trực tiếp bằng tên bảng                    |
| **Cú pháp**              | Ngắn gọn, thân thiện, giống code logic               | Linh hoạt, gần với SQL gốc                          |
| **Tự động hóa**          | Có sẵn: timestamps, relationships, events,...        | Không có, phải xử lý thủ công                       |
| **Query phức tạp**       | Khó viết hơn nếu quá nhiều join / subquery           | Viết rõ ràng và linh hoạt với join/subquery         |
| **Hiệu năng**            | Chậm hơn một chút với dữ liệu lớn/phức tạp           | Nhanh hơn vì không qua tầng ánh xạ                  |
| **Tính mở rộng**         | Hỗ trợ Relationship (hasOne, hasMany,...)            | Không hỗ trợ quan hệ, phải join thủ công            |
| **Testability**          | Dễ viết test unit với Model (fake, mock)             | Khó hơn nếu nhiều logic trộn lẫn                    |
| **Khi nên dùng**         | CRUD, logic đơn giản, quan hệ rõ ràng                | Báo cáo, thống kê, query phức tạp, data lớn         |
| **Ví dụ SELECT**         | `User::where('active', 1)->get()`                    | `DB::table('users')->where('active', 1)->get()`     |
| **Ví dụ JOIN**           | `User::with('posts')->get()`                         | `DB::table('users')->join(...)->get()`              |

## Khi nào nên dùng ORM (Eloquent)?

* Khi bạn làm việc CRUD nhanh, rõ ràng
* Có mối quan hệ rõ ràng giữa các bảng (1-1, 1-n, n-n)
* Dự án thiên về logic nghiệp vụ nhiều hơn là truy vấn dữ liệu nặng

## Khi nào nên dùng Query Builder?

* Cần tối ưu hiệu năng
* Dữ liệu lớn, truy vấn nhiều bảng
* Báo cáo, thống kê, phân trang custom
* Join/GroupBy phức tạp mà ORM khó diễn đạt

## Gợi ý kết hợp

* Dùng ORM cho phần nghiệp vụ logic
* Dùng Query Builder riêng cho phần **report, dashboard, export**, hoặc tạo lớp repository tùy biến
