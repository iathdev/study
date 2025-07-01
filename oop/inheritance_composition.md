| Tiêu chí                | Inheritance (Kế thừa)       | Composition (Thành phần)      |
| ----------------------- | --------------------------- | ----------------------------- |
| Quan hệ                 | "is-a" (là một loại)        | "has-a" (có một)              |
| Độ linh hoạt            | Thấp – phụ thuộc cha        | Cao – thay đổi runtime được   |
| Dễ test                 | Khó test độc lập            | Dễ test theo từng thành phần  |
| Phù hợp khi             | Có phân cấp logic rõ ràng   | Cần linh hoạt, module rời rạc |
| Sử dụng lại code        | Qua kế thừa                 | Qua sử dụng đối tượng         |
| Dễ bị ảnh hưởng khi sửa | Cao – sửa lớp cha ảnh hưởng | Thấp – module tách biệt       |
| Đa hình                 | Hỗ trợ tốt                  | Hỗ trợ thông qua interface    |
| Design pattern hỗ trợ   | Template Method             | Strategy, Decorator, Adapter  |
