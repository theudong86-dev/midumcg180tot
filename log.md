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

## [2026-07-15] deploy & expand | Vercel Deployments & Second Brain Updates
- **Deploy Midu MenaQ7:** Đăng nhập Vercel CLI, liên kết dự án và deploy thành công trang landing page lên **[midumcg180tot.vercel.app](https://midumcg180tot.vercel.app)**. Di chuyển các tệp `index.html` và `anh mcg180.jpg` ra thư mục gốc để hiển thị trực tiếp. Cập nhật lại giá ưu đãi các gói Combo và đồng bộ lên GitHub + Vercel Production.
- **Tạo trang mới "Tâm số học Trò chuyện cùng con":**
  - Sao chép & Tự động tùy biến mã nguồn từ trang reference `https://tamsohocmecon.vercel.app/` sang dự án mới độc lập tại `c:\Users\Admin\Downloads\tamsohoctrochuyencungcon`.
  - Thiết lập Git/GitHub, tạo repo `theudong86-dev/tamsohoctrochuyencungcon` nhánh `main` và đẩy code lên.
  - Liên kết Vercel, cấu hình Google Sheets Script Web App URL mới của chị (`AKfycbw4eDgTk...`) và deploy chạy chính thức tại **[tamsohoctrochuyencungcon.vercel.app](https://tamsohoctrochuyencungcon.vercel.app)**.
- **Cập nhật Bộ não thứ 2 (Obsidian):**
  - Đọc và đồng bộ dữ liệu tiểu sử đầy đủ từ tệp mới `raw/Gioi thieu ban than.txt` và ảnh chân dung `raw/anh chan dung.jpg`.
  - Cập nhật thông tin chi tiết vào [[wiki/entities/Đồng Thêu|Đồng Thêu]] (bổ sung: kỷ niệm nuốt hạt vải tuổi thơ, 7 năm học liên thông khó khăn, 3 người con nhỏ, câu chuyện sơ cứu trẻ sốt co giật, lời khuyên tuổi 20 và đính kèm link hiển thị ảnh chân dung của chị).
  - Cập nhật thông tin nguồn đọc [[wiki/sources/Gioi thieu ban than|Gioi thieu ban than]].

## [2026-07-15] ingest | HEIGHT_EXPERT_KNOWLEDGE_BASE
- Source: `raw/HEIGHT_EXPERT_KNOWLEDGE_BASE.md` (Khung kiến thức cơ sở tư vấn phát triển chiều cao v1.0)
- Created source page: [[wiki/sources/HEIGHT_EXPERT_KNOWLEDGE_BASE|HEIGHT_EXPERT_KNOWLEDGE_BASE]]
- Updated concept page: [[wiki/concepts/Chuyên gia chiều cao|Chuyên gia chiều cao]] (tích hợp triết lý tăng trưởng, sinh lý học, 4 trụ cột lối sống, quy trình tư vấn 6 bước và Prompt AI).
- Updated: [[index.md]]
- Notes: Thiết lập cơ sở tri thức chuẩn để cấu hình AI đóng vai Dược sĩ Đồng Thêu tư vấn chiều cao.
