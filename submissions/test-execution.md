# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | Group 24 |
| **Ngày thực thi** | 19/05/2026 |
| **Trình duyệt** | Firefox 150.0.3 |
| **Hệ điều hành** | Linux |

---

## Kết quả chi tiết

### REQ-01: Login

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Login | Redirected to the homepage successfully | Successfully redirected to the homepage and displayed username + role | Pass | ![Login Success Screen](./assets//REQ-01/Login-success.png) | - |
| TC-02 | Login | Displays error message: "Không tìm thấy thành viên". | Displayed error message under the email input field: "Không tìm thấy thành viên" | Pass | ![User Not Found](./assets/REQ-01/user-not-found.png) | - |
| TC-03 | Login | Displays error message: "Mật khẩu không đúng". | Displayed error message under the email input field: "Mật khẩu không đúng" | Pass | ![Incorrect Password](./assets/REQ-01/Incorrect-password.png) | - |
| TC-04 | Login | Displays error message: "Vui lòng nhập email và mật khẩu". | Displayed error message under the email input field: "Vui lòng nhập email và mật khẩu" | Pass | ![Blank Email and Pass](./assets/REQ-01/Blank-email-pass.png) | - |
| TC-05 | Login | Displays error message: "Vui lòng nhập email và mật khẩu". | Displayed error message under the email input field: "Vui lòng nhập email và mật khẩu" | Pass | ![Laziness took over](./assets/REQ-01/Blank-email.png) | - |
| TC-06 | Login | Displays error message: "Vui lòng nhập email và mật khẩu". | Displayed error message under the email input field: "Vui lòng nhập email và mật khẩu" | Pass | ![](./assets/REQ-01/Blank-pass.png) | - |
| TC-07 | Login | Displays error message: "Không tìm thấy thành viên". | Displayed error message under the email input field: "Không tìm thấy thành viên" | Pass | ![](./assets/REQ-01/Wrong-Email-Pass.png) | - |

### REQ-04: Borrow Book

| TC-08 | Borrow Book | Successful book borrowing with correct status transition and 14-day loan period calculation.                         | \- The member borrow BOOK001 succesfully.<br><br>\- Book status transitions to "Borrowed".<br><br>\- A 14-day loan period was added on the day MEM006 started borrowing BOOK001.<br><br>\- A green banner at the bottom of the screen stating: "Mượn sách thành công!" | Pass       | ![](./assets/REQ-04/08-1.png)<br>![](./assets/REQ-04/08-2.png)<br>![](./assets/REQ-04/08-3.png)<br>![](./assets/REQ-04/08-4.png) | \-     |
| TC-09 | Borrow Book | The system denies the borrowing request if the book is unavailable                                                   | The system displays a disabled button labeled 'Borrowed' next to book BOOK003, preventing the user from triggering a borrowing request.                                                                                                                                | Pass       | ![](./assets/REQ-04/09-1.png) | \-     |
| TC-10 | Borrow Book | The system denies the borrowing request if the book is lost                                                          | The system displays a disabled button labeled 'Lost' next to book BOOK007, preventing the user from triggering a borrowing request.                                                                                                                                    | Pass       | ![](./assets/REQ-04/10-1.png) | \-     |
| TC-11 | Borrow Book | The system denies the borrowing request if the member status is suspended                                            | The system displays a red error banner at the bottom of the screen stating: 'Thành viên đã hết hạn. Không thể mượn sách.' (Member has expired. Cannot borrow book.)                                                                                                    | Fail       | ![](./assets/REQ-04/11-1.png)<br>![](./assets/REQ-04/11-2.png)<br>![](./assets/REQ-04/11-3.png) | BUG-01 |
| TC-12 | Borrow Book | The system denies the borrowing request if the member status is expired                                              | The system displays a red error banner at the bottom of the screen stating: 'Thành viên đã hết hạn. Không thể mượn sách.' (Member has expired. Cannot borrow book.)                                                                                                    | Pass       | ![](./assets/REQ-04/12-1.png)<br>![](./assets/REQ-04/12-2.png)<br>![](./assets/REQ-04/12-3.png) | \-     |
| TC-13 | Borrow Book | The system denies the borrowing request because the member has already reached the maximum limit of 3 borrowed books | The system allows the borrowing transaction to proceed and displays a green banner stating: "Mượn sách thành công!".                                                                                                                                                   | Fail       | ![](./assets/REQ-04/13-1.png)<br>![](./assets/REQ-04/13-2.png)<br>![](./assets/REQ-04/13-3.png)<br>![](./assets/REQ-04/13-4.png)<br>![](./assets/REQ-04/13-5.png) | BUG-02 |
---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | `<!-- số -->` |
| Pass | `<!-- số -->` |
| Fail | `<!-- số -->` |
| Blocked | `<!-- số -->` |
| Not Run | `<!-- số -->` |
| **Tỷ lệ Pass** | `<!-- xx% -->` |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| | | | | |
