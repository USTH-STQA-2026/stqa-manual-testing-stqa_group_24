# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | GROUP 24 |
| **Ngày báo cáo** | 06/06/2026 |

---

## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | TC-11 |
| **REQ liên quan** | REQ-04 |
| **Mức độ** | Medium |
| **Người phát hiện** | Đoàn Quốc Việt |
| **Ngày phát hiện** | 27/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
System displays "Expired" error message instead of "Suspended" message when a suspended member attempts to borrow a book.

**Môi trường:**
- Trình duyệt: Firefox 150.0.3
- Hệ điều hành: Linux
- Ngôn ngữ giao diện: Tiếng Việt/English

**Điều kiện tiên quyết:**
The suspended user is at the Books tab and the data is refreshed.

**Bước tái hiện:**
1. Log into the library application using a suspended member account (e.g., Account: cu.le@email.com / Member ID: MEM004).<br>
2. Navigate to the Books tab.<br>
3. Select any available book (e.g., BOOK001 - Lập trình Flutter cơ bản) and click the "Borrow" button.<br>
4. Confirm the transaction in the confirmation pop-up window.

**Kết quả mong đợi:**
The system denies the borrowing request and displays the exact error message indicating account suspension: "The member's account is currently suspended."

**Kết quả thực tế:**
The system successfully blocks the transaction but displays an incorrect red error banner at the bottom of the screen stating: "Thành viên đã hết hạn. Không thể mượn sách." (Member has expired. Cannot borrow book.)

**Tác động:**
Directly violates the explicit business rule in REQ-04 (suspended ≠ expired). This misleads both the library staff and the member regarding the true operational status of the account, causing confusion on how to resolve the restriction (e.g., attempting subscription renewal instead of lifting a penalty).

**Minh chứng:**
![prove](./assets/REQ-04/11-3.png)

**Đề xuất xử lý:**
Update the backend verification logic or localization mapping for business rule constraints. Ensure that when checking member status, an account matching the Suspended flag triggers its dedicated warning string block instead of routing to the Expired message block.

---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | TC-13 |
| **REQ liên quan** | REQ-04 |
| **Mức độ** | High |
| **Người phát hiện** | Đoàn Quốc Việt |
| **Ngày phát hiện** | 27/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
System fails to enforce maximum limit, allowing a member holding 3 active books to borrow a 4th book successfully.

**Môi trường:**
- Trình duyệt: Firefox 150.0.3
- Hệ điều hành: Linux
- Ngôn ngữ giao diện: Tiếng Việt/English

**Điều kiện tiên quyết:**
- The database contains a member account configured to have exactly 3 active, unreturned borrow records (e.g., Status: "Borrowed"), thereby hitting the maximum allowed limit.<br>
- The user is at the Books tab.

**Bước tái hiện:**
1. Log into the library application using the member account that already holds 3 books.<br>
2. Navigate to the Books tab.<br>
3. Select any available book (e.g., status: "Available") and click the "Borrow" button.<br>
4. Confirm the transaction in the confirmation pop-up.

**Kết quả mong đợi:**
The system denies the borrowing request because the member has already reached the maximum limit of 3 borrowed books, and displays an error message stating: "Member has reached the maximum limit of 3 books."

**Kết quả thực tế:**
The system allows the borrowing transaction to proceed completely, updates the book's availability status, and displays a green success banner stating: "Mượn sách thành công!" (Borrow book successfully!).

**Tác động:**
Critical business rule violation. This off-by-one or missing conditional logic bypasses library inventory controls entirely, allowing users to borrow books beyond specified limits and draining available book resources for other members.

**Minh chứng:**
![](./assets/REQ-04/13-1.png)<br>
![](./assets/REQ=04/13-4.png)<br>
![](./assets/REQ=04/13-5.png)

**Đề xuất xử lý:**
Review the backend constraint validation inside the borrow processing controller. Ensure that a count query checking active loans handles strict inequality checks before saving the transaction to the database (e.g., verify that an if (activeLoans >= 3) rejection block handles the validation intercept properly prior to saving a new entry).

---

<!-- Copy template BUG trên để thêm BUG-03, BUG-04, ... cho mỗi TC Fail -->
