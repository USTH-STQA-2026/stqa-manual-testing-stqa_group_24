# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | `<!-- Tên nhóm -->` |
| **Ngày tạo** | `<!-- DD/MM/YYYY -->` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Email có tồn tại trong DB? | Có | `librarian@library.com` | Đăng nhập thành công |
| | Không | `noone@email.com` | Thông báo lỗi |
| Mật khẩu có đúng? | Đúng | `admin123` | Đăng nhập thành công |
| | Sai | `wrongpass` | Thông báo lỗi |
| Ô nhập có rỗng? | Không rỗng | (giá trị bất kỳ) | Xử lý bình thường |
| | Rỗng | `""` | Thông báo "Vui lòng nhập..." |

### IDM — Tìm kiếm sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Từ khóa có tồn tại trong DB? | Có (tên sách) | `"Flutter"` | Hiển thị sách chứa "Flutter" |
| | Có (tên tác giả) | `"Nguyễn"` | Hiển thị sách của tác giả Nguyễn |
| | Không | `"XYZ123"` | Danh sách rỗng |
| Phân biệt HOA/thường? | Chữ thường | `"flutter"` | Kết quả giống "Flutter" |
| | Chữ HOA | `"FLUTTER"` | Kết quả giống "Flutter" |

### IDM — Mượn sách (REQ-04, REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái sách? | Có sẵn | BOOK001 | Cho phép mượn |
| | Đang mượn | BOOK003 | Không cho phép |
| | Thất lạc | BOOK007 | Không cho phép |
| Trạng thái thành viên? | Hoạt động | MEM002 | Cho phép mượn |
| | Tạm ngưng | MEM004 | Từ chối, thông báo lỗi |
| | Hết hạn | MEM005 | Từ chối, thông báo lỗi |
| Số sách đang mượn? | < 3 (BVA: 0, 1, 2) | MEM006 (0 sách) | Cho phép mượn |
| | = 3 (BVA: giới hạn) | MEM đã mượn 3 sách | Từ chối, thông báo vượt giới hạn |

### IDM — `<!-- Nhóm tự bổ sung cho REQ-05 đến REQ-08 -->`

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| `<!-- Nhóm tự điền -->` | | | |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | Đăng nhập thành công với tài khoản và mật khẩu hợp lệ | 1. Người dùng đang ở trang đăng nhập. 2. Tài khoản đã tồn tại trên hệ thống. | 1. Nhập Email hợp lệ. 2. Nhập Mật khẩu hợp lệ. 3. Nhấn nút “Đăng nhập”. | Email: `librarian@library.com`, Mật khẩu: `admin123` | - Chuyển hướng sang trang chủ thành công. - Trên AppBar hiển thị chính xác tên người dùng + vai trò. | REQ-01 | Decision Table (True/True) |
| TC-02 | Báo lỗi khi nhập Email chưa đăng ký hệ thống | Người dùng đang ở trang đăng nhập. | 1. Nhập Email chưa tồn tại. 2. Nhập Mật khẩu bất kỳ. 3. Nhấn nút "Đăng nhập". | Email: `nobody@test.com`, Mật khẩu: `anything` | Hiển thị thông báo lỗi: "Không tìm thấy thành viên". | REQ-01 | Decision Table (False/True) |
| TC-03 | Báo lỗi khi nhập đúng Email nhưng sai Mật khẩu | 1. Người dùng đang ở trang đăng nhập. 2. Email đã tồn tại trên hệ thống. | 1. Nhập Email đúng. 2. Nhập Mật khẩu sai. 3. Nhấn nút "Đăng nhập". | Email: `ba.nguyen@email.com`, Mật khẩu: `wrongpassword` | Hiển thị thông báo lỗi: "Mật khẩu không đúng". | REQ-01 | Decision Table (True/False) |
| TC-04 | Báo lỗi khi bỏ trống cả Email và Mật khẩu | Người dùng đang ở trang đăng nhập. | 1. Để trống trường Email. 2. Để trống trường Mật khẩu. 3. Nhấn nút "Đăng nhập". | Email: (để trống), Mật khẩu: (để trống) | Hiển thị thông báo lỗi: "Vui lòng nhập email và mật khẩu". | REQ-01 | Decision Table (Trống/Trống) |
| TC-05 | Báo lỗi khi chỉ nhập Mật khẩu và bỏ trống Email | Người dùng đang ở trang đăng nhập. | 1. Để trống trường Email. 2. Nhập Mật khẩu bất kỳ. 3. Nhấn nút "Đăng nhập". | Email: (để trống), Mật khẩu: `anything` | Hiển thị thông báo lỗi: "Vui lòng nhập email và mật khẩu". | REQ-01 | EP (Tương đương vùng Trống) |
| TC-06 | Báo lỗi khi chỉ nhập Email và bỏ trống Mật khẩu | Người dùng đang ở trang đăng nhập. | 1. Nhập Email hợp lệ. 2. Để trống trường Mật khẩu. 3. Nhấn nút "Đăng nhập". | Email: `librarian@library.com`, Mật khẩu: (để trống) | Hiển thị thông báo lỗi: "Vui lòng nhập email và mật khẩu". | REQ-01 | EP (Tương đương vùng Trống) |
| TC-07 | Báo lỗi khi nhập cả Email sai và Mật khẩu sai | Người dùng đang ở trang đăng nhập. | 1. Nhập Email chưa tồn tại. 2. Nhập Mật khẩu sai. 3. Nhấn nút "Đăng nhập". | Email: `nobody@test.com`, Mật khẩu: `wrongpassword` | Hiển thị thông báo lỗi: "Không tìm thấy thành viên”. | REQ-01 | Decision Table (False/False) |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
