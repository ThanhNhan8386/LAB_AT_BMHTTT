# LAB 4 – Khảo sát hệ thống mạng bằng Nmap

## 1. Thông tin sinh viên
- Họ và tên: LẠI THÀNH NHÂN
- MSSV: 1150080151
- Môn học: ATBMHHT
- Tên bài Lab: LAB 4 – Khảo sát hệ thống mạng bằng Nmap

## 2. Môi trường thực hành
- VMware Workstation
- Kali Linux 2026.2
- Metasploitable 2
- Công cụ: Nmap
- Mạng thực hành: Host-Only

### Địa chỉ IP
- Kali Linux: 192.168.130.131
- Metasploitable 2: 192.168.130.130

## 3. Nội dung đã thực hiện
- Kiểm tra và sử dụng Nmap trên Kali Linux.
- Xác định địa chỉ IP của Kali Linux và Metasploitable 2.
- Thực hiện Host Discovery để phát hiện các host đang hoạt động.
- Thực hiện TCP Connect Scan (-sT).
- Thực hiện SYN Scan (-sS).
- Thực hiện FIN, Xmas và NULL Scan.
- Thực hiện ACK Scan (-sA).
- Thực hiện quét một số cổng UDP.
- Nhận diện dịch vụ và phiên bản bằng -sV.
- Nhận diện hệ điều hành bằng -O.
- Thực hiện Aggressive Scan (-A).
- Thực hiện NSE Script để thu thập/kiểm tra thông tin dịch vụ.

## 4. Kết quả thực hiện
- Kali Linux và Metasploitable 2 kết nối được với nhau trong mạng Host-Only.
- Phát hiện máy Metasploitable 2 tại IP 192.168.130.130.
- Nmap phát hiện nhiều dịch vụ đang mở trên Metasploitable 2 như:
  - 21/tcp: FTP
  - 22/tcp: SSH
  - 23/tcp: Telnet
  - 25/tcp: SMTP
  - 53/tcp: DNS
  - 80/tcp: HTTP
  - 139/tcp, 445/tcp: SMB
  - 3306/tcp: MySQL
  - 5432/tcp: PostgreSQL
  - 5900/tcp: VNC
- Quét -sV nhận diện được một số phiên bản dịch vụ như vsftpd 2.3.4,
  OpenSSH 4.7p1 và Apache httpd 2.2.8.
- OS Detection nhận diện máy đích thuộc Linux 2.6.x.
- Kết quả thực hành cho thấy sự khác biệt giữa các trạng thái
  open, closed, filtered, open|filtered và unfiltered.

## 5. Lưu ý khi kiểm tra/chạy lại
1. Khởi động cả Kali Linux và Metasploitable 2.
2. Đảm bảo hai máy ảo sử dụng cùng mạng Host-Only.
3. Kiểm tra lại IP vì địa chỉ IP có thể thay đổi sau khi khởi động lại máy ảo.
4. Thực hiện các lệnh Nmap từ Kali Linux tới IP của Metasploitable 2.
5. Một số kiểu quét như SYN Scan và OS Detection cần sử dụng sudo.
6. Các kết quả và hình ảnh trong báo cáo được lấy trực tiếp từ môi trường
   thực hành của sinh viên.

## 6. Phạm vi thực hành
Các thao tác quét được thực hiện trong môi trường máy ảo Host-Only phục vụ
mục đích học tập, không thực hiện quét các hệ thống bên ngoài hoặc hệ thống
không được phép.
