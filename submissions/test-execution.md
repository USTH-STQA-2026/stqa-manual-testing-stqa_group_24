# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | Group 24 |
| **Ngày thực thi** | 19/05/2026 |
| **Trình duyệt** | Firefox 150.0.3 |
| **Hệ điều hành** | Windows |

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Login | Redirected to the homepage successfully | Successfully redirected to the homepage and displayed username + role | Pass | ![Login Success Screen](./assets//REQ-01/Login-success.png) | - |
| TC-02 | Login | Displays error message: "Không tìm thấy thành viên". | Displayed error message under the email input field: "Không tìm thấy thành viên" | Pass | ![User Not Found](./assets/REQ-01/user-not-found.png) | - |
| TC-03 | Login | Displays error message: "Mật khẩu không đúng". | Displayed error message under the email input field: "Mật khẩu không đúng" | Pass | ![Incorrect Password](./assets/REQ-01/Incorrect-password.png) | - |
| TC-04 | Login | Displays error message: "Vui lòng nhập email và mật khẩu". | Displayed error message under the email input field: "Vui lòng nhập email và mật khẩu" | Pass | ![Blank Email and Pass](./assets/REQ-01/Blank-email-pass.png) | - |
| TC-05 | Login | Displays error message: "Vui lòng nhập email và mật khẩu". | Displayed error message under the email input field: "Vui lòng nhập email và mật khẩu" | Pass | ![Laziness took over](./assets/REQ-01/Blank-email.png) | - |
| TC-06 | Login | Displays error message: "Vui lòng nhập email và mật khẩu". | Displayed error message under the email input field: "Vui lòng nhập email và mật khẩu" | Pass | ![](./assets/REQ-01/Blank-pass.png) | - |
| TC-07 | Login | Displays error message: "Không tìm thấy thành viên". | Displayed error message under the email input field: "Không tìm thấy thành viên" | Pass | ![](./assets/REQ-01/Wrong-Email-Pass.png) | - |
| TC-08 | Borrow Book | Successful book borrowing with correct status transition and 14-day loan period calculation.                         | \- The member borrow BOOK001 succesfully.<br><br>\- Book status transitions to "Borrowed".<br><br>\- A 14-day loan period was added on the day MEM006 started borrowing BOOK001.<br><br>\- A green banner at the bottom of the screen stating: "Mượn sách thành công!" | Pass       | ![](./assets/REQ-04/08-1.png)<br>![](./assets/REQ-04/08-2.png)<br>![](./assets/REQ-04/08-3.png)<br>![](./assets/REQ-04/08-4.png) | \-     |
| TC-09 | Borrow Book | The system denies the borrowing request if the book is unavailable                                                   | The system displays a disabled button labeled 'Borrowed' next to book BOOK003, preventing the user from triggering a borrowing request.                                                                                                                                | Pass       | ![](./assets/REQ-04/09-1.png) | \-     |
| TC-10 | Borrow Book | The system denies the borrowing request if the book is lost                                                          | The system displays a disabled button labeled 'Lost' next to book BOOK007, preventing the user from triggering a borrowing request.                                                                                                                                    | Pass       | ![](./assets/REQ-04/10-1.png) | \-     |
| TC-11 | Borrow Book | The system denies the borrowing request if the member status is suspended                                            | The system displays a red error banner at the bottom of the screen stating: 'Thành viên đã hết hạn. Không thể mượn sách.' (Member has expired. Cannot borrow book.)                                                                                                    | Fail       | ![](./assets/REQ-04/11-1.png)<br>![](./assets/REQ-04/11-2.png)<br>![](./assets/REQ-04/11-3.png) | BUG-01 |
| TC-12 | Borrow Book | The system denies the borrowing request if the member status is expired                                              | The system displays a red error banner at the bottom of the screen stating: 'Thành viên đã hết hạn. Không thể mượn sách.' (Member has expired. Cannot borrow book.)                                                                                                    | Pass       | ![](./assets/REQ-04/12-1.png)<br>![](./assets/REQ-04/12-2.png)<br>![](./assets/REQ-04/12-3.png) | \-     |
| TC-13 | Borrow Book | The system denies the borrowing request because the member has already reached the maximum limit of 3 borrowed books | The system allows the borrowing transaction to proceed and displays a green banner stating: "Mượn sách thành công!".                                                                                                                                                   | Fail       | ![](./assets/REQ-04/13-1.png)<br>![](./assets/REQ-04/13-2.png)<br>![](./assets/REQ-04/13-3.png)<br>![](./assets/REQ-04/13-4.png)<br>![](./assets/REQ-04/13-5.png) | BUG-02 |
| TC-14 | View Book List | The user can view the book list with complete book information | After logging in as `ba.nguyen@email.com`, the Books tab displayed the book list. Each visible book showed title, author, category, publication year, and status. | Pass | ![TC-14 member view book list](./assets/REQ-02/TC-14-member-view-book-list.png) | - |
| TC-15 | View Book List | Books with different initial statuses are displayed correctly | BOOK001 was displayed as `Có sẵn`, BOOK003 was displayed as `Đang mượn`, and BOOK007 was displayed as `Thất lạc`. | Pass | ![TC-15 status available borrowed](./assets/REQ-02/TC-15-status-available-borrowed.png)<br>![TC-15 status lost](./assets/REQ-02/TC-15-status-lost.png) | - |
| TC-16 | View Book List / Return Book | Book status updates immediately after returning a borrowed book | After logging in as MEM006 and returning BOOK013 from BR003, the system displayed `Trả sách thành công.`. Then BOOK013 changed back to `Có sẵn` in the Books tab. | Pass | ![TC-16 return BOOK013 success](./assets/REQ-02/TC-16-return-book013-success.png)<br>![TC-16 BOOK013 available after return](./assets/REQ-02/TC-16-book013-available-after-return.png) | - |
| TC-17 | Search and Filter Books | Searching by book title displays the matching book | Searching `Flutter` displayed BOOK001 — `Lập trình Flutter cơ bản`. | Pass | ![TC-17 search title Flutter](./assets/REQ-03/TC-17-search-title-flutter.png) | - |
| TC-18 | Search and Filter Books | Searching by author displays matching books | Searching `Nguyễn Minh Đức` displayed BOOK001 and BOOK009, both written by Nguyễn Minh Đức. | Pass | ![TC-18 search author Nguyen Minh Duc](./assets/REQ-03/TC-18-search-author-nguyen-minh-duc.png) | - |
| TC-19 | Search and Filter Books | Search is case-insensitive for lowercase keyword | Searching lowercase `flutter` still displayed BOOK001 — `Lập trình Flutter cơ bản`. | Pass | ![TC-19 search lowercase flutter](./assets/REQ-03/TC-19-search-lowercase-flutter.png) | - |
| TC-20 | Search and Filter Books | Search is case-insensitive for uppercase keyword | Searching uppercase `FLUTTER` still displayed BOOK001 — `Lập trình Flutter cơ bản`. | Pass | ![TC-20 search uppercase FLUTTER](./assets/REQ-03/TC-20-search-uppercase-flutter.png) | - |
| TC-21 | Search and Filter Books | Searching with no matching result shows no-result message | Searching `xyz_khong_ton_tai` displayed no books and showed the message `Không tìm thấy sách nào.` | Pass | ![TC-21 search no result](./assets/REQ-03/TC-21-search-no-result.png) | - |
| TC-22 | Search and Filter Books | Filtering by Technology category displays only Technology books | Filtering by `Công nghệ` displayed books in the Technology category, such as BOOK001, BOOK002, BOOK003, BOOK005, and BOOK008. | Pass | ![TC-22 filter Cong nghe](./assets/REQ-03/TC-22-filter-cong-nghe.png) | - |

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
