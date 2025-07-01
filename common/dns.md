# Các bước phân giải một domain (DNS Resolution)

Khi truy cập một địa chỉ như `www.example.com`, trình duyệt cần phân giải domain này thành địa chỉ IP để gửi request. Quá trình đó gọi là DNS Resolution.

---

## 1. Kiểm tra cache cục bộ (Local DNS Cache)

- Hệ điều hành hoặc trình duyệt kiểm tra xem domain đã được phân giải trước đó chưa.
- Nếu có trong cache và TTL chưa hết hạn, sẽ sử dụng luôn kết quả IP từ cache.

---

## 2. Hỏi DNS Resolver (thường là của ISP)

- Nếu cache cục bộ không có, máy tính sẽ hỏi DNS Resolver (Recursive Resolver) do nhà mạng hoặc người dùng cấu hình.
- Resolver này sẽ thực hiện quá trình truy vấn DNS đệ quy.

---

## 3. Quá trình phân giải đệ quy

### a. Truy vấn Root DNS Server

- Resolver hỏi: “IP của www.example.com là gì?”
- Root Server trả lời: “Hãy hỏi TLD Server của .com”

### b. Truy vấn TLD Server (Top-Level Domain)

- Resolver hỏi TLD Server của `.com`: “IP của www.example.com?”
- Trả lời: “Hãy hỏi Name Server của domain `example.com`”

### c. Truy vấn Authoritative Name Server

- Resolver hỏi Name Server chính thức của `example.com`
- Nhận về IP thật của `www.example.com`

---

## 4. Trả kết quả về máy client

- Resolver gửi IP về máy của bạn
- IP được cache lại để sử dụng trong tương lai
- Trình duyệt dùng IP để mở kết nối tới máy chủ qua HTTP/HTTPS

---

## Tóm tắt quá trình phân giải DNS

```text
Trình duyệt
    ↓
Hệ điều hành (OS cache)
    ↓
DNS Resolver (ISP hoặc Google DNS)
    ↓
Root DNS Server
    ↓
TLD Server (.com)
    ↓
Authoritative Name Server (example.com)
    ↓
Địa chỉ IP của www.example.com
