# Các bước xác định Time Complexity (Độ phức tạp thời gian)

Time Complexity (độ phức tạp thời gian) giúp ta ước lượng số bước xử lý của thuật toán khi kích thước đầu vào (`n`) tăng lên.

| Bước | Mục tiêu                             |
| ---- | ------------------------------------ |
| 1️⃣  | Xác định `n` là gì                   |
| 2️⃣  | Phân tích số lần lặp                 |
| 3️⃣  | Xác định thao tác chính              |
| 4️⃣  | Nếu có vòng lặp lồng nhau → nhân lại |
| 5️⃣  | Nếu có đệ quy → viết phương trình    |
| 6️⃣  | Giữ lại phần lớn nhất trong Big-O    |

---

## 1. Xác định đầu vào chính (`n`)

- `n` là kích thước dữ liệu đầu vào (số phần tử trong mảng, số node, độ dài chuỗi,...)
- Mọi tính toán sẽ xoay quanh giá trị này.

---

## 2. Phân tích vòng lặp

- Với mỗi vòng lặp, ước lượng nó chạy bao nhiêu lần:
  - `for (i = 0; i < n; i++)` → O(n)
  - `for (i = 0; i < n; i++)` + `for (j = 0; j < n; j++)` → O(n²)
  - `for (i = 1; i < n; i *= 2)` → O(log n)

---

## 3. Xác định thao tác bên trong vòng lặp

- Truy cập mảng: `arr[i]` → O(1)
- Gọi hàm → xem trong hàm có vòng lặp không
- Tính tổng: O(n), Tìm max/min: O(n), So sánh cặp phần tử: O(n²)

---

## 4. Nhân số lần vòng lặp nếu lồng nhau

Ví dụ:

```php
for ($i = 0; $i < n; $i++) {
    for ($j = 0; $j < n; $j++) {
        // thao tác O(1)
    }
}
```
→ n * n = O(n²)

## 5. Nếu có đệ quy → viết phương trình đệ quy

```php
function fib($n) {
    if ($n <= 1) return 1;
    return fib($n - 1) + fib($n - 2);
}

```
→ Gọi 2 nhánh mỗi lần → O(2ⁿ)

## 6. Loại bỏ hằng số & phần không đáng kể

- O(n² + n) → O(n²)

- O(n + log n) → O(n)

Chỉ giữ lại phần tăng trưởng nhanh nhất khi n lớn.

## Một số Time Complexity phổ biến

| Pattern / Hành vi                    | Time Complexity |
| ------------------------------------ | --------------- |
| Duyệt 1 lần mảng                     | O(n)            |
| 2 vòng for lồng nhau (n \* n)        | O(n²)           |
| Vòng lặp tăng log: `i *= 2`          | O(log n)        |
| Tìm kiếm nhị phân                    | O(log n)        |
| Quicksort / Mergesort                | O(n log n)      |
| DFS / BFS đồ thị với n đỉnh + m cạnh | O(n + m)        |
| Đệ quy 2 nhánh (fib n)               | O(2ⁿ)           |




