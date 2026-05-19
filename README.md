# audit-trail

Security research journal — ongoing.

## Structure
- `audit-log/` — notes từng buổi research theo ngày
- `findings/` — findings đáng chú ý, có phân tích
- `poc/` — proof-of-concept drafts

## Guide
audit-log/     ← ghi lại từng buổi ngồi research
               "hôm nay mình đọc repo X, thấy issue Y, nghĩ là..."

findings/      ← khi bạn phân tích 1 issue đủ sâu để có nhận xét riêng
               "issue này thực sự là vuln vì..., impact là..., reproduce như sau..."

poc/           ← code demo khai thác hoặc fuzz driver bạn tự viết
               "đây là fuzz driver mình viết để test issue này"

## Format
Mỗi file: YYYY-MM-DD-repo-name.md
