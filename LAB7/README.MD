# README – LAB 7
## XÂY DỰNG CHÍNH SÁCH WEB PROTECTION TRÊN MÔ HÌNH pfSense + WEB PROXY

**Môn học:** Thực hành An toàn hệ thống thông tin  
**Sinh viên:** Nhân  
**MSSV:** 1150080151  
**Lớp:** 11DH_CNPM2  
**Bài thực hành:** LAB 7

---

## 1. Mục tiêu

Bài thực hành nhằm xây dựng hệ thống bảo vệ truy cập Web bằng cách kết hợp pfSense Firewall và Web Proxy trên Ubuntu Server.

Các mục tiêu chính:

- Cấu hình pfSense quản lý và kiểm soát lưu lượng mạng.
- Triển khai Web Proxy bằng Squid và E2Guardian.
- Sử dụng ClamAV để kiểm tra file tải xuống.
- Xây dựng chính sách cho phép, cảnh báo và chặn website.
- Ngăn người dùng truy cập Web trực tiếp để vượt qua Proxy.
- Kiểm tra nhật ký và đánh giá hiệu quả chính sách bảo mật.

## 2. Môi trường thực hành

| Thành phần | Hệ điều hành / Phiên bản | Địa chỉ IP |
|---|---|---|
| Firewall | pfSense 2.7.2 | LAN: 10.6.0.1 |
| Domain Controller | Windows Server 2022 | 10.6.0.10 (theo mô hình) |
| Client-A | Windows 11 | 10.6.0.21 (theo mô hình) |
| Client-B | Windows | 10.6.0.22 (theo mô hình) |
| WEB-PROXY | Ubuntu Server 24.04.3 LTS | 10.6.0.30 (IP cấu hình mục tiêu) |
| DMZ-WEB | Ubuntu / Nginx | 172.16.6.10 (theo mô hình) |

**Thông tin Ubuntu WEB-PROXY:**

- Username: `lab7`
- Hostname: `web-proxy`
- Network Interface: `ens33`
- LAN Segment: `lab6-lan`
- Gateway: `10.6.0.1`
- DNS: `10.6.0.10`

## 3. Các bước thực hiện

### Bước 1: Chuẩn bị môi trường VMware

Kiểm tra các máy ảo phục vụ thực hành, bao gồm pfSense, Windows Server, Windows Client và Ubuntu Server.

Kiểm tra cấu hình CPU, RAM, ổ cứng và Network Adapter của từng máy.

### Bước 2: Kiểm tra cấu hình pfSense

Đã kiểm tra các interface của pfSense:

| Interface | IP |
|---|---|
| WAN | 192.168.252.135/24 |
| LAN | 10.6.0.1/24 |
| MGMT | 192.168.56.254/24 |
| DMZ | 172.16.6.1/24 |

Các interface phục vụ việc phân chia mạng và kiểm soát lưu lượng giữa các vùng.

### Bước 3: Cài đặt Ubuntu WEB-PROXY

Thực hiện cài đặt Ubuntu Server 24.04.3 LTS trên VMware.

Cấu hình:

- CPU: 2 vCPU
- Disk: 20 GB
- Hostname: `web-proxy`
- Username: `lab7`

Kiểm tra phiên bản hệ điều hành:

```bash
cat /etc/os-release
```

Kiểm tra card mạng:

```bash
ip a
```

Kết quả: Ubuntu Server 24.04.3 LTS được cài đặt và đăng nhập thành công.

### Bước 4: Cấu hình mạng WEB-PROXY

Kết nối Network Adapter của Ubuntu vào LAN Segment `lab6-lan`.

Mở file Netplan:

```bash
sudo nano /etc/netplan/50-cloud-init.yaml
```

Cấu hình IP tĩnh:

```yaml
network:
  version: 2
  ethernets:
    ens33:
      dhcp4: false
      addresses:
        - 10.6.0.30/24
      routes:
        - to: default
          via: 10.6.0.1
      nameservers:
        addresses:
          - 10.6.0.10
```

Áp dụng cấu hình:

```bash
sudo chmod 600 /etc/netplan/50-cloud-init.yaml
sudo netplan generate
sudo netplan apply
```

Kiểm tra kết nối:

