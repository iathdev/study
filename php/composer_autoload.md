# 🎼 Composer và Autoload trong PHP

---

## 📦 1. Composer là gì?

**Composer** là một công cụ quản lý thư viện (dependency manager) cho PHP. Nó giúp bạn:

- Cài đặt và cập nhật thư viện PHP từ [Packagist](https://packagist.org)
- Tự động nạp (autoload) các lớp mà bạn định nghĩa hoặc dùng từ thư viện
- Quản lý phiên bản thư viện theo từng project (local)

---

## 📁 2. Autoload là gì?

**Autoload** giúp PHP tự động tìm và nạp file chứa class khi bạn `new` một đối tượng hoặc sử dụng một class, mà không cần `require` thủ công.

### 🔄 Composer hỗ trợ Autoload bằng cách:

- Dựa trên chuẩn [PSR-4](https://www.php-fig.org/psr/psr-4/)
- Mapping namespace vào thư mục tương ứng
- Tự động tạo file `vendor/autoload.php` để nạp tất cả các class

| Loại       | Giải thích                                       |
| ---------- | ------------------------------------------------ |
| `psr-4`    | Ánh xạ namespace → thư mục, chuẩn hiện đại       |
| `classmap` | Quét tất cả các file PHP để tìm class            |
| `files`    | Nạp thẳng các file (dùng cho function, constant) |
