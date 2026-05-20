---
title: ""
date: YYYY-MM-DD
type: concept
tags: []
# domain tags: windows, linux, web, network, binary, mobile, cloud, active-directory
# technique tags: reversing, fuzzing, static-analysis, dynamic-analysis, forensics, memory-analysis
status: inbox
refs:
  - url: ""
    title: ""
---

## mental model

> [Cơ chế X là ... vì ...]

<!-- 1 câu. Nếu không viết được = chưa hiểu đủ. Viết cái này trước tiên. -->

## background

<!-- Underlying technology làm cho concept này tồn tại.
     Ví dụ: trước khi giải thích heap overflow, giải thích heap allocator.
     Không giải thích concept chính ở đây — chỉ giải thích nền. -->

## how it works

<!-- Mechanism, data flow, call chain.
     Dùng pseudo-code hoặc diagram ASCII nếu cần.
     Tập trung vào "tại sao nó hoạt động vậy", không phải "làm thế nào để dùng". -->

```
# pseudo-code / call trace nếu có
```

## failure modes

<!-- Khi nào concept này bị khai thác hoặc fail.
     Đây là bridge sang vulns/ — link sang vuln notes cụ thể khi có. -->

- khi X thì Y xảy ra →  [[vulns/...]]

## detection signals

<!-- Nếu cơ chế này bị abuse, để lại trace gì?
     - network: packet pattern, anomaly
     - host: process behavior, file changes
     - log: event IDs, syscalls
     Để trống nếu chưa biết, fill sau. -->

- network: ...
- host: ...
- log: ...

## blind spots

<!-- Honest về những gì mình vẫn chưa hiểu. Ghi ra để research tiếp. -->

- [ ] ...
- [ ] ...

## related

<!-- Link chéo. Bidirectional — note kia cũng nên link về đây. -->

- concept: [[concepts/...]]
- vuln: [[vulns/...]]
- tool: [[tools/...]]
- defense: [[defense/...]]
