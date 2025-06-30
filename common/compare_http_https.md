So sánh HTTP và HTTPS

| Tiêu chí         | HTTP                                        | HTTPS                                          |
| ---------------- | ------------------------------------------- | ---------------------------------------------- |
| Viết tắt         | HyperText Transfer Protocol                 | HyperText Transfer Protocol Secure             |
| Cổng mặc định    | 80                                          | 443                                            |
| Bảo mật          | Không có mã hóa – dữ liệu truyền ở dạng thô | Dữ liệu được mã hóa (SSL/TLS)                  |
| Tính riêng tư    | Không bảo vệ thông tin người dùng           | Bảo vệ nội dung khỏi bị nghe lén hoặc thay đổi |
| Chứng chỉ        | Không yêu cầu                               | Cần chứng chỉ SSL/TLS                          |
| URL bắt đầu bằng | `http://`                                   | `https://`                                     |
| SEO & uy tín     | Không được đánh giá cao                     | Được ưu tiên hơn trên Google                   |
| Hiệu năng        | Nhanh hơn một chút (do không mã hóa)        | Hơi chậm hơn, nhưng có thể tăng tốc với HTTP/2 |
| Dễ bị tấn công   | Dễ bị sniffing, MITM                        | Khó bị tấn công, vì dữ liệu đã được mã hóa     |


# SSL/TLS là gì?

## 1. SSL (Secure Sockets Layer)

- Là **tiền thân** của TLS, được phát triển bởi Netscape từ giữa những năm 1990.
- Có các phiên bản: SSL 1.0 (bị huỷ), SSL 2.0, SSL 3.0.
- **Đã lỗi thời** và **không còn được sử dụng** vì có nhiều lỗ hổng bảo mật.

---

## 2. TLS (Transport Layer Security)

- Là **phiên bản kế nhiệm của SSL**.
- Ra mắt lần đầu với TLS 1.0 → TLS 1.1 → TLS 1.2 → hiện nay là **TLS 1.3**.
- TLS là giao thức **được sử dụng trong HTTPS** (ví dụ: trình duyệt ↔ website).

---

## 3. SSL/TLS dùng làm gì?

- **Mã hóa dữ liệu truyền đi** giữa client và server (trình duyệt ↔ website).
- **Ngăn chặn**:
  - Đọc lén (eavesdropping)
  - Giả mạo (spoofing)
  - Tấn công trung gian (MITM – Man In The Middle)

---

## 4. Ví dụ thực tế

Khi bạn truy cập vào một website:

1. Trình duyệt yêu cầu **kết nối bảo mật TLS**.
2. Server gửi về **chứng chỉ số (SSL certificate)** để xác minh.
3. Hai bên trao đổi **khóa mã hóa (handshake)**.
4. Sau khi kết nối được thiết lập, **dữ liệu truyền đi sẽ được mã hóa hoàn toàn**.

---

## 5. So sánh SSL vs TLS

| Tiêu chí             | SSL                      | TLS                       |
|----------------------|--------------------------|---------------------------|
| Trạng thái           | Cũ, không còn dùng       | Hiện đại, đang được dùng |
| Phiên bản cuối       | SSL 3.0                  | TLS 1.3                   |
| Bảo mật              | Yếu, dễ bị tấn công      | Mạnh, cải tiến nhiều      |
| Hiệu năng            | Kém hơn                  | Tốt hơn, handshake nhanh |
| Hỗ trợ trong HTTPS   | Không nên dùng           | Chuẩn mặc định hiện nay  |

---

## 6. Kết luận

- **SSL/TLS là công nghệ cốt lõi bảo vệ internet hiện đại.**
- Tất cả các website nên sử dụng **HTTPS với TLS** để bảo vệ người dùng.
- Nếu bạn thấy ổ khóa 🔒 trên trình duyệt → nghĩa là **TLS đang hoạt động**.

