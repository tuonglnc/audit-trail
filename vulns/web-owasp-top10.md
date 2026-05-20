# OWASP Top 10 — Bức tranh tổng về Web Security

> **Status:** 🔴 todo  
> **Tags:** #web #owasp #overview  
> **Nguồn:** OWASP.org + PortSwigger Web Academy  
> **Domino:** `Networking Basics` → **`OWASP Top 10`** → `SQLi` → `XSS` → `SSRF`

---

## CHIA — Câu hỏi cần trả lời

- 10 lỗ hổng này cover được bao nhiêu % lỗ hổng web thực tế?
- Cái nào 20/80 nhất — cần học sâu trước?
- Cơ chế chung của web attacks là gì?

---

## CHỌN — 20/80 cần nhớ

Web attacks xảy ra vì **application tin tưởng input từ user**.  
20/80 nhất để học trước: **SQLi** (data exposure), **XSS** (chiếm session), **IDOR** (access control), **SSRF** (pivot vào internal).  
PortSwigger Web Academy = tài nguyên tốt nhất, miễn phí, có lab thực hành.

---

## CHUỖI — Bản đồ OWASP Top 10 (2021)

| # | Tên | Nguy hiểm vì | Ví dụ |
|---|-----|-------------|-------|
| A01 | Broken Access Control | User làm được việc không được phép | IDOR, path traversal |
| A02 | Cryptographic Failures | Data nhạy cảm bị lộ | HTTP thay HTTPS, MD5 hash |
| **A03** | **Injection** | **App chạy code/query của attacker** | **SQLi, Command Injection** |
| A04 | Insecure Design | Thiết kế logic sai từ đầu | Password reset flaws |
| A05 | Security Misconfiguration | Cài đặt mặc định, debug bật | Default creds, verbose errors |
| A06 | Vulnerable Components | Dùng library có lỗ hổng | Log4Shell, outdated plugins |
| A07 | Auth Failures | Xác thực/session quản lý kém | Brute force, weak tokens |
| **A08** | **Software Integrity Failures** | **Code/update không verify** | **Supply chain attacks** |
| **A09** | **Security Logging Failures** | **Không detect được attack** | **Không có audit log** |
| A10 | SSRF | Server gọi internal resource | Cloud metadata, internal APIs |

### Thứ tự học theo Chuỗi Domino

```
[SQLi] → [XSS] → [IDOR/Access Control] → [SSRF] → [File Upload] → [XXE]
   ↑                    ↑
   Học trước vì         Học sau vì cần hiểu HTTP/sessions trước
   cơ bản nhất
```

### Cơ chế chung — tại sao web app bị tấn công?

```
User input ──→ Application logic ──→ Backend (DB, OS, API)
                     ↑
              Attacker chen vào đây
              bằng cách inject malicious input
              mà app không sanitize
```

---

## Associate — Liên kết với thứ đã biết

- **Mọi web attack = app tin tưởng input quá nhiều** — giống SQL: nếu query nhận thẳng input từ user = bị SQLi
- **OWASP ≠ toàn bộ web security**, chỉ là top 10 phổ biến nhất
- **Burp Suite** = tool để intercept và modify HTTP request → lab thực hành mọi vuln ở đây

---

## Nhớ nhanh — 1 câu

> Web attack = app tin tưởng input của user mà không kiểm tra; mọi lỗ hổng đều có thể trace về 1 trong 10 category này.

---

## Xem thêm

- [ ] [PortSwigger Web Security Academy](https://portswigger.net/web-security) ← học sâu từng vuln
- [ ] [OWASP Top 10 2021](https://owasp.org/Top10/)
- [ ] [TryHackMe - OWASP Top 10](https://tryhackme.com/room/owasptop10)
