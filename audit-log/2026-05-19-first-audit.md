# 🔍 [google/atheris](https://github.com/google/atheris) — 19/05/2026

> **Type:** `[x] Fuzzing`
> **Target lang:** `[x] Python` (+ C/C++ extensions via native hooks)
> **Severity:** N/A — tool research
> **Status:** `[x] Reading`

---

## 📌 1. Context — Cái này tồn tại để giải quyết vấn đề gì?

<!-- TODO: Fill in sau khi đọc repo -->
> *Gợi ý để nghĩ: Tại sao fuzzing Python khó hơn C? libFuzzer giải quyết gì? Coverage-guided fuzzing là gì?*

## 🧨 2. Threat model — Nếu không có atheris, chuyện gì xảy ra?

<!-- TODO -->
> *Gợi ý: Python lib không được fuzz → bug tồn tại lâu không ai phát hiện. Loại bug nào atheris tìm được mà unit test không tìm được?*

## 💡 3. Discovery — Hôm nay mình thấy gì mới?

<!-- TODO -->

## ⚙️ 4. Mechanism — Atheris hoạt động như thế nào?

<!-- TODO -->
> *Gợi ý để đào: Atheris dùng libFuzzer làm engine. Python bytecode được instrument như thế nào? `atheris.instrument_all()` làm gì? Coverage signal được collect ra sao?*

```python
# Minimal atheris harness — đọc và hiểu từng dòng
import atheris
import sys

def TestOneInput(data):
    fdp = atheris.FuzzedDataProvider(data)
    # target code here

atheris.Setup(sys.argv, TestOneInput)
atheris.Fuzz()
```

## 🔁 5. Reproduce — Chạy atheris lần đầu

```bash
# Setup
pip install atheris

# Chạy thử với target đơn giản
python my_fuzzer.py

# Nếu tìm được crash
python my_fuzzer.py crash-<hash>
```

## ❓ 6. Blind spots — Chưa hiểu

- [ ] `FuzzedDataProvider` API — các method và khi nào dùng cái nào?
- [ ] Atheris instrument C extensions như thế nào? (native hooks)
- [ ] Corpus management — seed corpus là gì, lưu ở đâu?
- [ ] Coverage metric — atheris dùng edge coverage hay block coverage?

## 🗣️ 7. ELI5

<!-- TODO: Giải thích atheris như cho người chưa biết fuzzing -->

## 🔭 8. So what?

<!-- TODO: Atheris fit vào research của mình như thế nào? Target nào mình sẽ fuzz? -->

## 🔗 References

- https://github.com/google/atheris
- https://security.googleblog.com/2020/12/how-atheris-python-fuzzer-works.html
- LibFuzzer docs: https://llvm.org/docs/LibFuzzer.html

## ⏭️ Next

- [ ] Đọc `atheris/` source code — hiểu `instrument_all()` implementation
- [ ] Viết harness đơn giản cho 1 Python lib bạn đang dùng
- [ ] Đọc 1 writeup về bug được tìm bằng atheris

---
*Logged: 2026-05-19 | Spent: [X hrs]*
