# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | `<!-- Tên nhóm -->` |
| **Ngày báo cáo** | `<!-- DD/MM/YYYY -->` |

---

## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | `<!-- TC-xx -->` |
| **REQ liên quan** | `<!-- REQ-xx -->` |
| **Mức độ** | `<!-- High / Medium / Low -->` |
| **Người phát hiện** | `<!-- Họ tên thành viên -->` |
| **Ngày phát hiện** | `<!-- DD/MM/YYYY -->` |
| **Trạng thái** | `<!-- Open / Closed -->` |

**Tiêu đề:**
`<!-- Mô tả hành vi lỗi cụ thể -->`

**Môi trường:**
- Trình duyệt: Chrome `<!-- version -->`
- Hệ điều hành: `<!-- OS -->`
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
`<!-- VD: Trang đăng nhập đã mở, dữ liệu đã reset -->`

**Bước tái hiện:**
1. `<!-- Bước 1 -->`
2. `<!-- Bước 2 -->`
3. `<!-- Bước 3 -->`

**Kết quả mong đợi:**
`<!-- Kết quả đúng theo SRS -->`

**Kết quả thực tế:**
`<!-- Kết quả hệ thống thật sự trả về -->`

**Tác động:**
`<!-- VD: Vi phạm quy tắc nghiệp vụ cốt lõi, cho phép mượn vượt giới hạn -->`

**Minh chứng:**
`<!-- Đính kèm ảnh chụp màn hình nếu có -->`

**Đề xuất xử lý:**
`<!-- Gợi ý cách sửa lỗi nếu có -->` 

---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | `<!-- TC-xx -->` |
| **REQ liên quan** | `<!-- REQ-xx -->` |
| **Mức độ** | `<!-- High / Medium / Low -->` |
| **Người phát hiện** | `<!-- Họ tên thành viên -->` |
| **Ngày phát hiện** | `<!-- DD/MM/YYYY -->` |
| **Trạng thái** | `<!-- Open / Closed -->` |

**Tiêu đề:**
`<!-- Mô tả hành vi lỗi -->`

**Bước tái hiện:**
1. `<!-- -->`
2. `<!-- -->`
3. `<!-- -->`

**Kết quả mong đợi:**
`<!-- -->`

**Kết quả thực tế:**
`<!-- -->`

**Tác động:**
`<!-- -->`

**Minh chứng:**
`<!-- -->`

**Đề xuất xử lý:**
`<!-- -->`

---

## BUG-03

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-03 |
| **TC liên quan** | TC-37 |
| **REQ liên quan** | REQ-07 |
| **Mức độ** | Medium |
| **Người phát hiện** | Tên của bạn |
| **Ngày phát hiện** | DD/MM/YYYY |
| **Trạng thái** | Open |

**Tiêu đề:**  
Hệ thống từ chối email hợp lệ khi thêm thành viên mới

**Môi trường:**
- Trình duyệt: Google Chrome
- Hệ điều hành: Windows
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**  
Dữ liệu đã reset. Đã đăng nhập bằng tài khoản thủ thư.

**Bước tái hiện:**
1. Đăng nhập bằng tài khoản `librarian@library.com`.
2. Vào tab **Thành viên**.
3. Chọn **Thêm thành viên**.
4. Nhập họ tên `Nguyễn Văn Mới`.
5. Nhập email `nguyen.van.moi@example.com`.
6. Nhập số điện thoại `0912345678`.
7. Nhấn **Thêm thành viên**.

**Kết quả mong đợi:**  
Hệ thống tạo thành viên mới thành công vì email `nguyen.van.moi@example.com` là email hợp lệ, có ký tự `@` và có dấu `.` trong phần domain.

**Kết quả thực tế:**  
Hệ thống hiển thị lỗi **“Email không hợp lệ.”** và không tạo thành viên mới.

**Tác động:**  
Thủ thư không thể thêm thành viên mới dù nhập email hợp lệ. Lỗi ảnh hưởng trực tiếp đến chức năng quản lý thành viên.

**Minh chứng:**  
![TC-37 valid email rejected](./assets/TC-37-valid-email-rejected.png)

