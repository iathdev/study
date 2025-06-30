# Cơ bản về Web Security

## 1. Web Security là gì?

**Web Security** là việc bảo vệ ứng dụng web khỏi các mối đe dọa bảo mật, lỗ hổng và tấn công mạng.

### Mục tiêu:

- **Tính bí mật (Confidentiality)**: Không để lộ dữ liệu.
- **Tính toàn vẹn (Integrity)**: Dữ liệu không bị thay đổi trái phép.
- **Tính sẵn sàng (Availability)**: Hệ thống hoạt động ổn định.

---

## 2. Các hình thức tấn công phổ biến

### 2.1 SQL Injection (SQLi)

- Kẻ tấn công chèn mã SQL vào các trường đầu vào (form, URL...) để:
  - Lấy cắp dữ liệu.
  - Xóa, sửa hoặc thêm dữ liệu trái phép.

**Ví dụ**:

```sql
SELECT * FROM users WHERE username = '$input';
```

Nếu `$input = ' OR 1=1 --` ⇒ truy vấn sẽ trả về toàn bộ bảng `users`.

---

### 2.2 Cross-site Scripting (XSS)

- Kẻ tấn công chèn **JavaScript độc hại** vào trang web.
- Thường thông qua:
  - Ô tìm kiếm, comment, URL, form...
- Hậu quả:
  - Đánh cắp cookie.
  - Redirect đến trang độc hại.

---

### 2.3 Cross-site Request Forgery (CSRF)

- Lợi dụng phiên đăng nhập của người dùng để **gửi yêu cầu trái phép** đến server.
- Ví dụ: gửi yêu cầu đổi mật khẩu, chuyển tiền mà người dùng không biết.

**Biện pháp phòng tránh**:
- CSRF Token
- SameSite Cookie
- Kiểm tra Referer Header

---

### 2.4 File Upload Attack

- Tấn công thông qua việc upload file độc hại (shell, script…).
- Có thể bị chiếm quyền máy chủ nếu file được thực thi.

**Cần kiểm tra**:
- MIME type
- Đuôi file
- Nội dung
- Không cho phép thực thi file upload

---

### 2.5 Directory Traversal

- Truy cập file nằm **ngoài thư mục cho phép** bằng cách lợi dụng `../`.

**Ví dụ**:
```
/download?file=../../../etc/passwd
```

---

### 2.6 Brute-force Attack

- Tấn công bằng cách thử nhiều username/password đến khi đúng.

**Biện pháp bảo vệ**:
- Giới hạn số lần đăng nhập
- Captcha
- 2FA

---

### 2.7 Man-In-The-Middle (MITM)

- Nghe lén hoặc chỉnh sửa dữ liệu giữa client và server.

**Xảy ra khi**:
- Dùng HTTP (không mã hóa).
- Dùng Wi-Fi công cộng.

**Giải pháp**:
- Sử dụng HTTPS (TLS).

---

### 2.8 Denial of Service (DoS/DDoS)

- Gửi lượng lớn request để làm server quá tải, dẫn đến sập hệ thống.
- DDoS là dạng tấn công từ nhiều máy khác nhau.

**Chống bằng**:
- Rate limiting
- Firewall
- Cloud proxy (Cloudflare…)

---

## 3. Một số kỹ thuật phòng thủ cơ bản

- Validate & sanitize tất cả đầu vào (input).
- Sử dụng prepared statements khi thao tác DB.
- Bảo vệ form với CSRF token.
- Thiết lập quyền truy cập đúng (Authorization).
- Sử dụng HTTPS.
- Cập nhật bản vá bảo mật định kỳ.



