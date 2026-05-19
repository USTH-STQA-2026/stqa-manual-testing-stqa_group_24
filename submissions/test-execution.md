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
| TC-01 | Đăng nhập | Chuyển hướng đến trang chủ thành công | Thành công chuyển hướng đến trang chủ và hiện tên người dùng + vai trò | Pass | ![Login Success Screen](./assets/Login-success.png) | - |
| TC-02 | Đăng nhập | Hiển thị thông báo lỗi: "Không tìm thấy thành viên". | Hiện thông báo lỗi dưới phần nhập email: "Không tìm thấy thành viên" | Pass | ![User Not Found](./assets/user-not-found.png) | - |
| TC-03 | Đăng nhập | Hiển thị thông báo lỗi: "Mật khẩu không đúng". | Hiện thông báo lỗi dưới phần nhập email: "Mật khẩu không đúng" | Pass |![Incorrect Password](./assets/Incorrect-password.png) | - |
| TC-04 | Đăng nhập | Hiển thị thông báo lỗi: "Vui lòng nhập email và mật khẩu". | Hiện thông báo lỗi dưới phần nhập email: "Vui lòng nhập email và mật khẩu" | Pass | ![Blank Email and Pass](./assets/Blank-email-pass.png) | - |
| TC-05 | Đăng nhập | Hiển thị thông báo lỗi: "Vui lòng nhập email và mật khẩu". | Hiện thông báo lỗi dưới phần nhập email: "Vui lòng nhập email và mật khẩu" | Pass | ![Laziness took over](./assets/Blank-email.png) | - | 
| TC-06 | Đăng nhập | Hiển thị thông báo lỗi: "Vui lòng nhập email và mật khẩu". | Hiện thông báo lỗi dưới phần nhập email: "Vui lòng nhập email và mật khẩu" | Pass | ![](./assets/Blank-pass.png) | - |
| TC-07 | Đăng nhập | Hiển thị thông báo lỗi: "Không tìm thấy thành viên". | Hiện thông báo lỗi dưới phần nhập email: "Không tìm thấy thành viên" | Pass | ![](./assets/Wrong-Email-Pass.png) | - |

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
