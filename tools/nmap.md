# Nmap — Cheat Sheet

> **Status:** 🔴 todo  
> **Tags:** #tools #recon #scanning  
> **Domino:** `Networking Basics` → **`Nmap`** → (dùng trong mọi bước recon)

---

## CHỌN — 20/80 cần nhớ

```bash
nmap -sC -sV -oN scan.txt TARGET    ← lệnh dùng 90% thời gian
```
- `-sC` = chạy default scripts
- `-sV` = detect version service
- `-oN` = lưu output ra file

---

## Các lệnh theo tình huống

```bash
# --- RECON CƠ BẢN ---
nmap TARGET                          # scan 1000 port phổ biến
nmap -p- TARGET                      # scan all 65535 ports (chậm)
nmap -p 80,443,8080 TARGET           # scan port cụ thể

# --- SERVICE & SCRIPT (hay dùng nhất) ---
nmap -sC -sV TARGET                  # default scripts + version
nmap -sC -sV -p- TARGET             # full scan + version (chậm nhưng đủ)
nmap -sC -sV -oN scan.txt TARGET    # + lưu output

# --- SPEED ---
nmap -T4 TARGET                      # nhanh hơn (T0 chậm nhất, T5 nhanh nhất)
nmap -T4 -p- --min-rate 5000 TARGET  # nhanh nhất, dễ bị detect

# --- SCAN TYPE ---
nmap -sS TARGET                      # SYN scan (stealth, cần root)
nmap -sU TARGET                      # UDP scan (chậm, nhưng DNS/SNMP dùng UDP)
nmap -sn 192.168.1.0/24             # ping scan, tìm host nào online

# --- SCRIPT CỤ THỂ ---
nmap --script vuln TARGET            # scan lỗ hổng phổ biến
nmap --script smb-vuln* TARGET       # SMB vulnerabilities
nmap --script http-enum TARGET       # enumerate web paths

# --- OUTPUT ---
nmap -oN output.txt TARGET           # normal
nmap -oX output.xml TARGET           # XML
nmap -oG output.gnmap TARGET         # grepable
nmap -oA output TARGET               # tất cả format
```

---

## Workflow HTB thực tế

```bash
# Bước 1: quick scan để biết port nào mở
nmap -T4 --min-rate 5000 -p- TARGET -oN ports.txt

# Bước 2: deep scan trên port đã tìm được
nmap -sC -sV -p 22,80,443 TARGET -oN detailed.txt

# Bước 3: nếu có web server, thêm http scripts
nmap --script http-enum,http-headers -p 80,443 TARGET
```

---

## Đọc output

```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1
80/tcp open  http    Apache httpd 2.4.41
                     ↑ service      ↑ version → tra CVE cho version này
```

---

## Nhớ nhanh — 1 câu

> `nmap -sC -sV -oN scan.txt TARGET` là lệnh 90% trường hợp; thêm `-p-` nếu cần scan hết port.
