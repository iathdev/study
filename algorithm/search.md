# Tổng hợp Thuật Toán Tìm Kiếm (Search Algorithms)

## 1. Linear Search (Tìm kiếm tuyến tính)

- Ý tưởng: Duyệt từng phần tử trong mảng từ đầu đến cuối để tìm phần tử cần tìm.
- Ưu điểm: Đơn giản, dễ hiểu, dùng được cho mảng chưa sắp xếp.
- Nhược điểm: Chậm với mảng lớn.
- Độ phức tạp: O(n)

---

## 2. Binary Search (Tìm kiếm nhị phân)

- Ý tưởng: Chia đôi mảng đã sắp xếp, so sánh phần tử ở giữa, loại bỏ 1 nửa mỗi bước.
- Điều kiện áp dụng: Mảng đã sắp xếp.
- Độ phức tạp: O(log n)

---

## 3. Jump Search

- Ý tưởng: Nhảy từng bước cố định (ví dụ √n), sau đó tìm kiếm tuyến tính trong đoạn đó.
- Độ phức tạp: O(√n)

---

## 4. Interpolation Search

- Ý tưởng: Giống Binary Search, nhưng ước lượng vị trí phần tử cần tìm bằng công thức nội suy.
- Điều kiện áp dụng: Mảng sắp xếp đều.
- Độ phức tạp: 
  - Trung bình: O(log log n)
  - Xấu nhất: O(n)

---

## 5. Exponential Search

- Ý tưởng: Tăng phạm vi tìm kiếm theo cấp số nhân (1, 2, 4, 8...) cho đến khi vượt giá trị cần tìm → dùng Binary Search trong đoạn đó.
- Độ phức tạp: O(log n)

---

## 6. Ternary Search

- Ý tưởng: Chia mảng thành 3 phần thay vì 2. Thường dùng để tìm cực trị (min/max) trong hàm đơn điệu.
- Độ phức tạp: O(log n)

---

## 7. Hash Table Lookup

- Ý tưởng: Dùng HashMap để tìm phần tử theo key.
- Ưu điểm: Truy cập rất nhanh nếu không bị collision.
- Độ phức tạp:
  - Trung bình: O(1)
  - Xấu nhất (collision): O(n)

Giải thích:
- Trong cấu trúc dữ liệu Hash Table, mỗi phần tử được lưu trữ tại một vị trí được xác định bởi hàm băm (hash function).
- Nếu hai key khác nhau tạo ra cùng giá trị hash → dẫn đến collision <br>
Ví dụ: hash("apple") = 5, hash("banana") = 5

---

## 8. BFS / DFS (Graph Search)

- Ý tưởng: Duyệt đồ thị hoặc cây để tìm kiếm theo chiều rộng (BFS) hoặc chiều sâu (DFS).
- Độ phức tạp: O(V + E) với:
  - V: số đỉnh (vertices)
  - E: số cạnh (edges)

---

## 9. A* Search / Dijkstra

- Ý tưởng: Tìm đường đi ngắn nhất trên đồ thị.
- Ứng dụng: GPS, game AI, routing, ...
- Độ phức tạp: Phụ thuộc vào cấu trúc đồ thị và cách cài đặt heap.

---

## Bảng So Sánh

| Thuật toán             | Áp dụng                       | Time (trung bình) | Cần sắp xếp |
|------------------------|-------------------------------|-------------------|-------------|
| Linear Search          | Mảng bất kỳ                   | O(n)              | Không        |
| Binary Search          | Mảng đã sắp xếp               | O(log n)          | Có           |
| Jump Search            | Mảng đã sắp xếp               | O(√n)             | Có           |
| Interpolation Search   | Mảng sắp xếp đều              | O(log log n)      | Có           |
| Exponential Search     | Mảng lớn, đã sắp xếp          | O(log n)          | Có           |
| Hash Lookup            | Tìm theo key                  | O(1)              | Không        |
| BFS / DFS              | Duyệt graph, tree             | O(V + E)          | Không        |
| A* / Dijkstra          | Tìm đường đi ngắn nhất        | Tùy cấu trúc       | Không        |

---

## Ghi chú thêm

- log n thường là log cơ số 2 trong thuật toán.
- Nếu cần cài đặt ví dụ cụ thể (C++, Java, PHP...), có thể thêm vào theo yêu cầu.


## Nếu bạn cần tìm kiếm trong 1 triệu bản ghi, thuật toán tốt nhất phụ thuộc vào dữ liệu đã được sắp xếp hay chưa, và bạn tìm kiếm theo kiểu gì (exact, range, fuzzy, v.v.).

1. Dữ liệu đã được sắp xếp → Dùng Binary Search
Thuật toán: Tìm kiếm nhị phân (Binary Search)

Độ phức tạp: O(log n) → Rất nhanh (log₂1_000_000 ≈ 20 lần so sánh)

Điều kiện: Dữ liệu phải được sắp xếp theo khóa tìm kiếm

2. Dữ liệu chưa sắp xếp → Dùng Hash Table nếu có thể
Thuật toán: Hashing (băm)

Độ phức tạp: O(1) trung bình (truy cập trực tiếp qua khóa)

Dùng khi: Bạn tìm kiếm theo key (mã, id,...), có thể tổ chức lại dữ liệu


| Loại tìm kiếm | Dữ liệu   | Thuật toán gợi ý     | Độ phức tạp             |
| ------------- | --------- | -------------------- | ----------------------- |
| Theo ID, mã   | Sắp xếp   | Binary Search        | `O(log n)`              |
| Theo ID, mã   | Không sắp | Hash Table           | `O(1)`                  |
| Tìm gần đúng  | Chuỗi     | Levenshtein, BK-tree | `O(n*m)`                |
| Theo khoảng   | Sắp xếp   | Segment Tree, BST    | `O(log n)` hoặc tốt hơn |
| Dữ liệu lớn   | > RAM     | B-Tree, Index        | Tùy vào DB              |

