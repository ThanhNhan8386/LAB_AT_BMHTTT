# LAB3 - NHẬN DIỆN VÀ ỨNG PHÓ CÁC MỐI ĐE DỌA ĐẾN AN TOÀN THÔNG TIN

## 1. Thông tin sinh viên

- Họ và tên: Nguyễn Lại Thành
- MSSV: 1150080151
- Lớp: 11DH_CNPM2
- Tên bài Lab: LAB3 - Nhận diện và ứng phó các mối đe dọa đến An toàn thông tin

---

## 2. Mục tiêu bài thực hành

Bài thực hành nhằm:

- Phân biệt các khái niệm Asset, Vulnerability, Threat, Risk và Attack.
- Nhận diện các nhóm mối đe dọa đến an toàn thông tin.
- Quan sát và thu thập bằng chứng liên quan đến:
  - Malware
  - Password attack
  - Keylogging
  - Backdoor / Persistence
  - Sniffing
  - MITM / Spoofing
  - DoS / DDoS
  - Mail Bombing
  - Social Engineering / Phishing
- Sử dụng các công cụ Windows Defender, Event Viewer, Sysmon, Autoruns, Process Explorer và Wireshark để thu thập bằng chứng.
- Thực hiện quy trình:
  Baseline → Observe → Detect → Contain → Recover → Verify.

---

## 3. Môi trường thực hành

### Máy ảo

- VMware Workstation Pro: 26H1
- Guest OS: Windows 11 Education
- Version: 25H2
- OS Build thực tế: 26200.9457
- CPU: 2 vCPU
- RAM: 6 GB
- Disk: 64 GB
- Network Adapter: Host-only
- Snapshot: `LAB3_CLEAN_20260914`

### Công cụ

| Công cụ | Phiên bản |
|---|---|
| Microsoft Defender Antivirus | Tích hợp Windows 11 |
| Windows PowerShell | 5.1 |
| Python | 3.14.7 |
| Wireshark | 4.6.8 |
| Sysmon | 15.22 |
| Autoruns | 14.3 |
| Process Explorer | 17.14 |

> Lưu ý: Phiên bản công cụ được kiểm tra trực tiếp trên máy ảo trước khi thực hành.

---

## 4. Cấu trúc thư mục

```text
C:\LAB3
├── Assets
├── Downloads
├── Evidence
├── Tools
└── lab3_assets
    ├── data
    ├── samples
    ├── scripts
    ├── www
    ├── sysmon-lab.xml
    └── README.txt
