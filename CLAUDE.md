# CLAUDE.md — Sơ đồ Wiki (Schema)

> **Hướng dẫn cho người mới:** Đổi `<Tên Vault>` ở phần dưới thành tên vault của bạn (vd: `My Brain`, `Sales Vault`). Phần còn lại của file này là schema chuẩn — chỉ nên sửa khi bạn đã nạp (ingest) 5-10 nguồn và tự rút ra được quy ước riêng.

Tên vault: **Bộ não của X**

Vault này là một **wiki bền vững, do LLM duy trì**. Kiến thức được biên soạn MỘT LẦN khi nguồn tài liệu được đưa vào, rồi được giữ cho luôn cập nhật — chứ không phải suy diễn lại từ đầu mỗi lần có câu hỏi.

Đọc file này ở đầu mỗi phiên làm việc, TRƯỚC khi đọc hoặc ghi bất kỳ file nào khác.

## Ba tầng (Three layers)

1. **Nguồn thô** (`raw/`) — tài liệu đầu vào, bất biến (bài viết clip về, PDF, ghi chú, bản ghi âm/transcript, hình ảnh). Chỉ đọc từ đây, KHÔNG bao giờ sửa.
2. **Wiki** (`wiki/`) — các trang markdown do LLM tạo ra: bản tóm tắt nguồn, trang thực thể (entity), trang khái niệm (concept), bản tổng hợp, so sánh, phân tích. LLM sở hữu hoàn toàn tầng này.
3. **Schema** (chính file này) — quy ước và quy trình làm việc. Tiến hóa dần cùng người dùng theo thời gian.

Cộng thêm hai file điều hướng ở thư mục gốc:
- `index.md` — mục lục nội dung (có những trang nào, sắp xếp theo danh mục)
- `log.md` — nhật ký ghi thêm theo thời gian, chỉ nối vào cuối (các lần nạp nguồn, truy vấn, rà soát lint)

## Cấu trúc thư mục

```
/
├── CLAUDE.md              # chính file này
├── index.md               # mục lục nội dung
├── log.md                 # nhật ký theo thời gian
├── raw/
│   ├── assets/            # hình ảnh, PDF đã tải về
│   └── ...                # tài liệu nguồn
├── wiki/
│   ├── sources/           # mỗi nguồn đã nạp = một trang tóm tắt
│   ├── entities/          # người, công ty, tổ chức, sản phẩm, dự án
│   ├── concepts/          # khung tư duy, ý tưởng, phương pháp, nguyên tắc
│   ├── topics/            # bản tổng hợp chủ đề liên ngành
│   └── analyses/          # kết quả truy vấn được lưu lại thành trang
└── reference/             # tài liệu về chính hệ thống này, không phải nội dung kiến thức
```

Các thư mục con trong `wiki/` chỉ là gợi ý, không cứng nhắc. Cứ thêm danh mục mới khi lĩnh vực của bạn cần (vd: `events/`, `decisions/`, `books/`). Khi thêm, nhớ cập nhật lại mục này.

## Quy ước về file

- **Tên file**: dùng tiêu đề dễ đọc, có dấu cách cũng được (Obsidian xử lý tốt). Dùng tên chuẩn (canonical) của thực thể, khái niệm hoặc nguồn.
- **Wikilink**: liên kết thật nhiều bằng `[[Tên Trang]]`. Mỗi thực thể, khái niệm và nguồn được nhắc trong văn bản đều nên là một liên kết.
- **Frontmatter**: mỗi trang wiki mở đầu bằng khối YAML frontmatter:
  ```yaml
  ---
  type: source | entity | concept | topic | analysis
  tags: [tag1, tag2]
  created: 2026-04-26
  updated: 2026-04-26
  sources: ["[[Nguồn A]]", "[[Nguồn B]]"]   # các trang nguồn wiki mà trang này dựa vào
  ---
  ```
