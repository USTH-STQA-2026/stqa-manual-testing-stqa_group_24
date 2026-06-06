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

### IDM — `<!-- Nhóm tự bổ sung cho REQ-05 đến REQ-08 -->`

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| `<!-- Nhóm tự điền -->` | | | |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->
### REQ-01: Đăng nhập / Login
| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | Test successful login with valid email and password | 1. User is on the login page. 2. Account already exists in the system. | 1. Enter a valid Email. 2. Enter a valid Password. 3. Click the "Login" button. | Email: `librarian@library.com`, Mật khẩu: `admin123` | - Redirected to the homepage successfully. - The AppBar accurately displays the username + role. | REQ-01 | Decision Table (True/True) |
| TC-02 | Test error message when entering an unregistered Email | User is on the login page. | 1. Enter a non-existent Email. 2. Enter any Password. 3. Click the "Login" button. | Email: `nobody@test.com`, Mật khẩu: `anything` | Displays error message: "Không tìm thấy thành viên". | REQ-01 | Decision Table (False/True) |
| TC-03 | Test error message when entering a correct Email but incorrect Password | 1. User is on the login page. 2. Email already exists in the system. | 1. Enter the correct Email. 2. Enter an incorrect Password. 3. Click the "Login" button. | Email: `ba.nguyen@email.com`, Mật khẩu: `wrongpassword` | Displays error message: "Mật khẩu không đúng". | REQ-01 | Decision Table (True/False) |
| TC-04 | Test error message when leaving both Email and Password blank | User is on the login page. | 1. Leave the Email field blank. 2. Leave the Password field blank. 3. Click the "Login" button. | Email: (Leave blank), Mật khẩu: (Leave blank) | Displays error message: "Vui lòng nhập email và mật khẩu". | REQ-01 | Decision Table (Blank/Blank) |
| TC-05 | Test error message when entering only Password and leaving Email blank | User is on the login page. | 1. Leave the Email field blank. 2. Enter any Password. 3. Click the "Login" button. | Email: (Leave blank), Mật khẩu: `anything` | Displays error message: "Vui lòng nhập email và mật khẩu". | REQ-01 | Equivalence Partitioning (Empty) |
| TC-06 | Test error message when entering only Email and leaving Password blank | User is on the login page. | 1. Enter a valid Email. 2. Leave the Password field blank. 3. Click the "Login" button. | Email: `librarian@library.com`, Mật khẩu: (Leave blank) | Displays error message: "Vui lòng nhập email và mật khẩu". | REQ-01 | Equivalence Partitioning (Empty) |
| TC-07 | Test error message when entering both an incorrect Email and incorrect Password | User is on the login page. | 1. Enter a non-existent Email. 2. Enter an incorrect Password. 3. Click the "Login" button. | Email: `nobody@test.com`, Mật khẩu: `wrongpassword` | Displays error message: "Không tìm thấy thành viên”. | REQ-01 | Decision Table (False/False) |
| TC-08 | <br><br>Verify successful borrowing for an active member with available borrowing slots and an available book | \- Logged in as MEM006(biet.hoang@email.com) (Status: Active, currently borrowing 1 books).            | 1\. Go to Books tab.<br><br>2\. Select book BOOK001.<br><br>3\. Click "Borrow". | \- Member: MEM006<br><br>\- Book ID: BOOK001<br><br>\- Book Status: Available                                       | \- System allows borrowing.<br><br>\- Due date is set to 14 days from the day the member start borrowing.<br><br>\- Book status transitions to "Borrowed". | REQ-04 | EP                  |

### REQ-04: Mượn sách / Borrow Book
| TC-09 | <br>Reject borrowing when the selected book is borrowed by another member                                     | \- Logged in as MEM006(biet.hoang@email.com) (Status: Active).                                         | 1\. Go to Books tab.<br><br>2\. Attempt to borrow book BOOK003.                 | \- Member: MEM006<br><br>\- Book ID: BOOK003<br><br>\- Book Status: Borrowed by MEM002                              | \- System denies borrowing.<br><br>\- Expected Error: "The book is currently unavailable (Already borrowed)."                                              | REQ-04 | Decision Table, EP  |
| TC-10 | <br>Reject borrowing if a book's status is "Lost"                                                             | \- Logged in as MEM006(biet.hoang@email.com) (Status: Active).                                         | 1\. Go to Books tab.<br><br>2\. Attempt to borrow book BOOK007.                 | \- Member: MEM006<br><br>\- Book ID: BOOK007<br><br>\- Book Status: Lost                                            | \- System denies borrowing<br><br>\- Expected Error: "The book is currently unavailable (Lost)."                                                           | REQ-04 | Decision Table, EP  |
| TC-11 | <br>Reject borrowing when the member account status is "Suspended"                                            | \- Logged in as MEM004(cu.le@email.com) (Status: Suspended).                                      | 1\. Go to Books tab.<br><br>2\. Select book BOOK001.<br><br>3\. Click "Borrow". | \- Member: MEM004<br><br>\- Book ID: BOOK001<br><br>\- Book Status: Available                                       | \- System denies borrowing<br><br>\- Expected Error: "The member's account is currently suspended." (Must not say expired).                                | REQ-04 | Decision Table, EP  |
| TC-12 | <br><br>Reject borrowing when the member account status is "Expired"                                          | \- Logged in as MEM005(binh.pham@email.com) (Status: Expired).                                        | 1\. Go to Books tab.<br><br>2\. Select book BOOK001.<br><br>3\. Click "Borrow". | \- Member: MEM005<br><br>\- Book ID: BOOK001<br><br>\- Book Status: Available                                       | \- System denies borrowing<br><br>\- Expected Error: "The member's account has expired."                                                                   | REQ-04 | Decision Table, EP  |
| TC-13 | <br>Reject borrowing when the member has already reached the maximum limit of 3 books                         | \- Logged in as a member who already has exactly 3 active borrows in the system. | 1\. Go to Books tab.<br><br>2\. Select book BOOK001.<br><br>3\. Click "Borrow". | \- Member: (MEM with 3 borrow records/3 books borrowed)<br><br>\- Book ID: BOOK001<br><br>\- Book Status: Available | \- System denies borrowing<br><br>\- Expected Error: "Member has reached the maximum limit of 3 books."                                                    | REQ-04 | Decision Table, BVA |
---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
