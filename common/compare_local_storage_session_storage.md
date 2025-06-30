| Tiêu chí             | Local Storage                                    | Session Storage                                      |
| -------------------- | ------------------------------------------------ | ---------------------------------------------------- |
| Vị trí lưu trữ       | Trình duyệt (client-side)                        | Trình duyệt (client-side)                            |
| Thời gian sống       | Tồn tại **vĩnh viễn** (cho đến khi xóa thủ công) | Chỉ tồn tại **trong tab hiện tại**                   |
| Khi reload trang     | Vẫn còn                                          | Vẫn còn                                              |
| Khi đóng tab         | Vẫn còn                                          | **Mất** khi tab/browser đóng                         |
| Khi mở tab mới       | Dữ liệu **được chia sẻ**                         | Dữ liệu **không chia sẻ**, tab nào lưu tab đó        |
| Dung lượng tối đa    | Khoảng 5–10MB (tùy trình duyệt)                  | Tương tự (\~5MB), nhưng ít được dùng cho dữ liệu lớn |
| Truy cập từ JS       | Có (`window.localStorage`)                       | Có (`window.sessionStorage`)                         |
| Gửi kèm HTTP Request | Không                                            | Không                                                |
| Bảo mật              | Không mã hóa, dễ đọc nếu truy cập máy            | Giống localStorage                                   |

Khi nào nên dùng?

| Tình huống                                          | Dùng gì?        |
| --------------------------------------------------- | --------------- |
| Lưu dữ liệu **dài hạn** (theme, token, ngôn ngữ)    | Local Storage   |
| Lưu tạm dữ liệu form/giỏ hàng trong **một tab**     | Session Storage |
| Lưu trạng thái trong bước đăng ký (multi-step form) | Session Storage |
| Lưu dữ liệu không nhạy cảm, cần chia sẻ giữa tab    | Local Storage   |
