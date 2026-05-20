---
title: ""
date: YYYY-MM-DD
type: writeup
tags: []
status: inbox
platform: HTB   # HTB | CTF
difficulty: ""  # easy | medium | hard | insane
os: ""          # Linux | Windows | FreeBSD | ...
retired: true   # chỉ publish writeup khi machine đã retired
refs:
  - url: ""
    title: ""
---

## tldr

> foothold → privesc → root/flag qua [X] → [Y] → [Z]

<!-- Kill chain trong 3 dòng. Viết cái này trước — nếu không tóm tắt được
     nghĩa là chưa hiểu đủ rõ để viết writeup. -->

## recon

<!-- Chỉ ghi những gì dẫn đến exploitation — bỏ rabbit holes.
     Rabbit holes ghi ở section cuối nếu muốn.
     Tập trung vào: tìm thấy gì, từ đó suy ra gì. -->

## foothold

<!-- Làm thế nào vào được machine.
     Code snippet ngắn nếu cần — không paste toàn bộ script. -->

```bash
# command / payload chính
```

## privilege escalation

<!-- Từ low-priv lên root/SYSTEM.
     Nếu có nhiều bước, dùng sub-heading. -->

## what i learned

<!-- Section quan trọng nhất.
     - Technique/concept nào mới với mình?
     - Assumption nào bị sai?
     - Cái gì mình sẽ làm khác nếu làm lại?
     Link sang concept notes cho những thứ mới học. -->

- [[concepts/...]] — ...
- [[concepts/...]] — ...

## detection perspective

<!-- Nếu là defender/SOC analyst, detect attack này bằng gì?
     Đây là section differentiate defensive track.
     Link sang detection notes nếu đã có. -->

- bước X để lại dấu hiệu gì?
- event ID / log source nào liên quan?
- detection rule: [[defense/detection/...]]

## rabbit holes

<!-- Optional. Những hướng sai mình đã đi — để sau này đỡ lặp lại.
     Format: [thứ thử] → [tại sao không work] -->

- ...
