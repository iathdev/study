| Tiêu chí                   | **Database**                                   | **Cache**                                     |
| -------------------------- | ---------------------------------------------- | --------------------------------------------- |
| **Lưu ở đâu**              | Trên **disk** (ổ cứng, SSD, đôi khi cloud)     | Trong **RAM** (bộ nhớ tạm, nhanh)             |
| Mục đích chính             | Lưu trữ **dữ liệu lâu dài**, có tính nhất quán | Lưu **tạm thời dữ liệu truy cập nhanh**       |
| Tính bền vững (persistent) | Có – dữ liệu lưu **vĩnh viễn** trên disk       | Không – **RAM-based**, dễ mất khi reset       |
| Tốc độ truy cập            | Chậm hơn (do lưu trên disk, có index...)       | Nhanh hơn (lưu trong RAM, truy cập tức thì)   |
| Dung lượng                 | Rất lớn (GB → TB)                              | Giới hạn (RAM vài trăm MB → vài GB)           |
| Tính nhất quán dữ liệu     | Đảm bảo (ACID)                                 | Không đảm bảo (eventually consistent)         |
| Khi nào mất dữ liệu?       | Khi xóa DB, hỏng ổ, hoặc cố ý drop             | Khi restart service, hết TTL, hoặc hết RAM    |
| Kiểu truy vấn              | Đa dạng (SQL, JOIN, filter...)                 | Đơn giản (theo key) – NoSQL hoặc object cache |
| Có hỗ trợ backup?          | Có                                             | Ít khi dùng backup                            |
| Chi phí lưu trữ            | Rẻ hơn (disk-based)                            | Đắt hơn (RAM)                                 |
| Ví dụ phổ biến             |                                                |                                               |



| So sánh nhanh     | Database                | Cache                       |
| ----------------- | ----------------------- | --------------------------- |
| Lưu trữ lâu dài   | Có                      | Không                       |
| Tốc độ            | Chậm hơn                | Rất nhanh                   |
| Dung lượng        | Lớn                     | Giới hạn (RAM)              |
| Chi phí           | Rẻ hơn                  | Đắt hơn (RAM-based)         |
| Truy vấn nâng cao | Có SQL, JOIN            | Chủ yếu theo key            |
| Mục tiêu chính    | Nguồn dữ liệu chuẩn xác | Tăng hiệu suất, giảm tải DB |

