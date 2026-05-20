---
title: ""
date: YYYY-MM-DD
type: vuln
tags: []
# bug class tags: heap-overflow, stack-overflow, uaf, race-condition, sqli, xss, ssrf, deserialization, privesc, lpe
status: inbox
cve: ""           # CVE-YYYY-NNNNN hoặc kosong
cvss: 0.0
affected: ""      # product + version bị ảnh hưởng
bug_class: ""     # heap-overflow | sqli | race-condition | ...
refs:
  - url: ""
    title: ""
---

## one-liner

> Attacker [có gì / điều kiện] → có thể [làm gì cụ thể] → ảnh hưởng [ai / system / data] — nếu [precondition]

<!-- Format bắt buộc. Nếu không điền được = chưa hiểu đủ impact. -->

## root cause

<!-- 1 đoạn ngắn. Không phải walkthrough — chỉ là nguyên nhân gốc rễ.
     Ví dụ: "Integer overflow khi parse length field do cast i16 → u32,
     cho phép attacker control size argument của memcpy phía sau." -->

## vulnerable code path

```
# Call chain từ entry point đến sink
# Chỉ cần đủ để thấy luồng, không cần full code

entry() → parse_input() → process() → vulnerable_sink()  ← bug ở đây
```

```c
// Snippet ngắn tại điểm vulnerable nếu có source
```

## exploitation

<!-- Primitive → chain → impact.
     Primitive: cái bug cho phép làm gì (read/write primitive, crash...)
     Chain: làm thế nào để biến primitive thành exploit
     Impact: cuối cùng đạt được gì -->

**primitive:** ...
**chain:** ...
**impact:** ...

## patch analysis

<!-- Fix dùng cách gì? Bounds check? Type change? Locking?
     Tradeoff là gì? Có edge case nào fix bỏ sót không?
     Quan trọng cho research — hiểu fix = hiểu bug sâu hơn. -->

## detection signals

<!-- Exploit này để lại trace gì để defender detect?
     Điền sau khi hiểu exploitation xong. -->

- network: ...
- host: ...
- log: ...
- ioc: ...

## blind spots

- [ ] ...

## related

- concept: [[concepts/...]]       <!-- underlying tech -->
- detection: [[defense/detection/...]]
- writeup: [[writeups/...]]       <!-- machine/CTF dùng bug class này -->
