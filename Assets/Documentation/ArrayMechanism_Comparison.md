# Phân tích Cơ chế Array & So sánh Ngôn ngữ

Tài liệu này đi sâu vào cách mảng được triển khai bên dưới các ngôn ngữ lập trình khác nhau.

---

## 1. Bản chất của Mảng Tĩnh (Static Array)
Mảng tĩnh là một khối bộ nhớ **liên tục**.
- **Công thức tính địa chỉ:** `Address = Base + (Index * Size)`.
- **Tốc độ:** O(1) - Truy cập tức thời vì CPU chỉ cần thực hiện 1 phép tính toán học.

---

## 2. Cơ chế Mảng Động (Dynamic Array/List)
Lập trình viên cảm thấy mảng có thể "co giãn", nhưng thực chất CPU không làm được việc đó:
1. **Khởi tạo:** Cấp phát một mảng tĩnh ban đầu (ví dụ size = 4).
2. **Khi đầy:** 
   - Cấp phát mảng mới lớn gấp đôi (Size = 8).
   - Copy dữ liệu cũ sang mảng mới.
   - Giải phóng mảng cũ.
3. **Chi phí:** Thao tác "Add" bình thường là O(1), nhưng khi bị Resize sẽ là O(n).

---

## 3. Managed vs Unmanaged (C# vs C/C++)

### C# (Managed)
- Mảng thường (`int[]`) nằm trên **Heap**.
- Được quản lý bởi Garbage Collector (GC).
- An toàn nhưng có độ trễ do GC.
- **`fixed` keyword:** Ghim mảng trên Heap để lấy con trỏ `unsafe`.

### C / C++ (Unmanaged)
- Tự do quyết định vị trí: `int a[5]` (Stack) hoặc `malloc(5)` (Heap).
- Không có GC, phải `free` thủ công.
- Tốc độ tối đa, rủi ro cao (Buffer Overflow).

---

## 4. Kỹ thuật Zero-Copy & Blittable Types
Được sử dụng trong Unity DOTS để tối ưu hiệu suất:
- **Blittable:** Các kiểu dữ liệu có cấu trúc nhị phân giống hệt nhau giữa C# và C++ (int, float, struct thuần).
- **Cơ chế:** C# gửi con trỏ (địa chỉ RAM) cho C++ thay vì copy toàn bộ mảng dữ liệu. C++ đọc trực tiếp từ bộ nhớ của C#.

---

## 5. JavaScript & Modern Web Memory
JavaScript hiện đại đã tiến xa với:
- **ArrayBuffer:** Cấp phát vùng nhớ nhị phân thô (Raw binary).
- **TypedArray:** (Int32Array, Float64Array) - Các view để thao tác trên Buffer giống như mảng trong C.
- **WebAssembly (Wasm):** Cho phép chạy C++/Rust trong trình duyệt với bộ nhớ chia sẻ với JS, đạt hiệu năng gần như Native.