- **Trang nguồn** còn có thêm: `raw_path: raw/...`, `author` (tác giả), `date` (ngày), `url` (khi có).
- **Trích dẫn**: trong văn bản wiki, dẫn nguồn bằng `[[Tiêu đề Nguồn]]` ngay trong dòng. Tránh đưa ra khẳng định mà không kèm liên kết nguồn.
- **Ngôn ngữ**: viết mỗi trang theo ngôn ngữ của nguồn. Nếu nguồn pha trộn nhiều ngôn ngữ, ngôn ngữ chiếm ưu thế thắng; giữ nguyên văn các câu trích dẫn gốc.

## Quy trình: Nạp nguồn (Ingest)

Khi người dùng nói "nạp/ingest X" hoặc thả một file vào `raw/`:

1. **Đọc** trọn vẹn nguồn. Với hình ảnh thì xem trực tiếp; với file dài thì đọc theo từng phần.
2. **Bàn về các ý chính** với người dùng (3-5 gạch đầu dòng). Hỏi xem cần nhấn mạnh điều gì trước khi viết.
3. **Viết bản tóm tắt nguồn** tại `wiki/sources/<Tiêu đề Nguồn>.md` — gồm frontmatter, một đoạn TL;DR, các luận điểm chính kèm tham chiếu mục/trang, và danh sách các thực thể + khái niệm được nhắc tới.
4. **Cập nhật hoặc tạo trang thực thể** cho mỗi thực thể có tên. Thực thể mới → tạo `wiki/entities/<Tên>.md`. Thực thể đã có → viết thêm vào mục liên quan, và liên kết trở lại nguồn mới. Thêm thư mục con khi lĩnh vực cần (vd `wiki/clients/`, `wiki/projects/`, `wiki/authors/`).
5. **Cập nhật hoặc tạo trang khái niệm** trong `wiki/concepts/` (khung tư duy, phương pháp, ý tưởng lặp lại). Thêm danh mục wiki khác khi cần (vd `wiki/courses/`, `wiki/stories/`, `wiki/papers/`) và ghi lại chúng trong file này.
6. **Ghi rõ mâu thuẫn**. Nếu nguồn mới bất đồng với một khẳng định đã có, thêm mục "Mâu thuẫn" (Contradictions) trên trang liên quan, nêu cả hai quan điểm kèm liên kết nguồn — KHÔNG âm thầm ghi đè.
7. **Cập nhật `index.md`** — thêm trang nguồn mới và mọi trang thực thể/khái niệm mới.
8. **Ghi thêm vào `log.md`** — xem định dạng Log ở dưới.

Một nguồn thường chạm tới 5-15 trang wiki. Sau khi nạp xong, tóm tắt lại cho người dùng những gì đã thay đổi.

## Quy trình: Truy vấn (Query)

Khi người dùng đặt câu hỏi dựa trên wiki:

1. **Đọc `index.md`** trước để tìm các trang ứng viên.
2. **Đào sâu vào các trang liên quan**. Đi theo các wikilink để gom đủ ngữ cảnh.
3. **Tổng hợp câu trả lời kèm trích dẫn** — mỗi khẳng định liên kết tới một trang wiki (hoặc, với trích dẫn nguyên văn, tới nguồn thô).
4. **Chọn định dạng đầu ra phù hợp** với câu hỏi: văn xuôi, bảng so sánh, danh sách gạch đầu dòng, slide Marp (`.md` với frontmatter `marp: true`), biểu đồ matplotlib, canvas, v.v.
5. **Đề nghị lưu câu trả lời lại** thành trang mới trong `wiki/analyses/` nếu đó là bản tổng hợp đáng giữ. Người dùng quyết định.

Nếu wiki chưa đủ dữ liệu để trả lời, hãy nói thẳng — ĐỪNG bịa. Gợi ý nguồn nên nạp thêm hoặc các tìm kiếm web nên chạy.

## Quy trình: Rà soát (Lint)

Khi người dùng nói "lint wiki" hoặc định kỳ:

