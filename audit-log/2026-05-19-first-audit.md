# 🔍 Audit Log — 19/05/2026

## TL;DR
> Hôm nay mình đọc google/oss-fuzz, tập trung vào project Pillow (thư viện xử lý ảnh Python).
> Kết luận: cách họ viết fuzz driver rất đơn giản — chỉ ~20 dòng, nhưng đủ tìm ra bug nghiêm trọng.
> Pipeline của họ khác thesis mình ở chỗ: họ fuzz mù, mình fuzz có hướng dẫn từ SAST.

---

## 📦 Repo này là gì?

- **Tên:** google/oss-fuzz
- **Link:** https://github.com/google/oss-fuzz
- **Nó làm gì:** Google chạy fuzzing liên tục — tức là tự động
  "ném" hàng triệu input ngẫu nhiên vào các thư viện mã nguồn mở
  để tìm chỗ bị crash hoặc lỗi. Khi tìm ra bug thì tự động báo
  cho người maintain thư viện đó.
- **Ai dùng nó:** Google vận hành, nhưng bất kỳ OSS project nào
  cũng có thể đăng ký để được fuzz miễn phí. Hiện có ~1000+ project
  đang được fuzz, trong đó ~80+ project Python.
- **Liên quan đến thesis mình chỗ nào:** Đây là nơi mình học được
  cách viết fuzz driver thực tế cho Python — cụ thể là dùng Atheris,
  đúng với stack thesis đang dùng.

---

## 🔎 Hôm nay mình đọc cái gì?

- **File:** `projects/pillow/fuzz_image.py`
- **Link:** https://github.com/google/oss-fuzz/blob/master/projects/pillow/fuzz_image.py
- **Mục tiêu ban đầu:** Hiểu fuzz driver thực tế trông như thế nào,
  so sánh với những gì thesis mình đang build
- **Thực tế tìm thấy:** Driver đơn giản hơn mình nghĩ rất nhiều.
  Ngoài ra tìm được 1 bug đã được fix liên quan đến JPEG decoder —
  đọc được full story từ fuzz → crash → fix.

---

## 💡 Mình hiểu được gì?

1. **Fuzz driver không cần phức tạp để hiệu quả.** Driver của
   Pillow chỉ làm 1 việc: nhận bytes ngẫu nhiên → mở như file ảnh
   → xem có crash không. Đơn giản vậy thôi mà tìm ra heap overflow.

2. **Atheris là standard cho Python fuzzing trong oss-fuzz.**
   Confirm rằng lựa chọn dùng Atheris trong thesis là đúng hướng,
   không phải mình tự nghĩ ra.

3. **Fuzz driver chỉ detect crash — không detect logic bug.**
   Đây là giới hạn của cách tiếp cận này. Muốn detect logic bug
   cần có assertion, tức là phải biết trước output đúng là gì —
   đây là chỗ LLM trong thesis mình có thể giúp được.

---

## ⚠️ Finding / Điểm đáng chú ý

- **Là gì:** Heap buffer overflow trong JPEG decoder của Pillow.
  Khi mở file ảnh JPEG bị hỏng header, chương trình cố đọc vùng
  nhớ không được phép → crash.
- **Tại sao đáng chú ý:** Bug này không thể phát hiện bằng SAST
  một mình — cần chạy thực tế mới thấy crash. Đây là lý do
  pipeline thesis mình cần cả SAST + LLM + fuzzing, không thể
  dùng riêng lẻ.
- **Status:** `fixed` — đã được patch, CVE đã assign
- **Nguồn:** https://bugs.chromium.org/p/oss-fuzz (search: pillow)

---

## 🔗 Áp dụng được gì?

| Cho thesis | Cho GRC90 / portfolio | Cho buổi research tiếp |
|---|---|---|
| Confirm Atheris là đúng stack | Commit file này lên audit-trail = proof-of-work hôm nay | Đọc thêm driver của project `cryptography` |
| Thấy giới hạn của crash-only fuzzing → LLM cần fill gap này | Có thể viết 1 đoạn ngắn về oss-fuzz trong README repo | Thử tự viết 1 fuzz driver đơn giản cho 1 lib nhỏ |
| Có ví dụ thực tế để cite trong thesis phần "related work" | | |

---

## ❓ Câu hỏi còn chưa rõ

- [ ] Atheris khác LibFuzzer chỗ nào? oss-fuzz dùng cả hai không?
- [ ] Làm sao oss-fuzz biết crash là security bug chứ không phải
      chỉ là normal exception?
- [ ] LLM-based fuzz driver generation đã có ai làm chưa —
      có paper nào mình có thể cite không?

---

## ⏭️ Bước tiếp theo

- [ ] Đọc fuzz driver của project `cryptography` hoặc `arrow`
      → xem pattern có khác Pillow không
- [ ] Tìm 1 Python lib nhỏ để tự chạy CodeQL → so output
      với những gì oss-fuzz đã tìm ra trên lib đó
- [ ] Search paper về LLM + fuzz driver generation để bổ sung
      vào phần related work của thesis

---
*Thời gian ngồi: ~40 phút | Mood: 🙂*
