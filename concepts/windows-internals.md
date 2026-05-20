# Windows Internals — Auth, Processes, Registry

> **Status:** 🔴 todo  
> **Tags:** #windows #internals #fundamentals  
> **Nguồn:** HTB Academy - Windows Fundamentals  
> **Domino:** `Networking Basics` → **`Windows Internals`** → `PrivEsc Windows` → `Active Directory`

---

## CHIA — Câu hỏi cần trả lời

- Windows xác thực user bằng gì? Tại sao Pass-the-Hash lại hoạt động?
- LSASS là gì và tại sao Mimikatz target nó?
- Attacker hay tìm gì trong Registry?

---

## CHỌN — 20/80 cần nhớ

**LSASS process** = lưu credential trong memory → Mimikatz dump từ đây.  
**SAM database** = lưu local password hash tại `C:\Windows\System32\config\SAM`.  
**Access Token** = sau khi login, Windows tạo token đại diện identity → kiểm soát token = kiểm soát quyền.  
**Registry autorun keys** = nơi malware hay persistence.  
**NTLM vs Kerberos** = 2 cơ chế auth chính trong môi trường Windows/AD.

---

## CHUỖI — Chi tiết + Thực hành

### Kiến trúc User Mode vs Kernel Mode

```
User Mode    → Applications, Win32 API, LSASS, services
─────────────────────────────────────────────────────────
Kernel Mode  → NTOSKRNL.exe, drivers, HAL
```

> Malware muốn chạy ở kernel mode → cần driver (rootkit). Đó là lý do AV khó detect.

### Authentication Flow

```
User nhập password
      ↓
LSASS.exe xử lý
      ↓
So sánh với SAM (local) hoặc Domain Controller (AD)
      ↓
Tạo Access Token nếu đúng
      ↓
Token đính kèm vào mọi process của user
```

> **Pass-the-Hash:** không cần biết plaintext password, chỉ cần hash → authenticate được.  
> **Tại sao?** NTLM dùng hash trực tiếp để xác thực, không verify plaintext.

### Lệnh khảo sát Windows

```cmd
:: Thông tin hệ thống
systeminfo
whoami /all          :: user + privileges + groups

:: Users và groups
net user
net localgroup administrators

:: Processes
tasklist /v
Get-Process          :: PowerShell

:: Services (nơi hay có privesc)
sc query
Get-Service

:: Scheduled Tasks
schtasks /query /fo LIST /v
Get-ScheduledTask

:: Registry autorun (nơi malware persistence)
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run

:: Tìm file có thể ghi được
icacls "C:\Program Files" /T | findstr "Everyone"

:: Network
netstat -ano
```

### Nơi thường có PrivEsc

| Vector | Tại sao nguy hiểm | Kiểm tra bằng |
|--------|-------------------|---------------|
| Unquoted Service Path | Windows load nhầm binary | `wmic service get name,pathname` |
| Weak Service Permissions | Ghi đè binary của service | `accesschk.exe -uwcqv *` |
| AlwaysInstallElevated | MSI chạy với SYSTEM | `reg query HKLM\...\Installer` |
| Writable PATH | Hijack command | `echo %PATH%` |
| DLL Hijacking | Load DLL của mình | Process Monitor |
| Scheduled Tasks | Task chạy với quyền cao | `schtasks /query` |

---

## Associate — Liên kết với thứ đã biết

- **LSASS** → Mimikatz target trực tiếp → dump NTLM hash, Kerberos tickets
- **SAM + SYSTEM file** → offline crack với secretsdump
- **Access Token** → `token impersonation` attacks (Juicy/Rotten/PrintSpoofer Potato)
- Giống Linux: Windows cũng có "SUID equivalent" → Services chạy với SYSTEM

---

## Nhớ nhanh — 1 câu

> Windows auth = password → LSASS → hash/token; lấy được hash hoặc token là lấy được identity — không cần biết plaintext password.

---

## Xem thêm

- [ ] [HTB Academy - Windows Fundamentals](https://academy.hackthebox.com/module/details/49)
- [ ] [LOLBAS Project](https://lolbas-project.github.io) — Living-off-the-land binaries
- [ ] [PayloadsAllTheThings - Windows PrivEsc](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md)