Đây là đợt kiểm tra sức khỏe của wiki. Tìm và báo cáo:
- **Mâu thuẫn** giữa các trang nói về cùng một thực thể hoặc khái niệm.
- **Khẳng định lỗi thời** — trang đã bị nguồn mới hơn thay thế nhưng chưa được cập nhật.
- **Trang mồ côi** — không có wikilink nào trỏ vào (dùng graph của Obsidian hoặc `grep`).
- **Trang còn thiếu** — khái niệm được nhắc trong 3+ nguồn nhưng chưa có trang riêng.
- **Thiếu liên kết chéo** — thực thể A và thực thể B liên tục xuất hiện cùng nhau nhưng không trang nào liên kết tới trang kia.
- **Lệch mục lục** — trang tồn tại trên ổ đĩa nhưng không có trong `index.md`, hoặc ngược lại.
- **Câu hỏi mở** — những lỗ hổng wiki đã nhận ra nhưng chưa trả lời. Gợi ý nguồn hoặc tìm kiếm.

Báo cáo kết quả dưới dạng danh sách kiểm (checklist). ĐỪNG tự ý sửa; để người dùng quyết định ưu tiên.

## Định dạng `index.md`

Sắp xếp theo danh mục. Mỗi mục là một dòng:

```markdown
- [[Tiêu đề Nguồn]] — tóm tắt một dòng (ngày, tác giả)
- [[Tên Thực Thể]] — mô tả một dòng
```

Các phần: Nguồn (Sources), Thực thể (Entities), Khái niệm (Concepts), Chủ đề (Topics), Phân tích (Analyses). Thêm danh mục khi wiki lớn dần.

## Định dạng `log.md`

Chỉ nối thêm vào cuối. Mỗi mục bắt đầu bằng một tiền tố nhất quán để dễ `grep`:

```markdown
## [2026-04-26] ingest | Tiêu đề Bài viết
- Đã tạo: [[Tiêu đề Nguồn]]
- Đã cập nhật: [[Thực thể A]], [[Khái niệm B]]
- Ghi chú: mâu thuẫn với khẳng định cũ trong [[Thực thể A]]; người dùng nhấn mạnh X.

## [2026-04-26] query | "X liên quan tới Y thế nào?"
- Đã đọc: [[Trang1]], [[Trang2]], [[Trang3]]
- Đầu ra: bảng so sánh, lưu tại [[wiki/analyses/X vs Y]]

## [2026-04-26] lint
- 3 trang mồ côi: ...
- 1 mâu thuẫn: ...
```

Mục mới nhất nằm ở cuối. Kiểm tra nhanh: `grep "^## \[" log.md | tail -10`.

## Mẹo (Tips)

- **Obsidian Web Clipper** đưa bài viết vào `raw/` dưới dạng markdown.
- **Tải hình ảnh**: trong Obsidian, đặt thư mục đính kèm là `raw/assets/`. Sau khi clip, chạy "Download attachments for current file" để tải hình về máy — xem hình khi ngữ cảnh cần.
- **Chế độ Graph** cho thấy hình dạng của wiki — đâu là các trung tâm (hub), đâu là trang mồ côi.
- **Marp** để làm slide (`marp: true` trong frontmatter).
- **Dataview** truy vấn frontmatter của trang — giữ YAML sạch và nhất quán.

## Cùng tiến hóa file này

Khi Claude phát hiện một cải tiến quy trình, một quy ước đặt tên bị đuối, hoặc một sở thích lặp lại của người dùng, hãy đề xuất chỉnh sửa file này và hỏi người dùng xác nhận. Schema này được thiết kế để trôi dần về phía những gì thực sự hiệu quả cho vault — chứ không đứng yên một chỗ.

---

*Mẫu vault này được chuyển giao & thiết lập bởi **Nguyễn Xuân Hợp — Midu Group**. Khái niệm "bộ não thứ hai" thuộc về cộng đồng; bản Việt hóa & quy trình đóng gói do Midu Group biên soạn.*
