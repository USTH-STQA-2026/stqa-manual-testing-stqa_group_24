# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | Group 24 |
| **Ngày thực thi** | 19/05/2026 |
| **Trình duyệt** | Google Chrome |
| **Hệ điều hành** | Windows 11 |

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-32 | Return Book | The borrowed book is returned successfully and the borrow record changes to “Đã trả” | BOOK002 was initially “Có sẵn”. After borrowing, BOOK002 changed to “Đang mượn”. After returning the book, the system displayed “Trả sách thành công.” and borrow record BR006 appeared with status “Đã trả”. | Pass | ![TC-32 before borrowing BOOK002](./assets/TC-32-truoc-khi-muon-book002.png)<br>![TC-32 after borrowing BOOK002](./assets/TC-32-sau-khi-muon-book002.png)<br>![TC-32 return success BR006](./assets/TC-32-tra-sach-thanh-cong-br006.png) | - |
| TC-33 | Return Book | The system displays an overdue warning when an overdue book is returned | Member MEM002 returned borrow record BR001 for BOOK003, whose due date was 15/09/2024. After returning the book, BOOK003 changed back to “Có sẵn”, but no overdue warning was displayed. | Fail | ![TC-33 before returning BR001](./assets/TC-33-truoc-khi-tra-br001.png)<br>![TC-33 after returning BOOK003](./assets/TC-33-sau-khi-tra-book003-co-san.png) | BUG-06 |
| TC-34 | Return Book / Access Control | A member must not be able to view or return another member’s borrowed book | Member MEM002 searched for `MEM006` and was able to view borrow record BR003 of another member. The record also displayed a **Return Book** button. After the action, BOOK013 was shown as “Có sẵn”, indicating that the member could return another member’s book. | Fail | ![TC-34 member views MEM006 record](./assets/TC-34-thanh-vien-thay-phieu-cua-mem006.png)<br>![TC-34 BOOK013 becomes available](./assets/TC-34-book013-tro-ve-co-san.png) | BUG-07 |
| TC-35 | Overdue Handling | The librarian can click the overdue checking button and the system updates overdue records | After logging in with the librarian account and clicking **Kiểm tra sách quá hạn**, the system displayed the message “Đã cập nhật: 2 phiếu mượn quá hạn.” | Pass | ![TC-35 overdue check success](./assets/TC-35-kiem-tra-qua-han-thanh-cong.png) | - |
| TC-36 | Overdue Handling | Borrow records whose due date is less than or equal to the current date are marked as “Quá hạn” | Before overdue checking, BR001 and BR003 were in “Đang mượn” status. After clicking **Kiểm tra sách quá hạn**, BR001 and BR003 changed to “Quá hạn”. | Pass | ![TC-36 before overdue checking](./assets/TC-36-truoc-khi-kiem-tra-qua-han.png)<br>![TC-36 after overdue checking](./assets/TC-36-sau-khi-kiem-tra-qua-han.png) | - |
| TC-37 | Member Management | The librarian can add a new member with valid information | After entering full name `Nguyễn Văn Mới`, email `nguyen.van.moi@example.com`, and phone number `0912345678`, the system displayed “Email không hợp lệ.” and did not create the new member. | Fail | ![TC-37 valid email rejected](./assets/TC-37-valid-email-rejected.png) | BUG-03 |
| TC-38 | Member Management | A normal member cannot add a new member | After logging in with member account `ba.nguyen@email.com`, the interface only displayed the **Books** and **Borrow / Return** tabs. The **Members** tab and **Add Member** button were not available. | Pass | ![TC-38 member no member management tab](./assets/TC-38-member-no-member-management-tab.png) | - |
| TC-39 | Member Management | Email `user@domain` is rejected because it does not contain a dot in the domain part | After entering email `user@domain`, the system still displayed “Thêm thành viên thành công! Mã: MEM007”. | Fail | ![TC-39 invalid email accepted](./assets/TC-39-invalid-email-user-domain-accepted.png) | BUG-04 |
| TC-40 | Member Management | Existing email `ba.nguyen@email.com` is rejected because it is duplicated | After entering existing email `ba.nguyen@email.com`, the system displayed “Email không hợp lệ.” instead of an email duplication error. | Fail | ![TC-40 duplicate email wrong error](./assets/TC-40-duplicate-email-wrong-error.png) | BUG-05 |

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
