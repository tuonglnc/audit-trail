---
title: ""
date: YYYY-MM-DD
type: defense
tags: []
# defensive tags: detection, sigma, yara, siem, dfir, threat-hunting, hardening
status: inbox
rule_type: ""   # sigma | yara | suricata | splunk-spl | kql | manual
tested_on: ""   # platform/env đã test
refs:
  - url: ""
    title: ""
---

## threat

<!-- Cái gì đang được detect/mitigate?
     Link sang vuln note hoặc concept note tương ứng. -->

- attack: [[vulns/...]]
- technique: [[concepts/...]]

## detection logic

<!-- Rule, query, hoặc điều kiện trigger.
     Đặt trong code block với syntax highlight phù hợp. -->

```yaml
# Sigma rule / YARA / SPL / KQL
```

**Tại sao rule này work:** ...

## false positive risk

<!-- Quan trọng — cái gì có thể trigger nhầm trong môi trường bình thường?
     Defender giỏi phân biệt bởi vì họ nghĩ về FP trước khi deploy rule. -->

- FP scenario 1: ...
- mitigation: ...

## coverage gaps

<!-- Evasion nào không cover được?
     Attacker có thể bypass rule này bằng cách nào?
     Honest về giới hạn. -->

- ...

## response actions

<!-- Khi rule trigger, làm gì tiếp theo? -->

1. ...
2. ...

## tested on

<!-- Môi trường, dataset, hoặc machine đã dùng để verify rule hoạt động. -->

- env: ...
- test case: [[writeups/...]]   <!-- HTB/CTF machine có attack này -->

## related

- vuln: [[vulns/...]]
- concept: [[concepts/...]]
- tool: [[tools/...]]           <!-- tool dùng để implement/test rule -->
