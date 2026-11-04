# MC56F Flasher

**Ứng dụng nạp Flash cho Windows x64 — phiên bản 1.0.295.**

MC56F Flasher phục vụ thao tác bộ nhớ Flash trên các MCU MC56F được liệt kê trong ứng dụng, thông qua phần cứng SEGGER Flasher / J-Link. Giao diện có các thao tác đọc, xóa, nạp và kiểm tra dữ liệu, cùng trình xem HEX / ASCII.

**Vui lòng đọc phần [Miễn trừ trách nhiệm](#miễn-trừ-trách-nhiệm) trước khi sử dụng với thiết bị thực tế.**

## Tải ứng dụng

**Trạng thái:** Bản phát hành `v1.0.295` đang chờ hoàn tất tải tệp thực thi. Hiện chưa có file `.exe` công khai trong Releases.

[Xem các bản phát hành và ghi chú phiên bản](https://github.com/nguyenhuytuan2023/MC56F-Flasher/releases). Sau khi phát hành, chọn `MC56F-Flasher.exe` trong mục **Assets**.

| Thông tin | Giá trị |
|---|---|
| Phiên bản | 1.0.295 |
| Nền tảng | Windows x64 |
| Tên tệp | `MC56F-Flasher.exe` |
| Dung lượng | 2.028.032 byte, khoảng 1,93 MiB |

### Kiểm tra tính toàn vẹn

SHA-256 của tệp `MC56F-Flasher.exe` phiên bản **1.0.295**:

```text
0846e32fdf9cb828dbd561b7d38428231d8e1f3d929a0d72fbddc1c3a71d8cba
```

Có thể kiểm tra tệp tải về bằng PowerShell trong thư mục chứa tệp:

```powershell
Get-FileHash .\MC56F-Flasher.exe -Algorithm SHA256
```

Giá trị SHA-256 giúp đối chiếu tệp tải về với bản phát hành; không chứng nhận khả năng tương thích với phần cứng.

## Yêu cầu

- Máy tính chạy Windows x64.
- Phần mềm **SEGGER J-Link x64** và driver USB phù hợp. Tải từ [trang chính thức của SEGGER](https://www.segger.com/downloads/jlink/).
- Phần cứng SEGGER Flasher / J-Link tương thích với MCU và giao thức được chọn trong ứng dụng.
- Sơ đồ chân, nguồn cấp và mức điện áp đúng với bo mạch cần thao tác.

## Chuẩn bị và sử dụng

1. Cài phần mềm và driver J-Link x64; chuẩn bị phần cứng kết nối phù hợp.
2. Kiểm tra chính xác mã MCU, sơ đồ đấu nối, GND, VTref và nguồn cấp. Không mặc định điện áp do bộ nạp cung cấp phù hợp với bo mạch.
3. Mở `MC56F-Flasher.exe`, chọn thiết bị và các thông số tương ứng trong giao diện.
4. Chọn đúng file firmware. Giao diện có bộ lọc cho các định dạng `.bin`, `.hex`, `.s19`, `.srec`, `.mot`; nội dung và địa chỉ dữ liệu phải phù hợp với MCU/vùng nhớ được chọn.
5. Sao lưu dữ liệu gốc và thông số cấu hình trước khi xóa hoặc ghi, nếu thiết bị cho phép. Chuẩn bị phương án phục hồi trước khi thực hiện thao tác có thể làm mất dữ liệu.
6. Duy trì nguồn cấp và kết nối ổn định trong quá trình thao tác; sử dụng chức năng kiểm tra dữ liệu khi phù hợp.

Khả năng thực hiện từng thao tác phụ thuộc MCU, trạng thái bảo vệ, bộ nạp và bo mạch. Danh sách lựa chọn trong giao diện không phải cam kết tương thích với mọi biến thể hoặc mọi thiết bị sử dụng MCU đó.

## Miễn trừ trách nhiệm

### Cung cấp theo hiện trạng

Phần mềm và tài liệu được cung cấp **theo hiện trạng ("AS IS")**. Trong phạm vi pháp luật cho phép, tác giả và bên phát hành không đưa ra bảo đảm rõ ràng hoặc ngụ ý về tính chính xác, độ tin cậy, khả năng tương thích, khả năng đáp ứng yêu cầu hay sự phù hợp với một mục đích cụ thể. Phần mềm có thể có lỗi và không được bảo đảm hoạt động liên tục hoặc thành công trên mọi thiết bị.

### Trách nhiệm của người sử dụng

Người sử dụng tự đánh giá tính phù hợp của phần mềm, file firmware và phương pháp kết nối trước khi thao tác. Người sử dụng có trách nhiệm kiểm tra đúng MCU, vùng nhớ, sơ đồ chân, mức điện áp, nguồn cấp và bản sao lưu cần thiết.

Việc chọn sai MCU, firmware, vùng nhớ, mức điện áp hoặc đấu nối; mất nguồn hay gián đoạn kết nối trong khi thao tác có thể làm mất dữ liệu, thay đổi cấu hình, khiến thiết bị không khởi động hoặc gây hư hỏng phần cứng. **Các thao tác xóa và ghi có thể không khôi phục được.** Chỉ thực hiện trên thiết bị và dữ liệu mà bạn có quyền thao tác.

### Giới hạn trách nhiệm

Trong phạm vi pháp luật cho phép, tác giả và bên phát hành không chịu trách nhiệm đối với thiệt hại trực tiếp hoặc gián tiếp phát sinh từ việc sử dụng, sử dụng sai hoặc không thể sử dụng phần mềm, bao gồm mất dữ liệu, hư hỏng thiết bị, gián đoạn hoạt động, mất lợi nhuận và chi phí sửa chữa hoặc thay thế.

Nội dung này không loại trừ hoặc hạn chế các quyền và trách nhiệm mà pháp luật áp dụng không cho phép loại trừ hoặc hạn chế.

## Báo lỗi

Tạo báo cáo tại [Issues](https://github.com/nguyenhuytuan2023/MC56F-Flasher/issues), kèm phiên bản ứng dụng, mã MCU, loại bộ nạp, thao tác đã thực hiện và thông báo lỗi liên quan. Không đăng khóa bảo mật, thông tin cá nhân hoặc firmware mà bạn không có quyền chia sẻ.
