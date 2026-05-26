# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | Group 24 |
| **Ngày tạo** | 20/05/2026 |
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

### IDM — Trả sách, xử lý quá hạn, quản lý thành viên (REQ-05, REQ-06, REQ-07)

| Đặc tính | Phân vùng | Giá trị đại diện | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái phiếu khi trả sách | Phiếu đang mượn | Phiếu mượn mới tạo từ BOOK002 | Cho phép trả sách |
| | Phiếu không thuộc thành viên hiện tại | BOOK013 đang được MEM006 mượn | Thành viên khác không được trả |
| Trả sách quá hạn | Phiếu quá hạn | BR001 / BOOK003 | Khi trả phải hiển thị cảnh báo quá hạn |
| Trạng thái sách sau khi trả | Đang mượn → Có sẵn | BOOK002 sau khi trả | Sách chuyển về trạng thái “Có sẵn” |
| Kiểm tra quá hạn | dueDate ≤ ngày hiện tại | BR001, hạn trả 15/09/2024 | Phiếu được đánh dấu “Quá hạn” |
| Quyền kiểm tra quá hạn | Thủ thư | librarian@library.com | Được kiểm tra quá hạn |
| Quyền thêm thành viên | Thủ thư | librarian@library.com | Được thêm thành viên mới |
| | Thành viên thường | ba.nguyen@email.com | Không được thêm thành viên |
| Email thành viên mới | Email hợp lệ | nguyen.van.moi@example.com | Tạo thành viên thành công |
| | Thiếu dấu chấm trong domain | user@domain | Từ chối, báo email không hợp lệ |
| | Email đã tồn tại | ba.nguyen@email.com | Từ chối, báo email đã tồn tại |

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
| TC-32 | Kiểm tra trả sách đang mượn thành công | 1. Dữ liệu đã được reset. 2. Đăng nhập bằng tài khoản thành viên hoạt động. 3. Thành viên mượn một sách có sẵn trong phiên hiện tại. | 1. Đăng nhập bằng `dam.tran@email.com`. 2. Vào tab **Sách**. 3. Mượn sách BOOK002 nếu đang “Có sẵn”. 4. Vào tab **Mượn / Trả**. 5. Chọn phiếu mượn của BOOK002. 6. Nhấn **Trả sách**. 7. Quay lại tab **Sách** và kiểm tra trạng thái BOOK002. | Tài khoản: `dam.tran@email.com` / `password123`; Sách: BOOK002 | - Hệ thống trả sách thành công. - Phiếu mượn BOOK002 chuyển sang trạng thái “Đã trả”. - BOOK002 chuyển về trạng thái “Có sẵn”. | REQ-05 | Happy Path, State Transition |
| TC-33 | Kiểm tra trả sách quá hạn phải hiển thị cảnh báo quá hạn | 1. Dữ liệu đã được reset. 2. BR001 tồn tại trong dữ liệu ban đầu và đã quá hạn. | 1. Đăng nhập bằng `ba.nguyen@email.com`. 2. Vào tab **Mượn / Trả**. 3. Tìm phiếu BR001 hoặc sách BOOK003. 4. Nhấn **Trả sách**. 5. Quan sát thông báo sau khi trả. | Tài khoản: `ba.nguyen@email.com` / `password123`; Phiếu: BR001; Sách: BOOK003 | - Hệ thống cho phép trả sách. - Hệ thống hiển thị cảnh báo quá hạn. - BOOK003 chuyển về trạng thái “Có sẵn”. | REQ-05 | BVA, Scenario |
| TC-34 | Kiểm tra thành viên không được trả sách của người khác | 1. Dữ liệu đã được reset. 2. Đăng nhập bằng tài khoản MEM002. | 1. Đăng nhập bằng `ba.nguyen@email.com`. 2. Vào tab **Mượn / Trả**. 3. Kiểm tra xem có thấy phiếu mượn BOOK013 của MEM006 không. 4. Nếu hệ thống cho thao tác, thử trả BOOK013. | Tài khoản: `ba.nguyen@email.com`; Sách của người khác: BOOK013 | MEM002 không được thấy hoặc không được trả BOOK013 vì sách này thuộc phiếu mượn của MEM006. | REQ-05, REQ-08 | Negative, Access Control |
| TC-35 | Kiểm tra thủ thư có thể thực hiện kiểm tra quá hạn | 1. Dữ liệu đã được reset. 2. Đang ở màn hình đăng nhập. | 1. Đăng nhập bằng `librarian@library.com`. 2. Vào tab **Mượn / Trả** hoặc khu vực có nút **Kiểm tra quá hạn**. 3. Nhấn **Kiểm tra quá hạn**. 4. Quan sát phản hồi của hệ thống. | Tài khoản: `librarian@library.com` / `admin123` | Hệ thống thực hiện kiểm tra quá hạn và cập nhật các phiếu có ngày hết hạn ≤ ngày hiện tại sang trạng thái “Quá hạn”. | REQ-06 | BVA |
| TC-36 | Kiểm tra phiếu quá hạn được đánh dấu “Quá hạn” | 1. Dữ liệu đã được reset. 2. Đăng nhập bằng tài khoản thủ thư. | 1. Đăng nhập bằng thủ thư. 2. Vào tab **Mượn / Trả**. 3. Quan sát trạng thái BR001 trước khi kiểm tra quá hạn. 4. Nhấn **Kiểm tra quá hạn**. 5. Quan sát lại trạng thái BR001. | Phiếu: BR001; Ngày hết hạn: 15/09/2024 Phiếu: BR003; Hạn trả: 15/10/2024 | BR001 được đánh dấu trạng thái “Quá hạn”. Nếu hệ thống còn phiếu đang mượn khác có ngày hết hạn ≤ ngày hiện tại, các phiếu đó cũng được đánh dấu “Quá hạn”. | REQ-06 | BVA |
| TC-37 | Kiểm tra thủ thư thêm thành viên mới với thông tin hợp lệ | 1. Dữ liệu đã được reset. 2. Đăng nhập bằng tài khoản thủ thư. | 1. Đăng nhập bằng `librarian@library.com`. 2. Vào tab **Thành viên**. 3. Chọn **Thêm thành viên**. 4. Nhập họ tên, email và số điện thoại hợp lệ. 5. Nhấn **Lưu** hoặc **Thêm**. | Họ tên: `Nguyễn Văn Mới`; Email: `nguyen.van.moi@example.com`; SĐT: `0912345678` | Hệ thống tạo thành viên mới thành công. Thành viên `Nguyễn Văn Mới` xuất hiện trong danh sách thành viên. | REQ-07 | Happy Path, EP |
| TC-38 | Kiểm tra thành viên thường không được thêm thành viên mới | 1. Dữ liệu đã được reset. 2. Đăng nhập bằng tài khoản thành viên thường. | 1. Đăng nhập bằng `ba.nguyen@email.com`. 2. Quan sát thanh menu hoặc các tab chức năng. 3. Kiểm tra có tab **Thành viên** hoặc nút **Thêm thành viên** không. | Tài khoản: `ba.nguyen@email.com` / `password123` | Thành viên thường không được truy cập chức năng quản lý thành viên và không thể thêm thành viên mới. | REQ-07 | Access Control, Negative |
| TC-39 | Kiểm tra không cho thêm thành viên với email thiếu dấu chấm trong domain | 1. Dữ liệu đã được reset. 2. Đăng nhập bằng tài khoản thủ thư. | 1. Đăng nhập bằng thủ thư. 2. Vào tab **Thành viên**. 3. Chọn **Thêm thành viên**. 4. Nhập họ tên `Email Sai Domain`. 5. Nhập email `user@domain`. 6. Nhập SĐT `0912345678`. 7. Nhấn **Lưu** hoặc **Thêm**. | Họ tên: `Email Sai Domain`; Email: `user@domain`; SĐT: `0912345678` | Hệ thống không tạo thành viên mới và hiển thị lỗi email không hợp lệ vì email thiếu dấu `.` trong phần domain. | REQ-07 | BVA, EP |
| TC-40 | Kiểm tra không cho thêm thành viên với email đã tồn tại | 1. Dữ liệu đã được reset. 2. Đăng nhập bằng tài khoản thủ thư. | 1. Đăng nhập bằng thủ thư. 2. Vào tab **Thành viên**. 3. Chọn **Thêm thành viên**. 4. Nhập họ tên `Nguyễn Trùng Email`. 5. Nhập email đã tồn tại `ba.nguyen@email.com`. 6. Nhập SĐT `0912345678`. 7. Nhấn **Lưu** hoặc **Thêm**. | Họ tên: `Nguyễn Trùng Email`; Email: `ba.nguyen@email.com`; SĐT: `0912345678` | Hệ thống không tạo thành viên mới và hiển thị lỗi email đã tồn tại hoặc email bị trùng. | REQ-07 | EP, Negative |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
