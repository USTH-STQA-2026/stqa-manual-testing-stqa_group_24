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
| TC-32 | Trả sách | Trả sách đang mượn thành công, phiếu chuyển “Đã trả” | BOOK002 ban đầu ở trạng thái “Có sẵn”. Sau khi mượn, BOOK002 chuyển sang “Đang mượn”. Sau khi trả sách, hệ thống hiển thị thông báo “Trả sách thành công.” và phiếu BR006 xuất hiện với trạng thái “Đã trả”. | Pass | ![TC-32 trước khi mượn](./assets/TC-32-truoc-khi-muon-book002.png)<br>![TC-32 sau khi mượn](./assets/TC-32-sau-khi-muon-book002.png)<br>![TC-32 trả sách thành công](./assets/TC-32-tra-sach-thanh-cong-br006.png) | - |
| TC-33 | Trả sách | Khi trả sách quá hạn, hệ thống phải hiển thị cảnh báo quá hạn | Thành viên MEM002 trả phiếu BR001 của BOOK003 (hạn trả 15/09/2024). Sau khi trả, BOOK003 trở về trạng thái “Có sẵn”, nhưng không thấy hệ thống hiển thị cảnh báo quá hạn. | Fail | ![TC-33 trước khi trả BR001](./assets/TC-33-truoc-khi-tra-br001.png)<br>![TC-33 sau khi trả BOOK003 có sẵn](./assets/TC-33-sau-khi-tra-book003-co-san.png) | BUG-06 |
| TC-34 | Trả sách / Quyền truy cập | Thành viên không được thấy hoặc trả sách của người khác | Thành viên MEM002 tra cứu `MEM006` và xem được phiếu BR003 của thành viên khác, đồng thời có nút “Trả sách”. Sau đó BOOK013 hiển thị trạng thái “Có sẵn”, cho thấy thành viên có thể đã trả được sách của người khác. | Fail | ![TC-34 thành viên thấy phiếu của MEM006](./assets/TC-34-thanh-vien-thay-phieu-cua-mem006.png)<br>![TC-34 BOOK013 trở về có sẵn](./assets/TC-34-book013-tro-ve-co-san.png) | BUG-07 |
| TC-35 | Xử lý quá hạn | Thủ thư nhấn được nút kiểm tra quá hạn và hệ thống cập nhật các phiếu quá hạn | Sau khi đăng nhập bằng tài khoản thủ thư và nhấn **Kiểm tra sách quá hạn**, hệ thống hiển thị thông báo “Đã cập nhật: 2 phiếu mượn quá hạn.” | Pass | ![TC-35 kiểm tra quá hạn thành công](./assets/TC-35-kiem-tra-qua-han-thanh-cong.png) | - |
| TC-36 | Xử lý quá hạn | Phiếu có ngày hết hạn ≤ ngày hiện tại được đánh dấu “Quá hạn” | Trước khi kiểm tra, BR001 và BR003 đang ở trạng thái “Đang mượn”. Sau khi nhấn **Kiểm tra sách quá hạn**, BR001 và BR003 chuyển sang trạng thái “Quá hạn”. | Pass | ![TC-36 trước kiểm tra quá hạn](./assets/TC-36-truoc-khi-kiem-tra-qua-han.png)<br>![TC-36 sau kiểm tra quá hạn](./assets/TC-36-sau-khi-kiem-tra-qua-han.png) | - |
| TC-37 | Quản lý thành viên | Thủ thư thêm thành viên hợp lệ thành công | Nhập họ tên `Nguyễn Văn Mới`, email `nguyen.van.moi@example.com`, SĐT `0912345678`. Hệ thống hiển thị lỗi “Email không hợp lệ.” và không tạo thành viên mới. | Fail | ![TC-37 valid email rejected](./assets/TC-37-valid-email-rejected.png) | BUG-03 |
| TC-38 | Quản lý thành viên | Thành viên thường không được thêm thành viên | Đăng nhập bằng tài khoản thành viên `ba.nguyen@email.com`. Giao diện chỉ hiển thị tab **Sách** và **Mượn / Trả**, không có tab **Thành viên** hoặc nút **Thêm thành viên**. | Pass | ![TC-38 member no member management tab](./assets/TC-38-member-no-member-management-tab.png) | - |
| TC-39 | Quản lý thành viên | Email `user@domain` bị từ chối vì thiếu dấu `.` trong domain | Nhập email `user@domain`, hệ thống vẫn hiển thị “Thêm thành viên thành công! Mã: MEM007”. | Fail | ![TC-39 invalid email accepted](./assets/TC-39-invalid-email-user-domain-accepted.png) | BUG-04 |
| TC-40 | Quản lý thành viên | Email đã tồn tại `ba.nguyen@email.com` bị từ chối vì trùng email | Nhập email đã tồn tại `ba.nguyen@email.com`, hệ thống hiển thị “Email không hợp lệ.” thay vì thông báo email đã tồn tại. | Fail | ![TC-40 duplicate email wrong error](./assets/TC-40-duplicate-email-wrong-error.png) | BUG-05 |

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