**Đề xuất xử lý:**  
Kiểm tra lại logic validate email. Hệ thống cần chấp nhận email hợp lệ dạng `user@domain.com`, bao gồm cả email có dấu `.` trong phần tên người dùng như `nguyen.van.moi@example.com`.

---

## BUG-04

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-04 |
| **TC liên quan** | TC-39 |
| **REQ liên quan** | REQ-07 |
| **Mức độ** | Medium |
| **Người phát hiện** | Tên của bạn |
| **Ngày phát hiện** | DD/MM/YYYY |
| **Trạng thái** | Open |

**Tiêu đề:**  
Hệ thống cho phép thêm thành viên với email không hợp lệ `user@domain`

**Môi trường:**
- Trình duyệt: Google Chrome
- Hệ điều hành: Windows
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**  
Dữ liệu đã reset. Đã đăng nhập bằng tài khoản thủ thư.

**Bước tái hiện:**
1. Đăng nhập bằng tài khoản `librarian@library.com`.
2. Vào tab **Thành viên**.
3. Chọn **Thêm thành viên**.
4. Nhập họ tên `Email Sai Domain`.
5. Nhập email `user@domain`.
6. Nhập số điện thoại `0912345678`.
7. Nhấn **Thêm thành viên**.

**Kết quả mong đợi:**  
Hệ thống không tạo thành viên mới và hiển thị lỗi email không hợp lệ vì email `user@domain` thiếu dấu `.` trong phần domain.

**Kết quả thực tế:**  
Hệ thống vẫn tạo thành viên mới và hiển thị thông báo **“Thêm thành viên thành công! Mã: MEM007”**.

**Tác động:**  
Hệ thống cho phép lưu email sai định dạng, làm giảm chất lượng dữ liệu thành viên và vi phạm quy tắc xác thực email của REQ-07.

**Minh chứng:**  
![TC-39 invalid email input](./assets/TC-39-invalid-email-user-domain-input.png)  
![TC-39 invalid email accepted](./assets/TC-39-invalid-email-user-domain-accepted.png)

**Đề xuất xử lý:**  
Cập nhật logic validate email để yêu cầu email phải có ký tự `@` và dấu `.` trong phần domain.

---

## BUG-05

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-05 |
| **TC liên quan** | TC-40 |
| **REQ liên quan** | REQ-07 |
| **Mức độ** | Medium |
| **Người phát hiện** | Tên của bạn |
| **Ngày phát hiện** | DD/MM/YYYY |
| **Trạng thái** | Open |

**Tiêu đề:**  
Hệ thống hiển thị sai thông báo lỗi khi thêm thành viên với email đã tồn tại

**Môi trường:**
- Trình duyệt: Google Chrome
- Hệ điều hành: Windows
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**  
Dữ liệu đã reset. Đã đăng nhập bằng tài khoản thủ thư. Email `ba.nguyen@email.com` đã tồn tại trong hệ thống.

**Bước tái hiện:**
1. Đăng nhập bằng tài khoản `librarian@library.com`.
2. Vào tab **Thành viên**.
3. Chọn **Thêm thành viên**.
4. Nhập họ tên `Nguyễn Trùng Email`.
5. Nhập email `ba.nguyen@email.com`.
6. Nhập số điện thoại `0912345678`.
7. Nhấn **Thêm thành viên**.

**Kết quả mong đợi:**  
Hệ thống không tạo thành viên mới và hiển thị thông báo lỗi email đã tồn tại hoặc email bị trùng.

**Kết quả thực tế:**  
Hệ thống hiển thị lỗi **“Email không hợp lệ.”** thay vì thông báo email đã tồn tại.

**Tác động:**  
Thông báo lỗi sai làm người dùng hiểu nhầm rằng email bị sai định dạng, trong khi vấn đề thực tế là email đã tồn tại. Điều này gây khó khăn cho thủ thư khi nhập dữ liệu.

**Minh chứng:**  
![TC-40 duplicate email input](./assets/TC-40-duplicate-email-input.png)  
![TC-40 duplicate email wrong error](./assets/TC-40-duplicate-email-wrong-error.png)

**Đề xuất xử lý:**  
Kiểm tra thứ tự xử lý validation. Hệ thống cần nhận diện email hợp lệ trước, sau đó kiểm tra email đã tồn tại để hiển thị đúng thông báo lỗi trùng email.
