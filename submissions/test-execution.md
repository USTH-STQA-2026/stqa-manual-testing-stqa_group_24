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

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Login | Redirected to the homepage successfully | Successfully redirected to the homepage and displayed username + role | Pass | ![Login Success Screen](./assets/Login-success.png) | - |
| TC-02 | Login | Displays error message: "Không tìm thấy thành viên". | Displayed error message under the email input field: "Không tìm thấy thành viên" | Pass | ![User Not Found](./assets/user-not-found.png) | - |
| TC-03 | Login | Displays error message: "Mật khẩu không đúng". | Displayed error message under the email input field: "Mật khẩu không đúng" | Pass | ![Incorrect Password](./assets/Incorrect-password.png) | - |
| TC-04 | Login | Displays error message: "Vui lòng nhập email và mật khẩu". | Displayed error message under the email input field: "Vui lòng nhập email và mật khẩu" | Pass | ![Blank Email and Pass](./assets/Blank-email-pass.png) | - |
| TC-05 | Login | Displays error message: "Vui lòng nhập email và mật khẩu". | Displayed error message under the email input field: "Vui lòng nhập email và mật khẩu" | Pass | ![Laziness took over](./assets/Blank-email.png) | - |
| TC-06 | Login | Displays error message: "Vui lòng nhập email và mật khẩu". | Displayed error message under the email input field: "Vui lòng nhập email và mật khẩu" | Pass | ![](./assets/Blank-pass.png) | - |
| TC-07 | Login | Displays error message: "Không tìm thấy thành viên". | Displayed error message under the email input field: "Không tìm thấy thành viên" | Pass | ![](./assets/Wrong-Email-Pass.png) | - |

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
