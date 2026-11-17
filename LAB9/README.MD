# LAB 9 – Remote DNS Cache Poisoning

Bài thực hành môn **An toàn hệ thống thông tin** trong môi trường máy ảo cô lập bằng **pfSense**. Bài lab tìm hiểu ảnh hưởng của DNS cache poisoning đối với kết quả phân giải tên miền và các biện pháp bảo vệ DNS resolver.

## Thông tin sinh viên

- **Họ và tên:** Lại Thành Nhân
- **MSSV:** 1150080151
- **Lớp:** 11_CNPM2

## Môi trường thực hành

| Thành phần | Vai trò |
| --- | --- |
| pfSense | Định tuyến và phân tách các vùng ATTACKNET, DNSLAB và DMZ |
| Kali Linux | Máy kiểm thử ở vùng ATTACKNET, tách khỏi vùng DNSLAB |
| DNS-SERVER | Máy chủ DNS resolver chạy BIND9 ở cấu hình chuẩn |
| AUTH-DNS / APP-TEST | Máy chủ DNS có thẩm quyền và dịch vụ thử nghiệm trong vùng DMZ |
| VICTIM | Máy trạm kiểm tra kết quả phân giải tên miền |

## Nội dung thực hành

1. Kiểm tra cấu hình chuẩn của BIND9 và xác nhận máy trạm phân giải tên miền thử nghiệm về đúng máy chủ trong DMZ.
2. Kiểm tra khả năng phân tách mạng bằng cách đối chiếu lưu lượng DNS quan sát được ở ATTACKNET với lưu lượng tại máy chủ DNS.
3. Phân tích log và gói tin để so sánh kết quả phân giải trước và sau tình huống DNS cache poisoning mô phỏng.
4. Khôi phục BIND9, kiểm tra việc giới hạn truy vấn đệ quy và quan sát sự thay đổi của cổng nguồn UDP qua các lần truy vấn.

## Kết quả đối chiếu

| Giai đoạn | Kết quả mong đợi |
| --- | --- |
| Trước mô phỏng | Máy trạm phân giải tên miền thử nghiệm về máy chủ hợp lệ trong DMZ. |
| Sau mô phỏng | Kết quả phân giải trỏ về máy chủ mô phỏng thay vì máy chủ hợp lệ. |
| Sau khi khôi phục | BIND9 hoạt động trở lại, truy vấn đệ quy chỉ được phép từ mạng nội bộ và cổng nguồn UDP không còn cố định như trong mô hình thử nghiệm. |

## Bài học rút ra

- **Phân tách mạng** hạn chế khả năng quan sát lưu lượng giữa các vùng.
- **Recursion ACL** chỉ cho phép các máy được cấp quyền sử dụng chức năng phân giải đệ quy.
- **Ngẫu nhiên hóa cổng nguồn** làm giảm khả năng đoán đúng thông tin truy vấn DNS.
- **DNSSEC** giúp xác thực nguồn gốc và tính toàn vẹn của dữ liệu DNS đối với các vùng được ký hợp lệ.
