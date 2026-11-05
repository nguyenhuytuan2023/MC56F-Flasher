# MC56F Flasher

**Ứng dụng nạp Flash cho Windows x64 — phiên bản 1.0.369.**

MC56F Flasher phục vụ thao tác bộ nhớ Flash trên các MCU MC56F được liệt kê trong ứng dụng, thông qua phần cứng SEGGER Flasher / J-Link. Giao diện có các thao tác đọc, xóa, nạp và kiểm tra dữ liệu, cùng trình xem HEX / ASCII.

**Vui lòng đọc phần [Miễn trừ trách nhiệm](#miễn-trừ-trách-nhiệm) trước khi sử dụng với thiết bị thực tế.**

## Tải ứng dụng

[Tải MC56F-Flasher.exe v1.0.369](https://github.com/nguyenhuytuan2023/MC56F-Flasher/releases/download/v1.0.369/MC56F-Flasher.exe)

| Thông tin | Giá trị |
|---|---|
| Phiên bản | 1.0.369 |
| Nền tảng | Windows x64 |
| Tên tệp | `MC56F-Flasher.exe` |
| Dung lượng | 531.968 byte (Windows x64) |

### Kiểm tra tính toàn vẹn

SHA-256 của tệp `MC56F-Flasher.exe` phiên bản **1.0.369**:

```text
5a2e1784508629d8636d3de1502d2c3e8a1c9b707e5a31facb8719bd8fe83863
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
5. Duy trì nguồn cấp và kết nối ổn định trong quá trình thao tác; sử dụng chức năng kiểm tra dữ liệu khi phù hợp.

Khả năng thực hiện từng thao tác phụ thuộc MCU, trạng thái bảo vệ, bộ nạp và bo mạch. Danh sách lựa chọn trong giao diện không phải cam kết tương thích với mọi biến thể hoặc mọi thiết bị sử dụng MCU đó.

## Thay đổi trong v1.0.369

- Sửa trạng thái **Not Responding** khi xem HEX lớn trong lúc WRITE; bảng HEX vẽ các dòng đang nhìn thấy, vẫn giữ HEX/ASCII, cuộn toàn vùng, Home/End và Go tới địa chỉ.
- Tiến độ có giai đoạn/thời gian chạy; UI không chờ chặn worker. Cancel/đóng cửa sổ yêu cầu dừng tại ranh giới an toàn của giao thức, không cưỡng bức ngắt lệnh đang chạy.
- **MC56F8035:** ERASE bỏ bảo vệ ghi HFM có kiểm tra readback rồi xóa đúng một lần; WRITE dùng ERASE một lần → WRITE → VERIFY toàn vùng một lần. Không vượt CNFG.LOCK hoặc khóa đọc/security, không tự sửa word cấu hình trong firmware. Quy tắc bỏ bảo vệ này không tự áp dụng cho các model khác.
- VERIFY có thể đối chiếu buffer READ gần nhất nếu chưa mở firmware; nút **Use READ as firmware** sao chép buffer để chuẩn bị ghi một cách chủ động.
- Sửa nhãn checksum thành **SUM16**. App đơn lẻ hoạt động offline, không yêu cầu license/activation/đăng nhập.
- TCK chỉ 100 / 500 / 1000 kHz, tối đa 1 MHz. **Nguồn J-Link bật mặc định:** pin 19 là 5 V; dùng mạch ổn áp 3,3 V phù hợp, VTref phải trong khoảng 3,0–3,6 V.

Bản Release này đã qua **565 kiểm tra phần mềm** và kiểm thử form-worker WRITE/Cancel/Close/cleanup cùng UI Automation. MC56F8035 có bằng chứng BOOT/READ/CHECKSUM/VERIFY/ERASE/WRITE trên chip thật từ các bản Debug cùng core; kiểm thử mới nhất qua form đã ghi/VERIFY đủ 64 KiB và không có timeout phản hồi UI. Đây không phải chứng nhận HIL cho toàn bộ danh sách MCU; việc bỏ hậu tố Test trong app không thay cho bằng chứng trên từng model.

Gói tải về chỉ gồm một EXE; driver/bộ phần mềm SEGGER J-Link cài riêng. Không kèm firmware, công cụ kiểm thử, source hoặc dữ liệu thiết bị của người sử dụng.

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
