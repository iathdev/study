# Mã hóa đối xứng và bất đối xứng

## 1. Mã hóa đối xứng (Symmetric Encryption)

### ➤ Là gì?
Là phương pháp **dùng cùng một khóa (secret key)** để **mã hoá và giải mã** dữ liệu.

### ➤ Cách hoạt động:

```lua
+-----------+ +-----------+ +-----------+
| Sender | --(key)-> Ciphertext --(key)->| Receiver |
+-----------+ +-----------+ +-----------+
```


### ➤ Ví dụ:
- Cả hai bên cùng có khóa `abc123`.
- Dữ liệu được mã hoá bằng `abc123`, và bên kia giải mã cũng bằng `abc123`.

### ➤ Các thuật toán phổ biến:
- AES (Advanced Encryption Standard)
- DES / Triple DES
- ChaCha20
- Blowfish

### ➤ Ưu & Nhược điểm:

| Ưu điểm                  | Nhược điểm                                 |
|--------------------------|---------------------------------------------|
| Rất nhanh, hiệu quả cao  | Phải chia sẻ khóa an toàn trước khi dùng   |
| Dễ triển khai            | Không an toàn nếu nhiều người dùng chung key |
| Dữ liệu lớn mã hoá tốt   | Không hỗ trợ xác minh danh tính người gửi  |

---

## 2. Mã hóa bất đối xứng (Asymmetric Encryption)

### ➤ Là gì?
Là phương pháp sử dụng **hai khóa khác nhau**:
- **Public key (khóa công khai)** → dùng để **mã hoá**
- **Private key (khóa riêng tư)** → dùng để **giải mã**

### ➤ Cách hoạt động:

```lua
+-----------+ +-----------------+ +-----------+
| Sender | --> | Public Key of B | --> | Receiver |
+-----------+ +-----------------+ +-----------+
<--(Private Key to decrypt)
```


### ➤ Các thuật toán phổ biến:
- RSA
- ECC (Elliptic Curve Cryptography)
- ElGamal

### ➤ Ưu & Nhược điểm:

| Ưu điểm                                     | Nhược điểm                        |
|--------------------------------------------|------------------------------------|
| Không cần chia sẻ khóa bí mật              | Mã hoá & giải mã chậm hơn          |
| Hỗ trợ chữ ký số, xác thực danh tính       | Không phù hợp cho dữ liệu lớn      |
| Dùng để trao đổi key an toàn trong TLS     | Thường phải kết hợp với đối xứng   |

---

## 3. Ví dụ thực tế

| Trường hợp                      | Dùng loại gì?            | Ghi chú                                     |
|----------------------------------|---------------------------|---------------------------------------------|
| Mã hoá file lớn để backup        | Đối xứng (AES)            | Nhanh, gọn, không cần xác thực              |
| Gửi dữ liệu bảo mật qua Internet | Cả 2 (Hybrid)             | RSA để trao đổi khóa AES, AES để mã hoá nội dung |
| SSL/TLS (HTTPS)                  | Bắt đầu bằng bất đối xứng | Sau đó chuyển sang đối xứng để tăng tốc    |
| JWT, chữ ký số                   | Bất đối xứng              | Dùng private key để ký, public để xác minh  |

---

## 4. So sánh tổng quát

| Tiêu chí                  | Mã hoá đối xứng        | Mã hoá bất đối xứng       |
|---------------------------|------------------------|----------------------------|
| Số lượng khóa             | 1                      | 2 (public + private)       |
| Tốc độ                    | Rất nhanh              | Chậm hơn nhiều             |
| Độ phức tạp triển khai    | Đơn giản               | Phức tạp hơn               |
| Trao đổi khóa an toàn     | Khó khăn               | An toàn hơn                |
| Dùng cho dữ liệu lớn      | Rất phù hợp            | Không phù hợp              |
| Hỗ trợ xác minh danh tính | Không                  | Có                         |

---

## 5. Kết luận

- **Cần mã hoá nhanh, đơn giản?** → Dùng **đối xứng (AES)**
- **Cần trao đổi khóa an toàn, chữ ký số?** → Dùng **bất đối xứng (RSA, ECC)**
- **Cần bảo mật thực tế cao nhất?** → Dùng **cả hai (Hybrid encryption)**