```bash
ip a
ping -c 4 10.6.0.1
ping -c 4 10.6.0.10
```

**Trạng thái:** Đã được hướng dẫn cấu hình, chưa có ảnh xác nhận kết quả ping thành công.

### Bước 5: Triển khai Web Proxy

Theo yêu cầu bài LAB, Web Proxy sử dụng ba thành phần:

- Squid: Forward Proxy.
- E2Guardian: Lọc nội dung và kiểm soát truy cập website.
- ClamAV: Quét virus trong nội dung tải xuống.

Lệnh cài đặt dự kiến:

```bash
sudo apt update
sudo apt install -y squid e2guardian clamav clamav-daemon curl openssl
```

Luồng xử lý:

Client → E2Guardian (8080) → Squid (3128) → pfSense → Website.

**Trạng thái:** Chưa có minh chứng hoàn tất cài đặt và cấu hình dịch vụ.

### Bước 6: Xây dựng chính sách Web Protection

Theo tài liệu LAB 7, các chính sách cần kiểm thử gồm:

| Chính sách | Website kiểm thử | Kết quả mong đợi |
|---|---|---|
| Allow | normal.lab7.test | Cho phép |
| Hard Block | jobs.lab7.test | Chặn |
| Geo Block | china.lab7.test | Chặn |
| Warning | politics.lab7.test | Cảnh báo |
| Whitelist | education.lab7.test | Cho phép |
| Schedule | games.lab7.test | Theo khung giờ |
| Antivirus | download.lab7.test | Quét file EICAR |
| Download Limit | File 100 MB / 110 MB | Kiểm tra giới hạn tải |

**Trạng thái:** Đây là các kịch bản yêu cầu theo tài liệu, chưa phải kết quả kiểm thử thực tế.

## 4. Hình ảnh minh chứng

Các hình ảnh cần đưa vào báo cáo:

1. Danh sách máy ảo trong VMware.
2. Kiểm tra phiên bản Ubuntu Server 24.04.3 LTS.
3. Cấu hình các interface trên pfSense.
4. Cấu hình LAN Segment cho WEB-PROXY.
5. Cấu hình IP tĩnh và kiểm tra ping.
6. Cài đặt và kiểm tra dịch vụ Proxy.
7. Cấu hình Firewall Rules.
8. Kết quả kiểm thử website được phép và bị chặn.
9. Kiểm thử cảnh báo, Schedule và Antivirus.
10. Kiểm tra log hoạt động.

Các ảnh 1–4 đã có từ quá trình thực hành. Những ảnh còn lại cần bổ sung khi hoàn tất các bước tương ứng.

## 5. Kết quả thực hiện

**Đã hoàn thành:**

- Chuẩn bị môi trường máy ảo VMware.
- Kiểm tra pfSense 2.7.2 và các interface mạng.
- Cài đặt Ubuntu Server 24.04.3 LTS.
- Tạo tài khoản `lab7` và hostname `web-proxy`.
- Cấu hình VMware Network Adapter vào LAN Segment `lab6-lan`.

**Đang thực hiện hoặc chưa xác minh:**

- Áp dụng IP tĩnh và kiểm tra ping.
- Cài đặt Squid, E2Guardian và ClamAV.
- Cấu hình website mô phỏng và DNS.
- Tạo Firewall Rules chống bypass.
- Thiết lập và kiểm thử các chính sách Web Protection.
- Thu thập log và hoàn thiện minh chứng.

## 6. Kết luận

Qua quá trình thực hành LAB 7, sinh viên đã bước đầu xây dựng môi trường mạng ảo phục vụ triển khai giải pháp Web Protection kết hợp giữa pfSense và Ubuntu Server.

Việc sử dụng pfSense kết hợp Web Proxy giúp phân tách chức năng kiểm soát kết nối mạng và lọc nội dung Web. Sau khi hoàn tất các chính sách và kiểm thử, mô hình sẽ hỗ trợ đánh giá khả năng chặn website, ngăn truy cập vượt Proxy, kiểm tra file tải xuống và giám sát hoạt động truy cập.

Các nội dung chưa hoàn thành cần tiếp tục triển khai và kiểm chứng bằng kết quả thực tế trước khi kết luận toàn bộ LAB 7 đạt yêu cầu.
