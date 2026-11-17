# LAB 1 – Mã hóa đối xứng cổ điển

Bài thực hành môn **An toàn và Bảo mật thông tin**. Chương trình sử dụng Java Swing để minh họa quá trình mã hóa và giải mã bằng sáu thuật toán mật mã cổ điển.

## Thông tin sinh viên

- **Họ và tên:** Lại Thành Nhân
- **MSSV:** 1150080151
- **Lớp:** 11_CNPM2

## Chức năng

- Mã hóa và giải mã bằng Caesar, Vigenère, Rail Fence, Playfair, Transposition và Autokey.
- Kiểm tra khóa đầu vào, mở và lưu bản mã dưới dạng tệp `.txt`.
- Hiển thị ma trận khóa 5×5 của thuật toán Playfair.
- Chọn thuật toán trên giao diện tổng hợp và lưu lịch sử thao tác vào SQL Server.
- Minh họa điểm yếu của mật mã cổ điển bằng thử khóa Caesar, thống kê tần suất chữ cái và phân tích Vigenère khi biết cặp bản rõ và bản mã.

## Công nghệ sử dụng

- Java 17 và Java Swing
- Apache NetBeans và Maven
- Microsoft SQL Server Express và JDBC

## Hướng dẫn chạy

1. Mở project `LAB1_MaHoaCoDien` trong NetBeans.
2. Chọn **Clean and Build** (`Shift+F11`).
3. Chọn **Run Project** (`F6`) để mở menu chính `week_01.frm_Menu`.
4. Chọn thuật toán, nhập bản rõ và khóa. Bấm **Encrypt** để mã hóa hoặc **Decrypt** để giải mã.

**Lưu lịch sử:** Chạy script tạo cơ sở dữ liệu trong phụ lục báo cáo. Trên ứng dụng, mở **Kết nối SQL Server** và chọn **Test Connection** sau khi nhập thông tin kết nối. Các thao tác trên form **Tổng hợp** sẽ được lưu vào bảng `dbo.history`. Nếu chưa cấu hình SQL Server, vẫn có thể mã hóa và giải mã bình thường.

## Kết quả kiểm thử mẫu

| Thuật toán | Bản rõ | Khóa | Bản mã | Kết quả giải mã |
| --- | --- | --- | --- | --- |
| Caesar | `HELLO` | `3` | `KHOOR` | `HELLO` |
| Vigenère | `HELLO` | `KEY` | `RIJVS` | `HELLO` |
| Rail Fence | `HELLO WORLD` | `3` | `HOREL OLLWD` | `HELLO WORLD` |
| Playfair | `HELLOWORLD` | `KEYWORD` | `GYIZSCOKCFBU` | `HELXLOWORLDX` |
| Transposition | `BAOMAT` | `2,3,1` | `AAOTBM` | `BAOMAT` |
| Autokey | `HELLO` | `KEY` | `RIJSS` | `HELLO` |

Ở ví dụ Playfair, kết quả giải mã còn ký tự đệm `X` do thuật toán chèn thêm khi chia bản rõ thành từng cặp chữ.

## Báo cáo và video demo

- [Báo cáo thực hành LAB 1](./11DH_CNPM2_1150080151_LAITHANHNHAN.docx)
- [Video demo trên YouTube](https://youtu.be/TI8vywJC_Co)
