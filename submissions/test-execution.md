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
| TC-01 | Đăng nhập | Chuyển hướng đến trang chủ thành công | Thành công chuyển hướng đến trang chủ và hiện tên người dùng + vai trò | Pass | ![Login Success Screen](./assets/Login-success.png) | - |
| TC-02 | Đăng nhập | Hiển thị thông báo lỗi: "Không tìm thấy thành viên". | Hiện thông báo lỗi dưới phần nhập email: "Không tìm thấy thành viên" | Pass | ![User Not Found](./assets/user-not-found.png) | - |
| TC-03 | Đăng nhập | Hiển thị thông báo lỗi: "Mật khẩu không đúng". | Hiện thông báo lỗi dưới phần nhập email: "Mật khẩu không đúng" | Pass |![Incorrect Password](./assets/Incorrect-password.png) | - |
| TC-04 | Đăng nhập | Hiển thị thông báo lỗi: "Vui lòng nhập email và mật khẩu". | Hiện thông báo lỗi dưới phần nhập email: "Vui lòng nhập email và mật khẩu" | Pass | ![Blank Email and Pass](./assets/Blank-email-pass.png) | - |
| TC-05 | Đăng nhập | Hiển thị thông báo lỗi: "Vui lòng nhập email và mật khẩu". | Hiện thông báo lỗi dưới phần nhập email: "Vui lòng nhập email và mật khẩu" | Pass | ![Laziness took over](./assets/Blank-email.png) | - | 
| TC-06 | Đăng nhập | Hiển thị thông báo lỗi: "Vui lòng nhập email và mật khẩu". | Hiện thông báo lỗi dưới phần nhập email: "Vui lòng nhập email và mật khẩu" | Pass | ![](./assets/Blank-pass.png) | - |
| TC-07 | Đăng nhập | Hiển thị thông báo lỗi: "Không tìm thấy thành viên". | Hiện thông báo lỗi dưới phần nhập email: "Không tìm thấy thành viên" | Pass | ![](./assets/Wrong-Email-Pass.png) | - |
| TC-32 | Return Book | Return borrowed book successfully | `<!-- ghi kết quả thực tế sau khi chạy -->` | Pass/Fail | `<!-- ảnh nếu có -->` | `<!-- BUG-xx nếu Fail, nếu không thì - -->` |
| TC-33 | Return Book | Book status changes back to “Có sẵn” after return | `<!-- ghi kết quả thực tế -->` | Pass/Fail | `<!-- ảnh nếu có -->` | - |
| TC-34 | Return Book / Borrow Record Lookup | Member cannot return another member’s borrowed book | `<!-- ghi kết quả thực tế -->` | Pass/Fail | `<!-- ảnh nếu có -->` | - |
| TC-35 | Return Book | Overdue warning is displayed when returning overdue book | `<!-- ghi kết quả thực tế -->` | Pass/Fail | `<!-- ảnh nếu có -->` | - |
| TC-36 | Overdue Handling | Librarian can trigger overdue checking | `<!-- ghi kết quả thực tế -->` | Pass/Fail | `<!-- ảnh nếu có -->` | - |
| TC-37 | Overdue Handling | Overdue record is marked as “Quá hạn” | `<!-- ghi kết quả thực tế -->` | Pass/Fail | `<!-- ảnh nếu có -->` | - |
| TC-38 | Overdue Handling | Member can see their own overdue record | `<!-- ghi kết quả thực tế -->` | Pass/Fail | `<!-- ảnh nếu có -->` | - |
| TC-39 | Member Management | Librarian can add a valid new member | `<!-- ghi kết quả thực tế -->` | Pass/Fail | `<!-- ảnh nếu có -->` | - |
| TC-40 | Member Management | Normal member cannot add new member | `<!-- ghi kết quả thực tế -->` | Pass/Fail | `<!-- ảnh nếu có -->` | - |
| TC-41 | Member Management | Reject email without dot in domain | `<!-- ghi kết quả thực tế -->` | Pass/Fail | `<!-- ảnh nếu có -->` | - |
| TC-42 | Member Management | Reject email missing @ | `<!-- ghi kết quả thực tế -->` | Pass/Fail | `<!-- ảnh nếu có -->` | - |
| TC-43 | Member Management | Reject duplicated email | `<!-- ghi kết quả thực tế -->` | Pass/Fail | `<!-- ảnh nếu có -->` | - |

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
