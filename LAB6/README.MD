

## 1. Thông tin sinh viên

- **Họ và tên:** Thành Nhân
- **Mã số sinh viên:** 1150080151
- **Lớp:** 11DH_CNPM2
- **Môn học:** Thực hành An toàn hệ thống thông tin
- **Tên bài Lab:** LAB 6 – Xác thực Active Directory và chính sách truy cập trên pfSense

## 2. Mục tiêu bài thực hành

- Xây dựng mô hình mạng sử dụng tường lửa pfSense trên VMware Workstation.
- Cấu hình các interface WAN, LAN, MGMT và DMZ.
- Tích hợp Active Directory với pfSense thông qua LDAP.
- Cấu hình Captive Portal để xác thực người dùng.
- Tạo Firewall Alias và Schedule.
- Thiết lập và kiểm thử các chính sách truy cập mạng theo kịch bản.
- Kiểm tra hoạt động của Firewall và khả năng truy cập giữa các máy trong hệ thống.

## 3. Môi trường thực hành

**Phần mềm sử dụng:**
- VMware Workstation
- pfSense CE 2.7.2
- Windows Server 2022
- Windows 11
- Ubuntu Linux

**Cấu hình mạng:**

| Thiết bị | Địa chỉ IP | Chức năng |
|---|---|---|
| pfSense WAN | 192.168.252.x/24 | Kết nối Internet |
| pfSense LAN | 10.6.0.1/24 | Gateway mạng LAN |
| pfSense MGMT | 192.168.56.254/24 | Quản trị pfSense |
| pfSense DMZ | 172.16.6.1/24 | Gateway DMZ |
| Windows Server 2022 | 10.6.0.10/24 | Active Directory và DNS |
| Client-A | 10.6.0.21/24 | Máy kiểm thử A |
| Client-B | 10.6.0.22/24 | Máy kiểm thử B |
| DMZ-WEB | 172.16.6.10/24 | Máy chủ Web mô phỏng |

## 4. Nội dung thực hiện

### 4.1. Cấu hình môi trường VMware

- Chuẩn bị máy ảo pfSense.
- Cấu hình 4 Network Adapter.
- Sử dụng VMnet8 NAT cho kết nối WAN.
- Cấu hình VMnet2 Host-only cho mạng quản trị.
- Tạo LAN Segment riêng cho mạng LAN và DMZ.

### 4.2. Cấu hình pfSense

- Gán các interface WAN, LAN, MGMT và DMZ.
- Cấu hình địa chỉ IPv4 tĩnh cho LAN, MGMT và DMZ.
- Kiểm tra kết nối giữa máy thật và pfSense.
- Truy cập giao diện quản trị WebGUI.
- Tạo Firewall Rule cho phép máy quản trị truy cập pfSense qua HTTPS.
- Kiểm tra trạng thái Firewall và điều chỉnh tên các interface.

### 4.3. Chuẩn bị Active Directory

- Sử dụng Windows Server 2022.
- Cấu hình địa chỉ IP `10.6.0.10/24`.
- Kiểm tra kết nối từ Windows Server đến pfSense.
- Kiểm tra dịch vụ Active Directory Domain Services và DNS Server.
- Ghi nhận domain hiện tại là `vietnam.local`.

**Lưu ý:** Tài liệu LAB 6 yêu cầu domain `lab6.test`. Cần cấu hình domain phù hợp trước khi thực hiện LDAP.

### 4.4. Các nội dung cần hoàn thiện

- Tạo tài khoản Active Directory `sv_a`, `sv_b` và `svc_pfsense_ldap`.
- Tích hợp LDAP Authentication Server trên pfSense.
- Cấu hình Captive Portal.
- Tạo Firewall Alias và Schedule.
- Thực hiện kiểm thử các kịch bản từ 1 đến 5.

**Không thực hiện kịch bản 6 và 7 theo phạm vi bài làm đã lựa chọn.**

## 5. Kết quả thực hiện

- Đã thiết lập mô hình mạng pfSense với 4 interface.
- Đã cấu hình địa chỉ IP cho WAN, LAN, MGMT và DMZ.
- Đã cấu hình mạng Host-only phục vụ quản trị.
- Đã truy cập được giao diện WebGUI của pfSense.
- Đã cấu hình Firewall Rule cho phép quản trị qua HTTPS.
- Đã cấu hình Windows Server 2022 với địa chỉ IP phù hợp.
- Đã kiểm tra kết nối từ Windows Server đến pfSense.
- Đã xác nhận Windows Server có dịch vụ Active Directory và DNS.

Các nội dung LDAP, Captive Portal và chính sách truy cập theo kịch bản chưa có kết quả kiểm thử được xác nhận.

## 6. Hướng dẫn kiểm tra lại bài Lab

1. Khởi động VMware Workstation.
2. Khởi động máy ảo pfSense.
3. Kiểm tra địa chỉ IP của các interface.
4. Truy cập WebGUI tại `https://192.168.56.254`.
5. Kiểm tra Firewall Rules.
6. Khởi động Windows Server 2022.
7. Kiểm tra IP và kết nối đến pfSense.
8. Kiểm tra dịch vụ Active Directory và DNS.
9. Sau khi hoàn thiện LDAP, Captive Portal và Firewall Policy, tiến hành kiểm thử các kịch bản 1–5 theo tài liệu.

## 7. Lưu ý

- Các máy ảo phải kết nối đúng Network Adapter và LAN Segment.
- Địa chỉ IP phải được cấu hình đúng với mô hình mạng.
- Khi thay đổi Firewall Rule cần Save và Apply Changes.
- Không để Firewall ở trạng thái Disabled sau khi kiểm tra.
- Kiểm tra thứ tự Firewall Rule vì pfSense xử lý theo nguyên tắc First Match.
- Hình ảnh minh chứng phải được chụp trực tiếp từ quá trình thực hành.
- Không sử dụng kết quả giả hoặc hình ảnh từ máy khác.
- Sao lưu cấu hình pfSense để phục vụ kiểm tra và khôi phục.

## 8. Kết luận

Qua quá trình thực hành LAB 6, sinh viên đã xây dựng được mô hình mạng sử dụng pfSense trên VMware Workstation, cấu hình các interface mạng, thiết lập địa chỉ IP và kiểm tra khả năng kết nối giữa các thành phần.

Sinh viên bước đầu nắm được cách quản trị pfSense, cấu hình Firewall Rule và chuẩn bị môi trường Windows Server phục vụ tích hợp Active Directory.

Các nội dung xác thực LDAP, Captive Portal và kiểm thử chính sách truy cập cần tiếp tục hoàn thiện để đáp ứng đầy đủ mục tiêu của LAB 6.
