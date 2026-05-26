# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | `<!-- Tên nhóm -->` |
| **Ngày báo cáo** | `<!-- DD/MM/YYYY -->` |

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

---

## BUG-06

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-06 |
| **TC liên quan** | TC-33 |
| **REQ liên quan** | REQ-05 |
| **Mức độ** | Medium |
| **Người phát hiện** | Tên của bạn |
| **Ngày phát hiện** | DD/MM/YYYY |
| **Trạng thái** | Open |

**Tiêu đề:**  
Hệ thống không hiển thị cảnh báo khi trả sách quá hạn

**Môi trường:**
- Trình duyệt: Google Chrome
- Hệ điều hành: Windows
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**  
Dữ liệu đã reset. Đăng nhập bằng tài khoản thành viên `ba.nguyen@email.com`. Phiếu BR001 đang ở trạng thái “Đang mượn” và đã quá hạn.

**Bước tái hiện:**
1. Đăng nhập bằng `ba.nguyen@email.com`.
2. Vào tab **Mượn / Trả**.
3. Tìm phiếu BR001 của sách **Kiểm thử phần mềm nhập môn**.
4. Nhấn **Trả sách**.
5. Quan sát thông báo và trạng thái sách.

**Kết quả mong đợi:**  
Hệ thống cho phép trả sách và hiển thị cảnh báo quá hạn.

**Kết quả thực tế:**  
Hệ thống cho trả sách, BOOK003 trở lại trạng thái “Có sẵn”, nhưng không thấy cảnh báo quá hạn.

**Tác động:**  
Người dùng không được thông báo rằng sách đã được trả quá hạn, vi phạm yêu cầu nghiệp vụ của REQ-05.

**Minh chứng:**  
![TC-33 trước khi trả BR001](./assets/TC-33-truoc-khi-tra-br001.png)  
![TC-33 sau khi trả BOOK003 có sẵn](./assets/TC-33-sau-khi-tra-book003-co-san.png)

**Đề xuất xử lý:**  
Bổ sung hoặc sửa logic hiển thị cảnh báo khi người dùng trả sách có hạn trả nhỏ hơn hoặc bằng ngày hiện tại.

---

## BUG-07

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-07 |
| **TC liên quan** | TC-34 |
| **REQ liên quan** | REQ-05, REQ-08 |
| **Mức độ** | High |
| **Người phát hiện** | Tên của bạn |
| **Ngày phát hiện** | DD/MM/YYYY |
| **Trạng thái** | Open |

**Tiêu đề:**  
Thành viên có thể xem và trả sách thuộc phiếu mượn của thành viên khác

**Môi trường:**
- Trình duyệt: Google Chrome
- Hệ điều hành: Windows
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**  
Dữ liệu đã reset. Đăng nhập bằng tài khoản thành viên `ba.nguyen@email.com`.

**Bước tái hiện:**
1. Đăng nhập bằng `ba.nguyen@email.com`.
2. Vào tab **Mượn / Trả**.
3. Chuyển sang tab **Tra cứu phiếu mượn**.
4. Nhập `MEM006` và nhấn **Tra cứu**.
5. Quan sát kết quả trả về.
6. Nhấn **Trả sách** trên phiếu BR003 nếu hệ thống cho phép.
7. Kiểm tra lại trạng thái sách BOOK013 trong tab **Sách**.

**Kết quả mong đợi:**  
Thành viên không được xem phiếu mượn của thành viên khác và không được trả sách thuộc phiếu của người khác.

**Kết quả thực tế:**  
Thành viên MEM002 xem được phiếu BR003 của MEM006, thấy nút **Trả sách**, và sau đó BOOK013 hiển thị trạng thái **Có sẵn**.

**Tác động:**  
Lỗi vi phạm nghiêm trọng về phân quyền và bảo mật dữ liệu. Thành viên có thể thao tác lên phiếu mượn không thuộc về mình.

**Minh chứng:**  
![TC-34 thành viên thấy phiếu của MEM006](./assets/TC-34-thanh-vien-thay-phieu-cua-mem006.png)  
![TC-34 BOOK013 trở về có sẵn](./assets/TC-34-book013-tro-ve-co-san.png)

**Đề xuất xử lý:**  
Giới hạn chức năng tra cứu và thao tác trả sách để thành viên chỉ nhìn thấy và thao tác trên các phiếu mượn của chính mình.

---

