# README – LAB 8: LOCAL DNS ATTACK

**Môn học:** Thực hành An toàn hệ thống thông tin  
**Họ và tên:** Thành Nhân  
**MSSV:** 1150080151  
**Lớp:** 11DH_CNPM2  
**Tên bài thực hành:** Local DNS Attack – DNS Spoofing và Cache Poisoning

## 1. Mục tiêu bài thực hành

- Tìm hiểu nguyên lý hoạt động của DNS trong mạng nội bộ.
- Cấu hình hệ thống DNS Server sử dụng BIND9.
- Tìm hiểu kỹ thuật DNS Spoofing và DNS Cache Poisoning.
- Quan sát các gói tin DNS bằng Wireshark.
- Thực hiện mô phỏng tấn công DNS trong mạng ảo cô lập.
- Tìm hiểu các biện pháp phòng chống và khôi phục hệ thống DNS.

## 2. Môi trường thực hành

**Phần mềm:** VMware Workstation

**Các máy ảo sử dụng:**

| Máy ảo | Vai trò | Địa chỉ IP |
|---|---|---|
| pfSense 2.7.2 | Firewall | 10.9.0.1 |
| Ubuntu Server | DNS Server | 10.9.0.10 |
| Ubuntu Client | Victim | 10.9.0.100 |
| Kali Linux | Attacker | 10.9.0.200 |
| DMZ-WEB | Web Server hợp lệ | 172.16.6.10 |
| APP-TEST | DNS mô phỏng | 172.16.6.20 |

Mạng thực hành DNS-LAB sử dụng dải địa chỉ `10.9.0.0/24`, được cô lập với các mạng khác bằng Firewall pfSense.

## 3. Nội dung thực hiện

### 3.1. Cấu hình pfSense

- Khởi động máy ảo pfSense 2.7.2.
- Thêm Network Adapter thứ 5 trên VMware.
- Tạo LAN Segment có tên `dns-lab`.
- Gán interface `em4` vào DNSLAB.
- Cấu hình địa chỉ IP `10.9.0.1/24`.
- Không cấu hình Upstream Gateway cho DNSLAB.

**Kết quả:** Đã tạo và kích hoạt interface DNSLAB trên pfSense.

### 3.2. Cấu hình Firewall Rules

Đã thực hiện cấu hình 5 Firewall Rules:

| STT | Action | Source | Destination | Port |
|---|---|---|---|---|
| 1 | Pass | 10.9.0.10 | 172.16.6.20 | TCP/UDP 53 |
| 2 | Pass | 10.9.0.0/24 | 172.16.6.10 | TCP 80 |
| 3 | Block | 10.9.0.0/24 | 10.6.0.0/24 | Any |
| 4 | Block + Log | 10.9.0.0/24 | 192.168.56.0/24 | Any |
| 5 | Block + Log | 10.9.0.0/24 | Any | Any |

**Kết quả:** Đã tạo đủ 5 rule để kiểm soát lưu lượng mạng DNSLAB. Rule 3 cần xác nhận bổ sung chức năng ghi log.

### 3.3. Chuẩn bị Ubuntu DNS Server

- Kiểm tra cấu hình máy ảo Ubuntu.
- Cấu hình RAM 6 GB, CPU 2 cores và ổ cứng 20 GB.
- Chuẩn bị thêm Network Adapter kết nối mạng `dns-lab`.
- Dự kiến cấu hình IP tĩnh `10.9.0.10/24`.
- Chuẩn bị cài đặt BIND9 và công cụ kiểm thử DNS.

**Trạng thái:** Chưa hoàn thành do cần khôi phục tài khoản đăng nhập Ubuntu.

### 3.4. Task 1 – Hosts File Redirection

**Mục tiêu:** Tìm hiểu cách thay đổi file `/etc/hosts` để chuyển hướng truy cập tên miền đến máy chủ giả lập.

**Kết quả mong đợi:** Victim truy cập địa chỉ `10.9.0.200` thay vì máy chủ hợp lệ `172.16.6.10`.

**Trạng thái:** Chưa thực hiện.

### 3.5. Task 2 – Direct DNS Spoofing

**Mục tiêu:** Tìm hiểu cách phản hồi DNS giả mạo có thể ảnh hưởng đến kết quả phân giải tên miền trên Victim.

**Kết quả mong đợi:** Victim nhận bản ghi DNS giả trỏ đến `10.9.0.200`, đồng thời quan sát gói DNS bằng Wireshark.

**Trạng thái:** Chưa thực hiện.

### 3.6. Task 3 – DNS Cache Poisoning

**Mục tiêu:** Tìm hiểu kỹ thuật đầu độc bộ nhớ đệm DNS Resolver.

**Kết quả mong đợi:** DNS Server lưu bản ghi giả trong cache, làm ảnh hưởng đến kết quả phân giải của các client sử dụng chung DNS Resolver.

**Trạng thái:** Chưa thực hiện.

## 4. Biện pháp phòng chống

- Phân đoạn và cô lập mạng bằng Firewall.
- Giới hạn các DNS Server mà client được phép sử dụng.
- Sử dụng DNSSEC để xác thực dữ liệu DNS khi được hỗ trợ.
- Sử dụng DNS COOKIE và cơ chế ngẫu nhiên hóa cổng nguồn.
- Giám sát các phản hồi DNS bất thường.
- Xóa DNS cache khi phát hiện dữ liệu bị giả mạo.
- Tắt Promiscuous Mode sau khi hoàn thành thực hành.

## 5. Kết quả thực hiện hiện tại

Đã hoàn thành phần chuẩn bị và cấu hình Firewall pfSense:

- Tạo interface DNSLAB.
- Thiết lập địa chỉ IP `10.9.0.1/24`.
- Tạo 5 Firewall Rules theo yêu cầu.
- Chuẩn bị máy ảo Ubuntu DNS Server.

Các nội dung BIND9, DNS Spoofing, Cache Poisoning và kiểm thử khôi phục chưa được hoàn thành.

## 6. Kết luận

Qua quá trình thực hành, sinh viên đã bước đầu tìm hiểu cách xây dựng mạng ảo cô lập và sử dụng pfSense để kiểm soát lưu lượng giữa các vùng mạng.

Phần cấu hình Firewall giúp hiểu vai trò của phân đoạn mạng và giới hạn quyền truy cập trong việc bảo vệ hệ thống DNS.

Các nhiệm vụ mô phỏng tấn công DNS và kiểm thử phòng thủ sẽ tiếp tục được thực hiện sau khi hoàn thành cấu hình DNS Server và các máy ảo liên quan.

---

**Sinh viên thực hiện:** Thành Nhân  
**MSSV:** 1150080151  
**Lớp:** 11DH_CNPM2
