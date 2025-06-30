Index
Được lưu ở disk. Tìm kiếm sẽ đọc thông tin dưới disk
—————————————————————————————————
Phân loại:
Data structure: B-tree, Hash, R-tree, Full text, ...
Physical storage: clustered index, non-clustered index
Number of column: single-column index, composite index (cover index)
Characteristics: primary key, unique, prefix
—————————————————————————————————
Data structure:
B tree:
Độ phức tạp: O(Log N)
Áp dụng cho các query: so sánh: =, !=, >, <, like, range
Sử dụng LIKE thì % ở cuối mới sử dụng dược index. Ví dụ ‘name%’
B+ tree:
Áp dụng cho các query: so sánh: =, !=, >, <, like, range
Tối ưu với query: range
Do các node lá đã được sắp xếp và link với nhau
Hash:
Sử dụng hash function để map key => hash table (dạng key-value)
Áp dụng với các query: so sánh =
Nhược điểm: Không phù hợp với range
—————————————————————————————————
Physical storage:
Clustered index:
Xác định vị trí vật lý của dữ liệu sẽ đặt ở đâu trên ổ đĩa
Một bảng có một clustered index duy nhất => primary key. Khi tạo primary key ngầm tạo clustered index tương ứng.
None-Clustered index (Secondary index):
Một bảng có nhiều None-Clustered index (Secondary index). Không phải primary key thì chính là None-Clustered index.
Trong B-tree thì node lá của Secondary index lưu giá trị của primary key index. Khi tìm thấy node lá, nó sẽ lấy thông tin của
primary key để duyệt B-tree của Clustered index
Cần ít nhất 2 thao tác đọc disk: đọc trên secondary index và clustered index
Nhược điểm:
Chậm quá trình insert dữ liệu, do quá trình tạo vào sửa index cũng sẽ mất một khoảng thời gian
Ghi vào disk nên chiếm memory của disk
Tại sao Secondary index lưu giá trị của primary key index mà không lưu địa chỉ vật lý của primary key index. Để trỏ
thằng đến địa chỉ luôn?
Do địa chỉ vật lý có thể thay đổi.
Sẽ thay đổi khi build lại index hoặc phân chia lại ổ đĩa
Insert-Delete thì không thay đổi
—————————————————————————————————
Characteristics: tính chất của index
Key & index khác nhau như thế nào:
Key: ràng buộc trên cột nào đó. VD: PK & FK
Index: cấu trúc để tăng tốc quá trình tìm kiếm dữ liệu
Primary index:
Sẽ là unique. Giá trị tăng dần thì sẽ hiệu quả hơn. B+ tree sẽ hạn chế tạo thêm node mới
Không cho phép giá trị NULL
Unique index:
Unique nhưng cho phép giá trị NULL

—————————————————————————————————
Number of columns
Composite index: index chứa nhiều column
Query có chứa cột đầu tiên mới sử dụng được index để cải thiện tốc độ query
Query cột đầu tiên chứa giá trị = là hiệu quả nhất
Cách xác định thứ tự hiệu quả:
Cardinality (số giá trị khác nhau). Những cột có cardinality lớn thì sẽ đặt đầu.
VD: (name, provine, country) do số lượng name khác nhau chắc chắn sẽ nhiều nhất .
Lý do: Lúc này duyệt tree, thì độ phức tạp theo thời gian sẽ giảm đi
—————————————————————————————————
Other
Fulltext (Inverted Index)
Spatial Index: GIST (Postgres)
Bitmap Index
—————————————————————————————————
Practices
Nên dùng index:
Các query chứa điều kiện where, join, group by, index thì nên có các column có index
Phù hợp lấy tập nhỏ dữ liệu. Lấy dữ liệu lớn có thể ko hiệu quả
Table chứa nhiều dữ liệu và phải query dữ liệu trong table này
Những trường là unique
Không nên dùng index:
Bảng quá ít dữ liệu
Những trường thường xuyên phải update. Hoặc bảng chỉ ghi
Những trường low-cardinality (quá ít giá trị khác nhau - ví dụ tuổi)
Những trường chứa lượng lớn giá trị NULL
—————————————————————————————————
Best Practices
Hạn chế số lượng index trong một bảng, tránh ảnh hưởng đến quá trình update, insert. Tuỳ thuộc vào các loại db.
Thậm chí khi có lượng lớn index có thể gây deadlock trong quá trình index.
Do ảnh hưởng có gap-lock (khoá khảng cách khi insert) có thể gây deadlock
Ưu tiên chọn primary key là kiểu tăng dần vì hạn chế việc di chuyển và tái cân bằng trê, phân mảnh.
Không làm việc tốt với giá trị NULL. Column nhiều index thì hạn chế.
Nên sử dụng covering index. Tránh hạn chế tốn I/O. Hạn chế đánh index từng cột vì phải mất 2 lần đọc vào ổ đĩa
Prefix index: Tránh tốn không gian lưu trữ index (dùng cho những trường có dữ liệu dài)
Cần monitor và optimize thường xuyên. Ít khi xảy ra
Tránh trường hợp failure index
——————————————————————————————————————————————————————————
Các column cần chú ý trong EXPLAIN
1. select_type:
SIMPLE: truy vấn cơ bản
PRIMARY
DERIVED: truy vấn con của truy vấn khác
SUBQUERY: truy vấn con
UNION:
2. table
3. type
- Quan trọng nhất
- Trả về type index mà câu query sử dụng
Index
Range
Ref
Const ....

All
All: là type tồi tệ nhất. Khi gặp type này thì cần phải tối ưu: index, giới hạn số record quét trong bảng, ...
4. Rows
=> quan trọng
Số lượng hàng phải quét qua để trả về kết quả
==> Làm thế nào để đánh index cho hợp lý