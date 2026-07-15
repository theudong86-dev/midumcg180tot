# Log

Append-only chronological record. Newest at the bottom.
Format: `## [YYYY-MM-DD] <op> | <title>`. See [[CLAUDE]] for log format.

Quick check: `grep "^## \[" log.md | tail -10`

---

## [2026-07-12] bootstrap | wiki initialized
- Created: vault structure (`raw/`, `raw/assets/`, `wiki/{sources,entities,concepts,topics,analyses}/`, `reference/`, `.claude/`)
- Created: `CLAUDE.md` (schema), `Home.md` (landing), `index.md` (catalog), `log.md` (this file), `README.md`
- Filed methodology spec at `reference/methodology.md` (English, gốc Geoff Huntley)
- Filed setup guide at `reference/Cách tạo bộ não thứ 2.md` (Vietnamese, đa nền tảng)
- Notes: vault initialized from starter template — sẵn sàng ingest source đầu tiên.

<!--
HƯỚNG DẪN:

1. Sửa "YYYY-MM-DD" ở entry trên thành ngày bạn bắt đầu (vd: ## [2026-05-23]).

2. Sau khi ingest source đầu tiên, Claude sẽ tự append entry mới ở đây theo format:

   ## [2026-04-28] ingest | Tên source
   - Source: `raw/ten-file.pdf` (mô tả ngắn)
   - Created source page: [[Tên source]]
   - Created N entity pages: [[Entity 1]], [[Entity 2]]
   - Created M concept pages: [[Concept 1]], [[Concept 2]]
   - Updated index.md
   - Open questions: ...
   - Notes: ...

3. Mỗi loại operation có prefix riêng — dễ greppable:
   - bootstrap | (lần đầu init)
   - ingest | (ingest source mới)
   - re-ingest | (đọc lại source đã có)
   - expand | (mở rộng wiki page có sẵn)
   - correction | (sửa lỗi đã commit)
   - query | (query có lưu lại analysis)
   - lint | (chạy health-check)

4. Newest entry ở dưới cùng. KHÔNG insert vào giữa.
-->

## [2026-07-12] ingest | Gioi thieu ban than
- Source: `raw/Gioi thieu ban than.txt` (Bài tự giới thiệu của Dược sĩ Đồng Thêu)
- Created source page: [[wiki/sources/Gioi thieu ban than|Gioi thieu ban than]]
- Created entity page: [[wiki/entities/Đồng Thêu|Đồng Thêu]]
- Created concept pages: [[wiki/concepts/Chuyên gia chiều cao|Chuyên gia chiều cao]], [[wiki/concepts/Tư vấn dinh dưỡng|Tư vấn dinh dưỡng]], [[wiki/concepts/Kinh doanh online sức khỏe|Kinh doanh online sức khỏe]]
- Updated: [[index.md]]
- Notes: Người dùng nhấn mạnh định hướng phát triển Chuyên gia chiều cao và Tư vấn dinh dưỡng chuẩn khoa học.

## [2026-07-15] expand | Landing Page Midu MenaQ7 180mcg
- Đã sao chép: `raw/anh mcg180.jpg` sang `landing/anh mcg180.jpg`
- Đã tạo: Trang Landing Page hoàn chỉnh tại [[landing/index.html]] dựa trên dữ liệu sản phẩm [[raw/mcg180.txt.txt]]
- Ghi chú: Thiết kế giao diện Light Mode lâm sàng, tối ưu chuyển đổi, tích hợp form tương tác và đồng hồ đếm ngược cho tên miền midumcg180tot.vercel.app.
