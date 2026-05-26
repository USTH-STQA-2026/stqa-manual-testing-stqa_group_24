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

### IDM — Trả sách, Quá hạn, Quản lý thành viên (REQ-05, REQ-06, REQ-07)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái phiếu mượn khi trả sách | Đang mượn | BR001 / phiếu mượn mới tạo | Cho phép trả sách |
| | Đã trả | BR002 | Không cần trả lại lần nữa / không cho thao tác trả |
| Sách sau khi trả | Đang mượn → Có sẵn | BOOK002 sau khi mượn rồi trả | Trạng thái sách chuyển về “Có sẵn” |
| Trả sách quá hạn | Quá hạn | BR001, dueDate 15/09/2024 | Hiển thị cảnh báo quá hạn |
| Kiểm tra quá hạn | dueDate ≤ ngày hiện tại | BR001 | Phiếu được đánh dấu “Quá hạn” |
| | dueDate > ngày hiện tại | Phiếu chưa đến hạn nếu có | Không bị đánh dấu quá hạn |
| Quyền thêm thành viên | Thủ thư | librarian@library.com | Được thêm thành viên |
| | Thành viên thường | ba.nguyen@email.com | Không được thêm thành viên |
| Email thành viên mới | Hợp lệ | user@domain.com | Cho phép tạo thành viên |
| | Thiếu dấu . trong domain | user@domain | Từ chối, báo email không hợp lệ |
| | Thiếu @ | userdomain.com | Từ chối, báo email không hợp lệ |
| | Email đã tồn tại | ba.nguyen@email.com | Từ chối, báo email trùng |

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
| TC-32 | Verify successful return of a borrowed book | 1. Data has been reset. 2. User is logged in with an active member account. 3. The member has borrowed an available book in the current session. | 1. Log in as `dam.tran@email.com`. 2. Open the **Books** tab. 3. Borrow BOOK002 if it is available. 4. Open the **Borrow / Return** tab. 5. Select the borrow record for BOOK002. 6. Click **Return Book**. | Account: `dam.tran@email.com` / `password123`; Book: BOOK002 | - The system returns the book successfully. - The borrow record status changes to “Đã trả”. | REQ-05 | Happy Path, Scenario |
| TC-33 | Verify book status changes to “Có sẵn” after return | TC-32 has been completed successfully. | 1. After returning BOOK002, open the **Books** tab. 2. Search for BOOK002. 3. Observe the book status. | Book: BOOK002 | BOOK002 status changes back to “Có sẵn”. | REQ-05 | State Transition |
| TC-34 | Verify member cannot return another member’s borrowed book | 1. Data has been reset. 2. User is logged in as MEM002. | 1. Log in as `ba.nguyen@email.com`. 2. Open the **Borrow / Return** tab. 3. Check whether the borrow record of BOOK013 borrowed by MEM006 is visible. 4. If visible, try to return it. | Account: `ba.nguyen@email.com`; Other member’s book: BOOK013 | MEM002 must not be able to see or return BOOK013 borrowed by MEM006. | REQ-05, REQ-08 | Negative, Access Control |
| TC-35 | Verify overdue warning is displayed when returning an overdue book | 1. Data has been reset. 2. BR001 exists and is overdue. | 1. Log in as `ba.nguyen@email.com`. 2. Open the **Borrow / Return** tab. 3. Find BR001 / BOOK003. 4. Click **Return Book**. 5. Observe the message. | Account: `ba.nguyen@email.com`; Record: BR001; Book: BOOK003 | The system allows the return but displays an overdue warning. BOOK003 changes back to “Có sẵn”. | REQ-05 | BVA, Scenario |
| TC-36 | Verify librarian can trigger overdue checking | 1. Data has been reset. 2. User is on the login page. | 1. Log in as `librarian@library.com`. 2. Open the **Borrow / Return** tab or the area containing **Kiểm tra quá hạn**. 3. Click **Kiểm tra quá hạn**. 4. Observe the result. | Account: `librarian@library.com` / `admin123` | The system checks overdue records and updates records with dueDate ≤ current date to “Quá hạn”. | REQ-06 | BVA |
| TC-37 | Verify overdue record is marked as “Quá hạn” | 1. Data has been reset. 2. Librarian is logged in. | 1. Open the **Borrow / Return** tab. 2. Observe BR001 before overdue checking. 3. Click **Kiểm tra quá hạn**. 4. Observe BR001 again. | Record: BR001; dueDate: 15/09/2024 | BR001 is marked as “Quá hạn” because its due date is less than or equal to the current date. | REQ-06 | BVA |
| TC-38 | Verify member can see their own overdue record | 1. Data has been reset. 2. Librarian has clicked **Kiểm tra quá hạn**. | 1. Log in as librarian. 2. Click **Kiểm tra quá hạn**. 3. Log out. 4. Log in as `ba.nguyen@email.com`. 5. Open the **Borrow / Return** tab. 6. Observe BR001. | Account: `ba.nguyen@email.com`; Record: BR001 | MEM002 can see their own BR001 record with status “Quá hạn”. Records of other members are not shown. | REQ-06, REQ-08 | Access Control, Scenario |
| TC-39 | Verify librarian can add a new member with valid information | 1. Data has been reset. 2. Librarian is logged in. | 1. Log in as `librarian@library.com`. 2. Open the **Members** tab. 3. Click **Add Member**. 4. Enter valid full name, email, and phone number. 5. Click **Save** or **Add**. | Name: `Nguyễn Văn Mới`; Email: `nguyen.van.moi@example.com`; Phone: `0912345678` | The system creates a new member successfully. The new member appears in the member list. | REQ-07 | Happy Path, EP |
| TC-40 | Verify normal member cannot add new member | 1. Data has been reset. 2. User is logged in as a normal member. | 1. Log in as `ba.nguyen@email.com`. 2. Observe the navigation tabs/menu. 3. Check whether the **Members** tab or **Add Member** button is available. | Account: `ba.nguyen@email.com` / `password123` | Normal member cannot access the member management function and cannot add a new member. | REQ-07 | Access Control, Negative |
| TC-41 | Reject new member when email has no dot in domain | 1. Data has been reset. 2. Librarian is logged in. | 1. Open the **Members** tab. 2. Click **Add Member**. 3. Enter name, invalid email `user@domain`, and valid phone. 4. Click **Save** or **Add**. | Name: `Email Sai Domain`; Email: `user@domain`; Phone: `0912345678` | The system does not create the member and displays an invalid email error because the domain does not contain a dot. | REQ-07 | BVA, EP |
| TC-42 | Reject new member when email is missing @ | 1. Data has been reset. 2. Librarian is logged in. | 1. Open the **Members** tab. 2. Click **Add Member**. 3. Enter name, invalid email `userdomain.com`, and valid phone. 4. Click **Save** or **Add**. | Name: `Email Thieu A Cong`; Email: `userdomain.com`; Phone: `0912345678` | The system does not create the member and displays an invalid email error because the email does not contain `@`. | REQ-07 | EP, Negative |
| TC-43 | Reject new member when email already exists | 1. Data has been reset. 2. Librarian is logged in. | 1. Open the **Members** tab. 2. Click **Add Member**. 3. Enter a new name but use an existing email. 4. Click **Save** or **Add**. | Name: `Nguyễn Trùng Email`; Email: `ba.nguyen@email.com`; Phone: `0912345678` | The system does not create the member and displays an error that the email already exists. | REQ-07 | EP, Negative |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
