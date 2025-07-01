## Khái niệm
AOP (Aspect-Oriented Programming – Lập trình hướng khía cạnh) là một mô hình lập trình giúp tách biệt các logic phụ trợ (cross-cutting concerns) ra khỏi logic chính của chương trình

## Mục đích của AOP
Giúp xử lý những phần logic lặp đi lặp lại ở nhiều nơi (ví dụ: logging, exception, bảo mật, transaction,…) một cách tập trung, không làm bẩn code chính.

## Thành phần chính trong AOP
| Thành phần     | Vai trò                                                                                        |
| -------------- | ---------------------------------------------------------------------------------------------- |
| **Aspect**     | Lớp chứa logic AOP (như xử lý lỗi, log, bảo mật,...)                                           |
| **Advice**     | Đoạn code sẽ chạy trước/sau/xung quanh method chính                                            |
| **Join Point** | Điểm có thể “chen ngang” (method được gọi, exception được ném,...)                             |
| **Pointcut**   | Điều kiện để áp dụng Advice vào Join Point (ví dụ: match method có annotation `@LogExecution`) |
| **Weaving**    | Quá trình áp dụng Aspect vào code (diễn ra lúc runtime ở Spring AOP)                           |

## Spring hỗ trợ AOP thế nào?
- Spring AOP dùng kỹ thuật proxy runtime (JDK Proxy / CGLIB) để chèn logic AOP vào các method phù hợp.
- Không cần sửa method gốc
- Không ảnh hưởng đến các tầng khác
- Dễ bật/tắt, test, mở rộng

## Khi nào nên dùng AOP?
- Ghi log theo chuẩn
- Xử lý exception
- Audit, đo performance
- Quản lý transaction
- Kiểm tra quyền (@PreAuthorize, v.v.)
- Chuẩn hóa phản hồi API (response wrapper)

