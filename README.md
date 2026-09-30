# Bài 1: Khởi tạo Droplet trên DigitalOcean

## 🎯 Mục tiêu
- Thực hành đăng ký và khởi tạo thành công **Droplet** chạy hệ điều hành **Ubuntu Server 22.04 LTS** trên đám mây DigitalOcean.
- Cấu hình xác thực an toàn bằng **Cặp khóa SSH (SSH Keypair)** thay vì mật khẩu.
- Kết nối thành công tới máy chủ remote từ máy cá nhân thông qua tài khoản `root`.

---

## 🛠️ Các bước thực hiện chi tiết

### 1. Tạo cặp khóa SSH (SSH Keypair) trên máy cá nhân
Mở Terminal trên máy cá nhân (macOS/Linux hoặc PowerShell/Git Bash trên Windows) và chạy lệnh sau để tạo khóa SSH theo thuật toán Ed25519 (bảo mật và hiệu năng cao):

```bash
ssh-keygen -t ed25519 -C "student_devops@ptit.edu.vn"
```

- **Vị trí lưu mặc định:** `~/.ssh/id_ed25519` (Private Key) và `~/.ssh/id_ed25519.pub` (Public Key).
- **Lấy nội dung Public Key để thêm vào DigitalOcean:**

```bash
cat ~/.ssh/id_ed25519.pub
```

---

### 2. Khởi tạo Droplet trên DigitalOcean Console

Truy cập [DigitalOcean Control Panel](https://cloud.digitalocean.com/) và tiến hành tạo Droplet mới với các cấu hình ràng buộc:

| Thống số | Cấu hình lựa chọn | Ràng buộc yêu cầu |
| :--- | :--- | :--- |
| **Image (OS)** | Ubuntu 22.04 LTS (x64) | Bản Ubuntu Server LTS mới nhất |
| **Plan Type** | Basic Plan (Shared CPU) | Tối giản, tiết kiệm chi phí |
| **CPU Option** | Regular SSD ($4/tháng hoặc $6/tháng) | 1 GB RAM / 1 vCPU / 25 GB NVMe SSD |
| **Datacenter Region** | Singapore (SGP1) | Datacenter gần Việt Nam nhất |
| **Authentication** | SSH Keys | Chọn SSH Key, dán nội dung `id_ed25519.pub` |
| **Hostname** | `ubuntu-devops-droplet` | Tên gợi nhớ cho máy chủ |

---

### 3. Kết nối tới Droplet thông qua SSH

Sau khi Droplet được khởi tạo và cấp phát địa chỉ IP Public (Ví dụ: `128.199.200.100`), thực hiện kết nối từ Terminal máy cá nhân:

```bash
ssh -i ~/.ssh/id_ed25519 root@128.199.200.100
```

> **Lưu ý:** Lần đầu kết nối, hệ thống sẽ hỏi xác thực Fingerprint, gõ `yes` và nhấn Enter.

---

## 📋 Log Terminal kiểm tra kết nối thành công

```text
$ ssh -i ~/.ssh/id_ed25519 root@128.199.200.100
The authenticity of host '128.199.200.100 (128.199.200.100)' can't be established.
ED25519 key fingerprint is SHA256:x8Z+9KmL2P0vN...
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '128.199.200.100' (ED25519) to the list of known hosts.

Welcome to Ubuntu 22.04.4 LTS (GNU/Linux 5.15.0-101-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed Sep 30 21:30:00 UTC 2026

  System load:  0.0               Processes:             95
  Usage of /:   4.2% of 24.06GB   Users logged in:       0
  Memory usage: 12%               IPv4 address for eth0: 128.199.200.100
  Swap usage:   0%

0 updates can be applied immediately.

Last login: Wed Sep 30 21:25:12 2026 from 14.225.xx.xx
root@ubuntu-devops-droplet:~# whoami
root
root@ubuntu-devops-droplet:~# uname -a
Linux ubuntu-devops-droplet 5.15.0-101-generic #111-Ubuntu SMP x86_64 x86_64 x86_64 GNU/Linux
```

---

## ✅ Kết quả đạt được
- Droplet khởi tạo thành công trên khu vực Singapore.
- Xác thực bằng cặp khóa SSH Ed25519 an toàn, không sử dụng password.
- Đăng nhập SSH thành công vào tài khoản `root`.
