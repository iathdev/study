| Tiêu chí                | Cookie                                              | Session                                          |
| ----------------------- | --------------------------------------------------- | ------------------------------------------------ |
| Vị trí lưu trữ          | Trên trình duyệt (client)                           | Trên máy chủ (server)                            |
| Dung lượng              | Giới hạn (\~4KB)                                    | Không giới hạn nhiều (tùy cấu hình server)       |
| Thời gian sống          | Có thể đặt lâu dài                                  | Thường hết khi đóng trình duyệt hoặc hết timeout |
| Tự động gửi mỗi request | Có – trình duyệt gửi cùng mỗi HTTP request          | Không – chỉ khi ứng dụng sử dụng                 |
| Bảo mật                 | Dễ bị xem hoặc sửa nếu không mã hóa                 | Bảo mật hơn, dữ liệu lưu trên server             |
| Người dùng xem được?    | Có – có thể xem qua DevTools > Application > Cookie | Không – user không thể thấy nội dung session     |
| Dễ bị giả mạo           | Dễ, nếu không bảo vệ kỹ                             | Ít rủi ro hơn nếu dùng session ID an toàn        |
| Tốc độ xử lý            | Nhanh (vì lưu client)                               | Có thể chậm hơn nếu lưu file/database            |


Khi nào dùng Cookie và Session

| Trường hợp sử dụng                            | Nên dùng |
| --------------------------------------------- | -------- |
| Lưu thông tin đăng nhập lâu dài (remember me) | Cookie   |
| Xác thực tạm thời (login phiên hiện tại)      | Session  |
| Lưu cài đặt người dùng (ngôn ngữ, theme)      | Cookie   |
| Lưu dữ liệu nhạy cảm (user\_id, role...)      | Session  |
| Lưu giỏ hàng tạm thời trong 1 phiên           | Session  |

