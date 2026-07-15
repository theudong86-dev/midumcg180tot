# Bộ não thứ 2 — Starter Template

Template vault để dựng "**bộ não thứ 2**" cá nhân với **Obsidian + Claude Code AI** — wiki kiến thức do AI duy trì, kiến thức tích lũy không mất đi.

> **Phương pháp:** Persistent LLM-maintained wiki — khác RAG ở chỗ kiến thức được biên soạn 1 lần và bồi đắp dần, thay vì tìm lại từ đầu mỗi câu hỏi.

---

## Bắt đầu trong 10 phút

### Bước 1 — Cài 3 công cụ
- **[Obsidian](https://obsidian.md)** — editor markdown miễn phí
- **[Node.js ≥ v18](https://nodejs.org)** — runtime cho Claude Code
- **[Claude Code](https://docs.claude.com/claude-code)**:
  ```bash
  npm install -g @anthropic-ai/claude-code
  ```

### Bước 2 — Mở folder này trong Obsidian
- Đổi tên folder template thành tên bạn chọn (vd: `My Brain`).
- Mở Obsidian → **Open folder as vault** → chọn folder vừa đổi tên.

### Bước 3 — Sửa tên vault trong CLAUDE.md
- Mở `CLAUDE.md` → tìm dòng `Vault name: **<Vault Name>**` → thay `<Vault Name>` bằng tên bạn chọn.

### Bước 4 — Khởi động Claude Code
```bash
cd "<đường-dẫn-tới-vault>"
claude
```
Hỏi để verify: *"Bạn đã đọc CLAUDE.md chưa? Tóm tắt 3 lớp của vault này."*
→ Phải trả lời được "raw / wiki / schema" → setup đúng.

### Bước 5 — Đọc hướng dẫn đầy đủ
- 📘 [`reference/Cách tạo bộ não thứ 2.md`](reference/Cách%20tạo%20bộ%20não%20thứ%202.md) — quy trình thực hành A-Z, đa nền tảng macOS/Windows/Linux + 7 nguyên tắc + 3 workflow + checklist + FAQ.
- 📚 [`reference/methodology.md`](reference/methodology.md) — lý thuyết nền tảng (English).

### Bước 6 — Ingest source đầu tiên
- Drop 1 file (PDF, article, transcript) vào folder `raw/`.
- Trong Claude Code REPL gõ: `ingest raw/ten-file.pdf`.
- Claude sẽ chạy 8 bước workflow Ingest → tạo source page + entity + concept + cập nhật `index.md`/`log.md`.
- Mở Graph view (`Ctrl/Cmd+G`) trong Obsidian → thấy cụm node mới.

---

## Cấu trúc thư mục

```
/
├── CLAUDE.md              # schema — quy tắc & workflow cho AI (đổi vault name ở đây)
├── Home.md                # landing page (sửa theo bạn)
├── index.md               # catalog tất cả wiki pages
├── log.md                 # nhật ký ingest/query/lint (entry bootstrap mẫu)
├── README.md              # file này
├── .gitignore             # cho Git users — exclude file không nên commit
├── .claude/
│   └── settings.local.json.example   # rename → settings.local.json để bật allowlist
├── raw/                   # source gốc (BẤT BIẾN — chỉ đọc)
│   └── assets/            # ảnh từ Web Clipper
└── wiki/                  # AI sinh ra (sources, entities, concepts...)
    ├── sources/           # 1 summary cho mỗi source ingest
    ├── entities/          # người, công ty, sản phẩm
    ├── concepts/          # framework, ý tưởng, methodology
    ├── topics/            # tổng hợp chủ đề chéo
    └── analyses/          # query results đáng giữ lại
```

---

## Tùy biến cho domain của bạn

Sau khi quen, bạn có thể thêm category mới trong `wiki/`:

| Domain | Category gợi ý |
|---|---|
| **Học viên / sinh viên** | `wiki/courses/`, `wiki/professors/` |
| **Doanh nhân** | `wiki/products/`, `wiki/customers/`, `wiki/competitors/` |
| **Researcher** | `wiki/papers/`, `wiki/authors/`, `wiki/methods/` |
| **Content creator** | `wiki/ideas/`, `wiki/scripts/`, `wiki/audiences/` |
| **Luật sư / consultant** | `wiki/clients/`, `wiki/cases/`, `wiki/regulations/` |

Mỗi lần thêm category mới → cập nhật section "Directory structure" trong `CLAUDE.md`.

---

## 3 workflow vận hành

### Ingest (mỗi khi có source mới)
```
ingest raw/file.pdf
```
→ Claude đọc, discuss takeaways, viết source page + entity + concept + update index/log.

### Query (mỗi khi cần synthesize)
```
So sánh A và B trong vault
```
→ Claude đọc index, drill xuống pages, trả lời với citation. Câu trả lời hay → bảo *"file this back as analysis"*.

### Lint (mỗi 5-10 source mới hoặc hàng tháng)
```
lint the wiki
```
→ Claude trả checklist 7 issue types (contradictions, orphans, missing pages, index drift...). Bạn prioritize, ra lệnh fix từng cái.

---

## Bật allowlist permissions (optional, nhưng tiện)

Mặc định Claude Code hỏi xin phép mỗi lần edit file. Để tự động hóa trong vault này:

```bash
mv .claude/settings.local.json.example .claude/settings.local.json
```

Sau đó Claude sẽ tự động edit `wiki/`, `index.md`, `log.md`, `Home.md` không cần hỏi. CLAUDE.md vẫn hỏi (intentional — schema thay đổi cần bạn duyệt).

---

## Sync vault giữa nhiều máy (optional)

| Cách | Free? | Phù hợp |
|---|---|---|
| **iCloud Drive** | ✅ | Mac (+ Windows hạn chế) |
| **Obsidian Sync** ($4/tháng) | ❌ | Đa nền tảng E2E encrypted |
| **Google Drive / Dropbox** | ✅ | Đa nền tảng (cẩn thận sync conflict) |
| **Git (GitHub)** | ✅ | Có version history (recommended cho dev) |
| **Syncthing** | ✅ | P2P, không qua cloud |
| **Không sync** | ✅ | OK nếu chỉ 1 máy |

Nếu dùng Git: `.gitignore` đã chuẩn bị sẵn (loại trừ `.DS_Store`, `workspace.json`, `settings.local.json`).

---

## Credit

Template dựa trên phương pháp **persistent LLM-maintained wiki** của [Geoff Huntley](https://ghuntley.com).

**License:** MIT — free to use cho cả cá nhân và thương mại.

---

*"Bộ não thứ 2 không phải để bạn thông minh hơn — nó giải phóng não khỏi việc nhớ chi tiết, để não tập trung suy nghĩ chiến lược."*
