# Networking Basics — TCP/IP, DNS, HTTP

> **Status:** 🟢 done  
> **Tags:** #networking #fundamentals  
> **Nguồn:** TryHackMe Pre-Security + HTB Academy  
> **Domino:** *(bắt đầu từ đây)* → **`Networking`** → `Linux Basics`

---

## CHIA — Câu hỏi cần trả lời

- Dữ liệu đi từ máy này sang máy kia như thế nào?
- Attacker có thể chen vào ở điểm nào?
- Tại sao biết TCP/IP lại giúp hiểu được khai thác mạng?

---

## CHỌN — 20/80 cần nhớ

**Mô hình OSI** = 7 tầng, mỗi tầng là 1 điểm có thể tấn công hoặc phòng thủ.  
**TCP handshake** = SYN → SYN-ACK → ACK. Không hoàn thành = không kết nối.  
**IP** = địa chỉ lớp 3 (định tuyến). **MAC** = địa chỉ lớp 2 (trong mạng nội bộ).  
**DNS** = dịch tên miền → IP. Đây là nguồn tấn công và exfiltration hay bị bỏ qua.  
**HTTP** = giao thức không có trạng thái, dữ liệu đi dạng plaintext (HTTP, không phải HTTPS).

---

## CHUỖI — Chi tiết + Thực hành

### Mô hình OSI — nhớ bằng: *"Please Do Not Throw Sausage Pizza Away"*

| Tầng | Tên | Protocol thực tế | Attack ở đây |
|------|-----|-----------------|--------------|
| 7 | Application | HTTP, DNS, FTP, SMTP | Web attacks, phishing |
| 6 | Presentation | SSL/TLS, encoding | SSL stripping |
| 5 | Session | SMB, RPC | Session hijacking |
| 4 | Transport | TCP, UDP | SYN flood, port scan |
| 3 | Network | IP, ICMP | IP spoofing, routing attacks |
| 2 | Data Link | ARP, MAC | ARP poisoning, MAC spoofing |
| 1 | Physical | Cable, WiFi | Packet sniffing (WiFi) |

### TCP 3-way Handshake

```
Client  →  SYN       →  Server      (tôi muốn kết nối)
Client  ←  SYN-ACK   ←  Server      (ok, tôi sẵn sàng)
Client  →  ACK       →  Server      (bắt đầu thôi)
```

> **SYN Flood attack:** gửi hàng nghìn SYN, không bao giờ gửi ACK cuối → server bị "treo" chờ, cạn resource (half-open connections).

### DNS — thường bị quên trong pentest

```
Browser hỏi: "google.com là IP gì?"
DNS trả lời: "142.250.x.x"

Attack vectors:
- DNS Spoofing: trả lời sai IP → redirect user
- DNS Exfiltration: nhét data vào DNS query để bypass firewall
- Zone Transfer: nếu misconfigure → lộ toàn bộ subdomain
```

### Lệnh thực hành

```bash
# Xem traffic real-time
tcpdump -i eth0 -n
tcpdump -i eth0 port 80 -w capture.pcap   # lưu ra file

# Thông tin DNS
dig google.com
dig google.com MX          # mail server
dig axfr @ns1.target.com target.com   # zone transfer (nếu được phép)

# Scan mạng (xem ai đang online)
nmap -sn 192.168.1.0/24

# Xem kết nối đang mở
ss -tulpn
netstat -tulpn

# Trace đường đi packet
traceroute 8.8.8.8
```

---

## Associate — Liên kết với thứ đã biết

- **TCP handshake** → liên quan trực tiếp đến SYN flood, Nmap scan (Nmap dùng SYN để scan)
- **DNS** → liên quan đến DNS spoofing, subdomain enumeration, DNS exfiltration
- **HTTP headers** → nơi XSS, CSRF, SSRF hay xảy ra (Host header, Cookie, Origin)
- **ARP** → liên quan đến Man-in-the-Middle attack trong mạng nội bộ
- Giống như hệ thống bưu chính: **IP** = địa chỉ nhà, **MAC** = tên người nhận trong tòa nhà, **DNS** = danh bạ điện thoại

---

## Nhớ nhanh — 1 câu

> Mạng = data được đóng gói qua 7 tầng từ nguồn đến đích; mỗi tầng là 1 chỗ attacker có thể chen vào và defender có thể kiểm soát.

---

## Xem thêm (đã lọc 20/80)

- [ ] [TryHackMe - Pre-Security Path](https://tryhackme.com/path/outline/presecurity) ← bắt đầu từ đây
- [ ] [Wireshark 101 - HTB Academy](https://academy.hackthebox.com/module/details/81)
- [ ] [tcpdump cheat sheet](https://danielmiessler.com/study/tcpdump/)
