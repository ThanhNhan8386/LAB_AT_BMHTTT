# LAB1 - Examining SSH & Telnet in Wireshark

## 1. Thông tin sinh viên

- Họ và tên: Lại Thành Nhân
- Mã số sinh viên: 1150080151
- Môn học: AT_BTHTTT
- Tên bài Lab: Bắt gói tin Telnet - SSH bằng Wireshark

---

## 2. Mục tiêu bài Lab

- Thiết lập mô hình Client/Server sử dụng Telnet và SSH.
- Sử dụng Wireshark để bắt và phân tích lưu lượng mạng.
- Quan sát sự khác biệt giữa Telnet và SSH về khả năng bảo vệ dữ liệu.
- Kiểm tra ảnh hưởng của việc sử dụng mật khẩu phức tạp đối với Telnet.
- Phân tích metadata của phiên SSH mặc dù payload đã được mã hóa.

---

## 3. Môi trường thực hành

### Máy Host / Client

- Hệ điều hành: Windows 11
- PuTTY 0.85
- Wireshark 4.6.8
- VMware Workstation

### Máy Server

- Ubuntu Server 26.04.1 LTS
- Hostname: `lab1-server`
- Username: `thanhnhan`
- IP: `192.168.252.129`

### Dịch vụ

- Telnet Server: TCP/23
- SSH Server: TCP/22

Mô hình thực hành:

Windows Client  
→ VMware Network Adapter VMnet8  
→ Ubuntu Server `192.168.252.129`

---

## 4. Nội dung đã thực hiện

### 4.1. Cài đặt và cấu hình Ubuntu Server

- Tạo Ubuntu Server VM trên VMware.
- Cấu hình network sử dụng VMware NAT.
- Kiểm tra địa chỉ IP và kết nối giữa Windows Host và Ubuntu Server.
- Tạo tài khoản Linux phục vụ bài thực hành.

### 4.2. Cấu hình Telnet Server

Cài đặt Telnet Server:

```bash
sudo apt update
sudo apt install inetutils-telnetd -y
