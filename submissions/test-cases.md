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

### IDM — View Book List (REQ-02)

| Characteristic | Partition | Representative Value | Expected Result |
|---|---|---|---|
| User role viewing book list | Librarian | `librarian@library.com` / `admin123` | The librarian can view the book list |
| | Member | `ba.nguyen@email.com` / `password123` | The member can view the book list |
| Book initial status | Available | BOOK001 | The book is displayed with status “Có sẵn” |
| | Borrowed | BOOK003 | The book is displayed with status “Đã mượn” |
| | Lost | BOOK007 | The book is displayed with status “Thất lạc” if the system supports displaying lost books |
| Book displayed information | Complete book information | BOOK001 | The system displays title, author, category, publication year, and status |

### IDM — Search and Filter Books (REQ-03)

| Characteristic | Partition | Representative Value | Expected Result |
|---|---|---|---|
| Search keyword type | Book title | `Flutter` | The system displays BOOK001 |
| | Author name | `Nguyễn Minh Đức` | The system displays BOOK001 and BOOK009 |
| | Non-existent keyword | `xyz_khong_ton_tai` | The system displays “Không tìm thấy sách” |
| Case sensitivity | Lowercase keyword | `flutter` | The system still displays BOOK001 |
| | Uppercase keyword | `FLUTTER` | The system still displays BOOK001 |
| Category filter | Existing category | `Công nghệ` | The system displays only books in the “Công nghệ” category |
| | Existing category | `Văn học` | The system displays only books in the “Văn học” category |

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

### IDM — Return Book (REQ-05)

| Characteristic | Partition | Representative Value | Expected Result |
|---|---|---|---|
| Borrow record ownership | Record belongs to the logged-in member | Logged-in member: MEM006; Borrow record: BR003; Book: BOOK013 | The member is allowed to return the book |
| | Record belongs to another member | Logged-in member: MEM002; Other member: MEM006; Borrow record: BR003; Book: BOOK013 | The member must not be allowed to view or return the book |
| Borrow record status | Currently borrowed | BR003 — BOOK013, status: Borrowing | The book can be returned |
| | Already returned | BR004 — BOOK005, status: Returned | The book should not be returned again as an active borrow |
| Book status after return | Borrowed book is returned | BOOK013 | The book status changes back to “Có sẵn” |
| Return timing | Overdue return | BR001 — BOOK003, due date: 15/09/2024 | The system displays an overdue warning when the book is returned |

### IDM — Overdue Handling (REQ-06)

| Characteristic | Partition | Representative Value | Expected Result |
|---|---|---|---|
| User role triggering overdue check | Librarian | `librarian@library.com` / `admin123` | The user can trigger overdue checking |
| Borrow record due date | dueDate ≤ current date | BR001 — due date: 15/09/2024 | The borrow record is marked as “Quá hạn” |
| | dueDate ≤ current date | BR003 — due date: 15/10/2024 | The borrow record is marked as “Quá hạn” if it is overdue at test time |
| Borrow record visibility after overdue check | Librarian views overdue records | Librarian account | The librarian can view all overdue records |
| | Member views own overdue record | MEM002 views BR001 | The member can see their own overdue record |

### IDM — Member Management (REQ-07)

| Characteristic | Partition | Representative Value | Expected Result |
|---|---|---|---|
| User role accessing member management | Librarian | `librarian@library.com` / `admin123` | The user can access member management and add a new member |
| | Normal member | `ba.nguyen@email.com` / `password123` | The user cannot access member management or add a new member |
| Email format | Valid email format | `user@domain.com` | The system allows creating a new member |
| | Missing dot in domain | `user@domain` | The system rejects the email as invalid |
| Email uniqueness | Existing email | `ba.nguyen@email.com` | The system rejects the email because it already exists |

### IDM — Borrow Record Lookup (REQ-08)

