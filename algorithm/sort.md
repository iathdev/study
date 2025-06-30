# Các Thuật Toán Sắp Xếp (Sorting Algorithms)

## 1. Bubble Sort (Sắp xếp nổi bọt)

### Nguyên lý:
So sánh từng cặp phần tử liền kề và hoán đổi nếu sai thứ tự. Lặp lại đến khi mảng được sắp xếp.

### Độ phức tạp:
- Best case: O(n) (khi đã sắp xếp, có kiểm tra)
- Average/Worst: O(n²)

### Sử dụng:
- Khi mảng rất nhỏ và không yêu cầu hiệu suất.
- Đơn giản, dễ hiểu (mục đích giáo dục).

---

## 2. Selection Sort (Sắp xếp chọn)

### Nguyên lý:
Tìm phần tử nhỏ nhất và đưa về đầu mảng. Lặp lại với phần còn lại.

### Độ phức tạp:
- Best/Average/Worst: O(n²)

### Sử dụng:
- Không dùng trong thực tế với dữ liệu lớn.
- Tốt khi cần sắp xếp **bộ nhớ ít thay đổi** vì số lần hoán đổi ít (O(n)).

---

## 3. Insertion Sort (Sắp xếp chèn)

### Nguyên lý:
Xây dựng mảng kết quả bằng cách chèn phần tử vào vị trí thích hợp trong phần đã sắp xếp.

### Độ phức tạp:
- Best: O(n) (mảng gần như đã sắp xếp)
- Average/Worst: O(n²)

### Sử dụng:
- Dữ liệu nhỏ hoặc gần như đã sắp xếp.
- Tốt cho danh sách nhỏ chèn dần.

---

## 4. Merge Sort (Sắp xếp trộn - chia để trị)

### Nguyên lý:
Chia đôi mảng → sắp xếp từng phần → trộn (merge) lại theo thứ tự.

### Độ phức tạp:
- Best/Average/Worst: O(n log n)
- Space: O(n) (dùng bộ nhớ phụ)

### Sử dụng:
- Cần ổn định và độ phức tạp thấp.
- Tốt với dữ liệu lớn hoặc cần ổn định sắp xếp (Stable Sort).

---

## 5. Quick Sort (Sắp xếp nhanh - chia để trị với pivot)

### Nguyên lý:
Chọn pivot → chia mảng thành 2 phần nhỏ hơn/lớn hơn → đệ quy

### Độ phức tạp:
- Best/Average: O(n log n)
- Worst: O(n²) (khi pivot chọn không tốt)
- Space: O(log n)

### Sử dụng:
- Hiệu suất rất tốt cho mảng lớn nếu có chiến lược chọn pivot tốt.
- Được dùng phổ biến nhất thực tế.

---

## 6. Heap Sort (Sắp xếp vun đống)

### Nguyên lý:
Xây dựng heap (cây nhị phân) → lấy max/min → đưa về cuối mảng

### Độ phức tạp:
- Best/Average/Worst: O(n log n)
- Space: O(1)

### Sử dụng:
- Cần độ phức tạp ổn định O(n log n), không cần bộ nhớ phụ.
- Không ổn định (không giữ vị trí phần tử giống nhau).

---

## 7. Counting Sort (Sắp xếp đếm)

### Nguyên lý:
Đếm số lượng phần tử xuất hiện → xác định vị trí.

### Độ phức tạp:
- O(n + k), với `k` là giá trị lớn nhất

### Sử dụng:
- Khi dữ liệu là số nguyên nhỏ, phạm vi giá trị nhỏ.
- Tốt cho dữ liệu rời rạc (ví dụ: điểm số từ 0 → 100)

---

## 8. Radix Sort

### Nguyên lý:
Sắp xếp theo chữ số (từng hàng đơn vị, chục, trăm...)

### Độ phức tạp:
- O(n * k), với `k` là số chữ số tối đa

### Sử dụng:
- Dữ liệu là số nguyên, chuỗi có độ dài không quá lớn.
- Tốt hơn Counting Sort nếu số chữ số nhỏ.

---

## 9. Bucket Sort

### Nguyên lý:
Chia phần tử thành nhiều “bucket”, mỗi bucket sắp xếp riêng rồi gộp lại.

### Độ phức tạp:
- Best: O(n + k)
- Worst: O(n²) (nếu phân phối không đều)

### Sử dụng:
- Dữ liệu phân phối đều, số thực từ 0 đến 1.
- Cần kỹ thuật phân chia bucket tốt.

---

# So sánh tổng quan

| Thuật toán       | Time Avg  | Space   | Stable | Thích hợp với                      |
|------------------|-----------|---------|--------|------------------------------------|
| Bubble Sort      | O(n²)     | O(1)    | ✔      | Mảng nhỏ, học thuật toán           |
| Selection Sort   | O(n²)     | O(1)    | ✘      | Cần ít hoán đổi                    |
| Insertion Sort   | O(n²)     | O(1)    | ✔      | Gần như đã sắp xếp                 |
| Merge Sort       | O(n log n)| O(n)    | ✔      | Cần độ ổn định, mảng lớn           |
| Quick Sort       | O(n log n)| O(log n)| ✘      | Tốt cho hiệu suất cao              |
| Heap Sort        | O(n log n)| O(1)    | ✘      | Không cần ổn định, ít RAM          |
| Counting Sort    | O(n + k)  | O(k)    | ✔      | Số nguyên, phạm vi nhỏ             |
| Radix Sort       | O(nk)     | O(n + k)| ✔      | Chuỗi/số nguyên, số chữ số nhỏ     |
| Bucket Sort      | O(n + k)  | O(n)    | ✔      | Dữ liệu phân phối đều              |

## Với 1 dãy có 1 triệu bản ghi, nên dùng thuật toán nào?
Quick Sort, Merge Sort, hoặc Heap Sort — tùy thuộc vào yêu cầu cụ thể về:


| Tiêu chí                                   | Khuyến nghị thuật toán            |
| ------------------------------------------ | --------------------------------- |
| Cần **hiệu suất cao** (RAM ổn)             | `Quick Sort` (nếu pivot tốt)      |
| Cần **ổn định (stable sort)**              | `Merge Sort`                      |
| Cần **tiết kiệm bộ nhớ**                   | `Heap Sort` (không dùng RAM phụ)  |
| Dữ liệu **đã gần sắp xếp**                 | `Insertion Sort` có thể rất nhanh |
| Dữ liệu là **số nguyên nhỏ, phân tán đều** | `Counting Sort`, `Radix Sort`     |


