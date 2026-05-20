# [Tên Machine] — HTB Writeup

> **Status:** 🔴 todo  
> **Difficulty:** Easy / Medium / Hard  
> **OS:** Linux / Windows  
> **Tags:** #htb #writeup #[tag]  
> **Date:** YYYY-MM-DD

---

## TL;DR (đọc cái này trước)

> Tóm tắt attack path trong 3 dòng:  
> 1. Recon → phát hiện [gì đó]  
> 2. Foothold qua [vuln nào]  
> 3. PrivEsc bằng [cách gì]

---

## Recon

```bash
nmap -sC -sV -oN scan.txt TARGET_IP
```

**Kết quả:** (ghi lại port/service quan trọng)
- Port X: service Y version Z
- Port X: ...

---

## Foothold

**Phát hiện:** (tìm thấy gì, ở đâu)

**Khai thác:**
```bash
# lệnh đã dùng
```

**Shell lấy được:** user `___`

---

## User Flag

```bash
cat /home/[user]/user.txt
```

---

## Privilege Escalation

**Vector:** (SUID? cron? sudo? service?)

**Khai thác:**
```bash
# lệnh đã dùng
```

---

## Root Flag

```bash
cat /root/root.txt
```

---

## Bài học rút ra

> *Phần quan trọng nhất — ghi lại để nhớ lâu*

- **Điều mới học được:**
- **Tool/technique lần đầu dùng:**
- **Nếu là defender, detect attack này bằng:**
- **Lần sau gặp machine tương tự, làm gì trước?**
