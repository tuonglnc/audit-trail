# 🛡️ CyberTun — Notebook học Cybersecurity


## 🗺️ Chuỗi Domino

> *"Đâu là quân domino làm mọi thứ khác dễ đi?"* — Tim Vũ

```
[1] Networking   →   [2] Linux   →   [3] Web Vulns   →   [4] System Hacking   →   [5] Thực chiến HTB
```

Mỗi bước là nền cho bước sau. Biết networking mới hiểu được traffic khi hack. Biết Linux mới chạy được tool.

---

## 📂 Cấu trúc 

| Folder | Nội dung |
|--------|----------|
| [`concepts/`](./concepts/) | Lý thuyết nền — **tại sao** thứ đó hoạt động |
| [`vulns/`](./vulns/) | Phân tích lỗ hổng — CVE, bug class, cách khai thác |
| [`writeups/`](./writeups/) | HTB, CTF — từng bước + bài học rút ra |
| [`tools/`](./tools/) | Cheat sheet — tra nhanh, dùng ngay |
| [`reading/`](./reading/) | Tóm tắt sách, blog, paper quan trọng |

---

## 📋 Checklist học (tick khi xong)

### 🟢 Phase 1 — Nền tảng (Domino đầu tiên)
- [ ] [`concepts/networking-basics.md`](./concepts/networking-basics.md) — TCP/IP, DNS, HTTP
- [ ] [`concepts/linux-basics.md`](./concepts/linux-basics.md) — Filesystem, permissions, bash
- [ ] [`concepts/windows-internals.md`](./concepts/windows-internals.md) — Auth, processes, registry
- [ ] [`tools/nmap.md`](./tools/nmap.md) — Scan mạng

### 🟡 Phase 2 — Web Security (20/80 nhất cho pentest)
- [ ] [`vulns/web-owasp-top10.md`](./vulns/web-owasp-top10.md) — Bức tranh tổng
- [ ] [`vulns/sqli.md`](./vulns/sqli.md) — SQL Injection
- [ ] [`vulns/xss.md`](./vulns/xss.md) — Cross-Site Scripting
- [ ] [`vulns/ssrf.md`](./vulns/ssrf.md) — SSRF
- [ ] [`tools/burpsuite.md`](./tools/burpsuite.md) — Tool không thể thiếu

### 🔴 Phase 3 — System Hacking
- [ ] [`vulns/privesc-linux.md`](./vulns/privesc-linux.md) — Leo thang đặc quyền Linux
- [ ] [`vulns/privesc-windows.md`](./vulns/privesc-windows.md) — Leo thang đặc quyền Windows
- [ ] [`concepts/active-directory.md`](./concepts/active-directory.md) — AD cơ bản
- [ ] [`tools/metasploit.md`](./tools/metasploit.md) — Framework khai thác

### ⚫ Phase 4 — Thực chiến
- [ ] Hoàn thành HTB machine đầu tiên → ghi vào `writeups/`
- [ ] Hoàn thành 5 HTB machines
- [ ] Thử OSCP labs

---

## 📥 Inbox — Ghi nhanh, phân loại sau

→ Xem [`inbox.md`](./inbox.md)

---

## 📌 Cách ghi 1 note mới (template 3C)

Copy [`_template.md`](./_template.md) → điền 3 phần:
1. **Chia** — Câu hỏi nào cần trả lời? Chia nhỏ ra thế nào?
2. **Chọn** — 20/80: phần nào quan trọng nhất?
3. **Chuỗi** — Phải biết gì trước? Dẫn đến gì tiếp theo?

---

## 🔗 Tài nguyên 20/80 (đã lọc)

| Tài nguyên | Dùng cho |
|------------|----------|
| [HTB Academy](https://academy.hackthebox.com) | Học có cấu trúc, free nhiều module |
| [TryHackMe](https://tryhackme.com) | Người mới, có lộ trình rõ |
| [PortSwigger Web Academy](https://portswigger.net/web-security) | Web security tốt nhất hiện tại, miễn phí |
| [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings) | Tra payload nhanh |
| [GTFOBins](https://gtfobins.github.io) | PrivEsc Linux — tra binary |
| [LOLBAS](https://lolbas-project.github.io) | PrivEsc Windows |

---

*Status: 🟢 đọc xong · 🟡 đang học · 🔴 chưa đụng*