| Characteristic | Partition | Representative Value | Expected Result |
|---|---|---|---|
| User role viewing borrow records | Librarian | `librarian@library.com` / `admin123` | The librarian can view all borrow records |
| | Member | `ba.nguyen@email.com` / `password123` | The member can only view their own borrow records |
| Borrow record ownership | Own records | MEM002 views BR001 and BR004 | The system displays records belonging to MEM002 |
| | Other member’s records | MEM002 tries to view BR003 of MEM006 | The system must not display BR003 to MEM002 |
| Borrow record information | Required fields | BR001 | The record displays record ID, borrowed book, borrow date, due date, and status |


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
| TC-15 | Verify that the librarian can view the book list | 1. The data has been reset. 2. The user is on the login page. | 1. Log in with `librarian@library.com`. 2. Open the **Books** tab. 3. Observe the displayed book list. | Account: `librarian@library.com` / `admin123` | The librarian can view the book list. Each book displays title, author, category, publication year, and status. | REQ-02 | EP |
| TC-16 | Verify that a member can view the book list | 1. The data has been reset. 2. The user is on the login page. | 1. Log in with `ba.nguyen@email.com`. 2. Open the **Books** tab. 3. Observe the displayed book list. | Account: `ba.nguyen@email.com` / `password123` | The member can view the book list. Each book displays title, author, category, publication year, and status. | REQ-02 | EP |
| TC-17 | Verify that an available book is displayed with correct information | 1. The data has been reset. 2. The user has logged in successfully. | 1. Open the **Books** tab. 2. Find BOOK001. 3. Observe the displayed book information. | Book: BOOK001 — `Lập trình Flutter cơ bản` | BOOK001 displays title `Lập trình Flutter cơ bản`, author `Nguyễn Minh Đức`, category `Công nghệ`, publication year `2023`, and status `Có sẵn`. | REQ-02 | EP |
| TC-18 | Verify that a borrowed book is displayed with correct status | 1. The data has been reset. 2. The user has logged in successfully. | 1. Open the **Books** tab. 2. Find BOOK003. 3. Observe the book status. | Book: BOOK003 — `Kiểm thử phần mềm nhập môn` | BOOK003 is displayed with status `Đã mượn` because it is initially borrowed by MEM002. | REQ-02 | EP |
| TC-19 | Verify book search by title | 1. The data has been reset. 2. The user has logged in successfully. | 1. Open the **Books** tab. 2. Enter `Flutter` in the search box. 3. Observe the result list. | Keyword: `Flutter` | The system displays BOOK001 — `Lập trình Flutter cơ bản`. Unrelated books are not displayed. | REQ-03 | EP |
| TC-20 | Verify book search by author | 1. The data has been reset. 2. The user has logged in successfully. | 1. Open the **Books** tab. 2. Enter `Nguyễn Minh Đức` in the search box. 3. Observe the result list. | Keyword: `Nguyễn Minh Đức` | The system displays books written by Nguyễn Minh Đức, including BOOK001 and BOOK009. | REQ-03 | EP |
| TC-21 | Verify case-insensitive search using lowercase keyword | 1. The data has been reset. 2. The user has logged in successfully. | 1. Open the **Books** tab. 2. Enter lowercase keyword `flutter`. 3. Observe the result list. | Keyword: `flutter` | The system still displays BOOK001 — `Lập trình Flutter cơ bản`, even though the keyword is entered in lowercase. | REQ-03 | EP |
| TC-22 | Verify case-insensitive search using uppercase keyword | 1. The data has been reset. 2. The user has logged in successfully. | 1. Open the **Books** tab. 2. Enter uppercase keyword `FLUTTER`. 3. Observe the result list. | Keyword: `FLUTTER` | The system still displays BOOK001 — `Lập trình Flutter cơ bản`, even though the keyword is entered in uppercase. | REQ-03 | EP |
| TC-23 | Verify search with no matching result | 1. The data has been reset. 2. The user has logged in successfully. | 1. Open the **Books** tab. 2. Enter `xyz_khong_ton_tai` in the search box. 3. Observe the result list. | Keyword: `xyz_khong_ton_tai` | The system displays no books and shows the message `Không tìm thấy sách`. | REQ-03 | EP |
| TC-24 | Verify filtering books by the Technology category | 1. The data has been reset. 2. The user has logged in successfully. | 1. Open the **Books** tab. 2. Select or enter category `Công nghệ`. 3. Observe the result list. | Category: `Công nghệ` | The system displays only books in the `Công nghệ` category, such as BOOK001, BOOK002, BOOK003, BOOK005, BOOK008, BOOK009, BOOK010, and BOOK011. | REQ-03 | EP |
| TC-25 | Verify that the librarian can view all borrow records | 1. The data has been reset. 2. The user is on the login page. | 1. Log in with `librarian@library.com`. 2. Open the **Borrow / Return** tab. 3. View the borrow record list. 4. Observe whether records of all members are displayed. | Account: `librarian@library.com` / `admin123`; Records: BR001, BR002, BR003, BR004, BR005 | The librarian can view all borrow records of all members, including BR001, BR002, BR003, BR004, and BR005. Each record displays record ID, borrowed book, borrow date, due date, and status. | REQ-08 | Decision Table, EP |
| TC-26 | Verify that a member cannot view borrow records of another member | 1. The data has been reset. 2. The user is logged in as MEM002. | 1. Log in with `ba.nguyen@email.com`. 2. Open the **Borrow / Return** tab. 3. Open the borrow record lookup area if available. 4. Search for `MEM006`. 5. Observe whether BR003 is displayed. | Logged-in account: `ba.nguyen@email.com` / `password123`; Logged-in member: MEM002; Other member: MEM006; Record: BR003 | The system must not display BR003 to MEM002 because BR003 belongs to MEM006. A member can only view their own borrow records. | REQ-08 | Decision Table, EP |
| TC-32 | Verify that a member can return their own currently borrowed book | 1. The data has been reset. 2. The user is logged in as MEM006. 3. BR003 exists in the initial seed data and belongs to MEM006. | 1. Log in with `biet.hoang@email.com`. 2. Open the **Borrow / Return** tab. 3. Find borrow record BR003 for BOOK013. 4. Click **Return Book**. 5. Open the **Books** tab. 6. Check the status of BOOK013. | Account: `biet.hoang@email.com` / `password123`; Member: MEM006; Borrow record: BR003; Book: BOOK013 | - The system allows MEM006 to return BOOK013 because BR003 belongs to MEM006. - The borrow record changes to “Đã trả”. - BOOK013 changes back to “Có sẵn”. | REQ-05 | EP |
| TC-33 | Verify that the system displays an overdue warning when returning an overdue book | 1. The data has been reset. 2. BR001 exists in the initial seed data. 3. BR001 belongs to MEM002 and has due date 15/09/2024. | 1. Log in with `ba.nguyen@email.com`. 2. Open the **Borrow / Return** tab. 3. Find borrow record BR001 for BOOK003. 4. Click **Return Book**. 5. Observe the message displayed by the system. 6. Open the **Books** tab and check the status of BOOK003. | Account: `ba.nguyen@email.com` / `password123`; Member: MEM002; Borrow record: BR001; Book: BOOK003; Due date: 15/09/2024 | - The system allows the book to be returned. - The system displays an overdue warning because BR001 is overdue. - BOOK003 changes back to “Có sẵn”. | REQ-05 | BVA |
| TC-34 | Verify that a member cannot view or return another member’s borrowed book | 1. The data has been reset. 2. The user is logged in as MEM002. 3. BR003 belongs to MEM006, not MEM002. | 1. Log in with `ba.nguyen@email.com`. 2. Open the **Borrow / Return** tab. 3. Open the borrow record lookup area if available. 4. Search for `MEM006`. 5. Check whether BR003 is displayed. 6. If BR003 is displayed, check whether the **Return Book** action is available. | Logged-in account: `ba.nguyen@email.com` / `password123`; Logged-in member: MEM002; Other member: MEM006; Borrow record: BR003; Book: BOOK013 | The system must not display BR003 to MEM002 and must not allow MEM002 to return BOOK013 because BR003 belongs to MEM006. | REQ-05, REQ-08 | Decision Table, EP |
| TC-35 | Verify that the librarian can trigger overdue checking | 1. The data has been reset. 2. The user is on the login page. | 1. Log in with `librarian@library.com`. 2. Open the **Borrow / Return** tab or the area containing the **Check Overdue** button. 3. Click **Check Overdue**. 4. Observe the system response. | Account: `librarian@library.com` / `admin123`; Role: Librarian | The system checks overdue records and updates borrow records whose due date is less than or equal to the current date to “Quá hạn”. | REQ-06 | BVA |
| TC-36 | Verify that overdue borrow records are marked as “Quá hạn” | 1. The data has been reset. 2. The user is logged in with the librarian account. 3. BR001 and BR003 exist in the initial seed data. | 1. Log in with `librarian@library.com`. 2. Open the **Borrow / Return** tab. 3. Observe the status of BR001 and BR003 before overdue checking. 4. Click **Check Overdue**. 5. Observe the status of BR001 and BR003 again. | Account: `librarian@library.com` / `admin123`; BR001 due date: 15/09/2024; BR003 due date: 15/10/2024 | BR001 and BR003 are marked as “Quá hạn” if their due dates are less than or equal to the current date. | REQ-06 | BVA |
| TC-37 | Verify that the librarian can add a new member with a valid email format | 1. The data has been reset. 2. The user is logged in with the librarian account. | 1. Log in with `librarian@library.com`. 2. Open the **Members** tab. 3. Select **Add Member**. 4. Enter a non-empty full name. 5. Enter email `user@domain.com`. 6. Enter a phone number. 7. Click **Add Member**. | Account: `librarian@library.com` / `admin123`; Email: `user@domain.com` | The system creates the new member successfully because `user@domain.com` is a valid email format with `@` and a dot `.` in the domain part. | REQ-07 | EP |
| TC-38 | Verify that a normal member cannot access member management | 1. The data has been reset. 2. The user is logged in with a normal member account. | 1. Log in with `ba.nguyen@email.com`. 2. Observe the navigation menu or available tabs. 3. Check whether the **Members** tab or **Add Member** function is available. | Account: `ba.nguyen@email.com` / `password123`; Role: Member | A normal member cannot access the member management function and cannot add a new member. | REQ-07 | Decision Table, EP |
| TC-39 | Verify that the system rejects an email without a dot in the domain part | 1. The data has been reset. 2. The user is logged in with the librarian account. | 1. Log in with `librarian@library.com`. 2. Open the **Members** tab. 3. Select **Add Member**. 4. Enter a non-empty full name. 5. Enter email `user@domain`. 6. Enter a phone number. 7. Click **Add Member**. | Account: `librarian@library.com` / `admin123`; Email: `user@domain` | The system does not create the new member and displays an invalid email error because `user@domain` does not contain a dot `.` in the domain part. | REQ-07 | BVA, EP |
| TC-40 | Verify that the system rejects an existing email | 1. The data has been reset. 2. The user is logged in with the librarian account. 3. Email `ba.nguyen@email.com` already exists in the initial seed data. | 1. Log in with `librarian@library.com`. 2. Open the **Members** tab. 3. Select **Add Member**. 4. Enter a non-empty full name. 5. Enter email `ba.nguyen@email.com`. 6. Enter a phone number. 7. Click **Add Member**. | Account: `librarian@library.com` / `admin123`; Existing email: `ba.nguyen@email.com` | The system does not create the new member and displays an error message indicating that the email already exists or is duplicated. | REQ-07 | EP |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
