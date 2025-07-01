# 📌 JSON Web Token (JWT) Là Gì?

**JWT (JSON Web Token)** là một chuẩn mở (RFC 7519) dùng để truyền tải thông tin giữa các bên một cách an toàn dưới dạng đối tượng JSON. JWT thường được sử dụng trong cơ chế **xác thực (authentication)** và **phân quyền (authorization)** giữa client và server.

---

## 🧱 Cấu Trúc Của JWT

JWT bao gồm 3 phần, phân cách bằng dấu `.`:

```
<Header>.<Payload>.<Signature> 
```

### 1. Header
Chứa metadata mô tả token:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```
- alg: thuật toán dùng để ký (ví dụ: HS256, RS256)
- typ: loại token, luôn là JWT

### 2. Payload
Chứa dữ liệu (claims):

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true,
  "iat": 1516239022
}
```
Có 3 loại claims:

- Registered claims: các trường chuẩn như iss, exp, sub, iat, ...
- Public claims: định nghĩa chung, nên đăng ký tránh xung đột.
- Private claims: định nghĩa riêng giữa các bên.

### 3. Signature
Dùng để xác minh token chưa bị chỉnh sửa. Cách tạo:

Với thuật toán HMAC-SHA256 (HS256):
```plaintext
Signature = HMACSHA256(
  base64UrlEncode(header) + "." + base64UrlEncode(payload),
  secret
)
```
Với thuật toán RSA (RS256):
```plaintext
Signature = SignWithPrivateKey(
  base64UrlEncode(header) + "." + base64UrlEncode(payload),
  privateKey
)
```
### ✨ Ưu Điểm Của JWT
- Tự chứa: Không cần lưu thông tin session phía server.
- Gọn nhẹ: Truyền dễ dàng qua header hoặc URL.
- Bảo mật: Nếu được ký đúng cách, tránh bị giả mạo.
- Không trạng thái (stateless): Phù hợp hệ thống phân tán, microservices.

### ⚠️ Nhược Điểm
- Không thể thu hồi token dễ dàng (trừ khi dùng blacklist).
- Dung lượng lớn hơn session ID truyền thống.
- Không nên chứa thông tin nhạy cảm (vì chỉ ký chứ không mã hóa).

### 🔐 Các Thuật Toán JWT Thường Dùng
| Thuật toán | Loại  | Mô tả                             |
| ---------- | ----- | --------------------------------- |
| HS256      | HMAC  | Ký với shared secret              |
| RS256      | RSA   | Private key ký, public key verify |
| ES256      | ECDSA | Ký bằng elliptic curve            |



