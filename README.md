# EDU-NET: Hệ thống mạng Trung tâm đào tạo CNTT tập trung

Dự án này trình bày mô hình thiết kế và triển khai hạ tầng mạng cho trung tâm đào tạo CNTT EDU-NET, giải quyết vấn đề quản trị thủ công và xung đột địa chỉ IP khi mở rộng quy mô phòng Lab.

## 📋 Mục tiêu dự án
* Xây dựng mô hình hạ tầng mạng trên nền tảng **GNS3** kết hợp ảo hóa **Windows Server 2022**.
* Phân chia **VLAN** để tối ưu hóa hiệu suất và giảm thiểu Broadcast Domain.
* Triển khai **DHCP Relay Agent** để tập trung hóa quản lý cấp phát địa chỉ IP.
* Thiết lập chính sách bảo mật cơ bản bằng **Standard ACL** để bảo vệ thiết bị định tuyến lõi.

## 🛠 Thành phần hệ thống
* **Máy chủ:** Windows Server 2022 (vai trò Domain Controller và DHCP Server).
* **Thiết bị mạng:**
    * 01 Core Switch Layer 3 (định tuyến Inter-VLAN và chuyển tiếp DHCP).
    * 05 Access Switch Layer 2 (phục vụ các phòng Lab và khu Văn phòng).
* **Phần mềm:** GNS3 (giả lập mạng).

## 🌐 Quy hoạch mạng (Subnetting)

| Khu vực | VLAN ID | Network Address | Default Gateway |
| :--- | :--- | :--- | :--- |
| Lab 1 | 10 | 192.168.10.0/26 | 192.168.10.1 |
| Lab 2 | 20 | 192.168.10.64/26 | 192.168.10.65 |
| Lab 3 | 30 | 192.168.10.128/26 | 192.168.10.129 |
| Lab 4 | 40 | 192.168.10.192/26 | 192.168.10.193 |
| Văn phòng | 50 | 192.168.20.0/24 | 192.168.20.1 |
| IT/Server | 99 | 192.168.99.0/24 | 192.168.99.1 |

## 🚀 Các tính năng chính
1.  **Inter-VLAN Routing:** Sử dụng Core Switch L3 để định tuyến giữa các VLAN.
2.  **DHCP tập trung:** Sử dụng `ip helper-address` trên Core Switch để chuyển tiếp yêu cầu DHCP từ các VLAN về DHCP Server.
3.  **Bảo mật quản trị:** Cấu hình **Standard ACL** trên đường VTY để chỉ cho phép IT Admin (dải mạng 192.168.99.0/24) được quyền truy cập Telnet.

## 👥 Nhóm thực hiện (Lớp 14DHBM01)
* Trương Lê Trúc Quỳnh (2033230246)
* Lê Ngọc Phương Quỳnh (2033230247)
* Đào Thị Khánh Chi (2033230035)
* Tống Lạc Lan Viên (2033230322)
