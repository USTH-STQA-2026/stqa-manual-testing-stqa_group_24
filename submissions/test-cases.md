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
| TC-01 | Test successful login with valid email and password | 1. User is on the login page. 2. Account already exists in the system. | 1. Enter a valid Email. 2. Enter a valid Password. 3. Click the "Login" button. | Email: `librarian@library.com`, Mật khẩu: `admin123` | - Redirected to the homepage successfully. - The AppBar accurately displays the username + role. | REQ-01 | Decision Table (True/True) |
| TC-02 | Test error message when entering an unregistered Email | User is on the login page. | 1. Enter a non-existent Email. 2. Enter any Password. 3. Click the "Login" button. | Email: `nobody@test.com`, Mật khẩu: `anything` | Displays error message: "Không tìm thấy thành viên". | REQ-01 | Decision Table (False/True) |
| TC-03 | Test error message when entering a correct Email but incorrect Password | 1. User is on the login page. 2. Email already exists in the system. | 1. Enter the correct Email. 2. Enter an incorrect Password. 3. Click the "Login" button. | Email: `ba.nguyen@email.com`, Mật khẩu: `wrongpassword` | Displays error message: "Mật khẩu không đúng". | REQ-01 | Decision Table (True/False) |
| TC-04 | Test error message when leaving both Email and Password blank | User is on the login page. | 1. Leave the Email field blank. 2. Leave the Password field blank. 3. Click the "Login" button. | Email: (Leave blank), Mật khẩu: (Leave blank) | Displays error message: "Vui lòng nhập email và mật khẩu". | REQ-01 | Decision Table (Blank/Blank) |
| TC-05 | Test error message when entering only Password and leaving Email blank | User is on the login page. | 1. Leave the Email field blank. 2. Enter any Password. 3. Click the "Login" button. | Email: (Leave blank), Mật khẩu: `anything` | Displays error message: "Vui lòng nhập email và mật khẩu". | REQ-01 | Equivalence Partitioning (Empty) |
| TC-06 | Test error message when entering only Email and leaving Password blank | User is on the login page. | 1. Enter a valid Email. 2. Leave the Password field blank. 3. Click the "Login" button. | Email: `librarian@library.com`, Mật khẩu: (Leave blank) | Displays error message: "Vui lòng nhập email và mật khẩu". | REQ-01 | Equivalence Partitioning (Empty) |
| TC-07 | Test error message when entering both an incorrect Email and incorrect Password | User is on the login page. | 1. Enter a non-existent Email. 2. Enter an incorrect Password. 3. Click the "Login" button. | Email: `nobody@test.com`, Mật khẩu: `wrongpassword` | Displays error message: "Không tìm thấy thành viên”. | REQ-01 | Decision Table (False/False) |
| TC-08 | <br><br>Verify successful borrowing for an active member with available borrowing slots and an available book | \- Logged in as MEM006 (Status: Active, currently borrowing 1 books).            | 1\. Go to Books tab.<br><br>2\. Select book BOOK001.<br><br>3\. Click "Borrow". | \- Member: MEM006<br><br>\- Book ID: BOOK001<br><br>\- Book Status: Available                                       | \- System allows borrowing.<br><br>\- Due date is set to 14 days from the day the member start borrowing.<br><br>\- Book status transitions to "Borrowed". | REQ-04 | EP                  |
| TC-09 | <br>Reject borrowing when the selected book is borrowed by another member                                     | \- Logged in as MEM006 (Status: Active).                                         | 1\. Go to Books tab.<br><br>2\. Attempt to borrow book BOOK003.                 | \- Member: MEM006<br><br>\- Book ID: BOOK003<br><br>\- Book Status: Borrowed by MEM002                              | \- System denies borrowing.<br><br>\- Expected Error: "The book is currently unavailable (Already borrowed)."                                              | REQ-04 | Decision Table, EP  |
| TC-10 | <br>Reject borrowing if a book's status is "Lost"                                                             | \- Logged in as MEM006 (Status: Active).                                         | 1\. Go to Books tab.<br><br>2\. Attempt to borrow book BOOK007.                 | \- Member: MEM006<br><br>\- Book ID: BOOK007<br><br>\- Book Status: Lost                                            | \- System denies borrowing<br><br>\- Expected Error: "The book is currently unavailable (Lost)."                                                           | REQ-04 | Decision Table, EP  |
| TC-11 | <br>Reject borrowing when the member account status is "Suspended"                                            | \- Logged in as MEM004 (Status: Suspended).                                      | 1\. Go to Books tab.<br><br>2\. Select book BOOK001.<br><br>3\. Click "Borrow". | \- Member: MEM004<br><br>\- Book ID: BOOK001<br><br>\- Book Status: Available                                       | \- System denies borrowing<br><br>\- Expected Error: "The member's account is currently suspended." (Must not say expired).                                | REQ-04 | Decision Table, EP  |
| TC-12 | <br><br>Reject borrowing when the member account status is "Expired"                                          | \- Logged in as MEM005 (Status: Expired).                                        | 1\. Go to Books tab.<br><br>2\. Select book BOOK001.<br><br>3\. Click "Borrow". | \- Member: MEM005<br><br>\- Book ID: BOOK001<br><br>\- Book Status: Available                                       | \- System denies borrowing<br><br>\- Expected Error: "The member's account has expired."                                                                   | REQ-04 | Decision Table, EP  |
| TC-13 | <br>Reject borrowing when the member has already reached the maximum limit of 3 books                         | \- Logged in as a member who already has exactly 3 active borrows in the system. | 1\. Go to Books tab.<br><br>2\. Select book BOOK001.<br><br>3\. Click "Borrow". | \- Member: (MEM with 3 borrow records/3 books borrowed)<br><br>\- Book ID: BOOK001<br><br>\- Book Status: Available | \- System denies borrowing<br><br>\- Expected Error: "Member has reached the maximum limit of 3 books."                                                    | REQ-04 | Decision Table, BVA |
| TC-32 | Verify successful return of a currently borrowed book | 1. The data has been reset. 2. The user is logged in with an active member account. 3. The member has borrowed an available book in the current session. | 1. Log in with `dam.tran@email.com`. 2. Open the **Books** tab. 3. Borrow BOOK002 if it is currently “Có sẵn”. 4. Open the **Borrow / Return** tab. 5. Select the borrow record of BOOK002. 6. Click **Return Book**. 7. Go back to the **Books** tab and check the status of BOOK002. | Account: `dam.tran@email.com` / `password123`; Book: BOOK002 | - The system returns the book successfully. - The borrow record of BOOK002 changes to “Đã trả”. - BOOK002 changes back to “Có sẵn”. | REQ-05 | EP |
| TC-33 | Verify overdue warning when returning an overdue book | 1. The data has been reset. 2. BR001 exists in the initial seed data and is overdue. | 1. Log in with `ba.nguyen@email.com`. 2. Open the **Borrow / Return** tab. 3. Find BR001 or BOOK003. 4. Click **Return Book**. 5. Observe the message after returning the book. | Account: `ba.nguyen@email.com` / `password123`; Borrow record: BR001; Book: BOOK003 | - The system allows the book to be returned. - The system displays an overdue warning. - BOOK003 changes back to “Có sẵn”. | REQ-05 | BVA |
| TC-34 | Verify that a member cannot return another member’s borrowed book | 1. The data has been reset. 2. The user is logged in as MEM002. | 1. Log in with `ba.nguyen@email.com`. 2. Open the **Borrow / Return** tab. 3. Check whether the borrow record of BOOK013 borrowed by MEM006 is visible. 4. If the system allows the action, try to return BOOK013. | Account: `ba.nguyen@email.com`; Another member’s book: BOOK013 | MEM002 must not be able to view or return BOOK013 because this book belongs to a borrow record of MEM006. | REQ-05, REQ-08 | Decision Table, EP |
| TC-35 | Verify that the librarian can perform overdue checking | 1. The data has been reset. 2. The user is on the login page. | 1. Log in with `librarian@library.com`. 2. Open the **Borrow / Return** tab or the area containing the **Check Overdue** button. 3. Click **Check Overdue**. 4. Observe the system response. | Account: `librarian@library.com` / `admin123` | The system checks overdue records and updates borrow records whose due date is less than or equal to the current date to “Quá hạn”. | REQ-06 | BVA |
| TC-36 | Verify that overdue borrow records are marked as “Quá hạn” | 1. The data has been reset. 2. The user is logged in with the librarian account. | 1. Log in as the librarian. 2. Open the **Borrow / Return** tab. 3. Observe the status of BR001 before overdue checking. 4. Click **Check Overdue**. 5. Observe the status of BR001 again. | Borrow record: BR001; Due date: 15/09/2024. Borrow record: BR003; Due date: 15/10/2024. | BR001 is marked as “Quá hạn”. If the system contains other active borrow records whose due date is less than or equal to the current date, those records are also marked as “Quá hạn”. | REQ-06 | BVA |
| TC-37 | Verify that the librarian can add a new member with valid information | 1. The data has been reset. 2. The user is logged in with the librarian account. | 1. Log in with `librarian@library.com`. 2. Open the **Members** tab. 3. Select **Add Member**. 4. Enter a valid full name, email, and phone number. 5. Click **Save** or **Add**. | Full name: `Nguyễn Văn Mới`; Email: `nguyen.van.moi@example.com`; Phone: `0912345678` | The system creates the new member successfully. Member `Nguyễn Văn Mới` appears in the member list. | REQ-07 | EP |
| TC-38 | Verify that a normal member cannot add a new member | 1. The data has been reset. 2. The user is logged in with a normal member account. | 1. Log in with `ba.nguyen@email.com`. 2. Observe the navigation menu or available function tabs. 3. Check whether the **Members** tab or **Add Member** button is available. | Account: `ba.nguyen@email.com` / `password123` | A normal member cannot access member management and cannot add a new member. | REQ-07 | Decision Table, EP |
| TC-39 | Verify that the system rejects an email without a dot in the domain | 1. The data has been reset. 2. The user is logged in with the librarian account. | 1. Log in as the librarian. 2. Open the **Members** tab. 3. Select **Add Member**. 4. Enter full name `Email Sai Domain`. 5. Enter email `user@domain`. 6. Enter phone number `0912345678`. 7. Click **Save** or **Add**. | Full name: `Email Sai Domain`; Email: `user@domain`; Phone: `0912345678` | The system does not create the new member and displays an invalid email error because the email is missing a dot `.` in the domain part. | REQ-07 | BVA, EP |
| TC-40 | Verify that the system rejects an already existing email | 1. The data has been reset. 2. The user is logged in with the librarian account. | 1. Log in as the librarian. 2. Open the **Members** tab. 3. Select **Add Member**. 4. Enter full name `Nguyễn Trùng Email`. 5. Enter existing email `ba.nguyen@email.com`. 6. Enter phone number `0912345678`. 7. Click **Save** or **Add**. | Full name: `Nguyễn Trùng Email`; Email: `ba.nguyen@email.com`; Phone: `0912345678` | The system does not create the new member and displays an error message indicating that the email already exists or is duplicated. | REQ-07 | EP |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
