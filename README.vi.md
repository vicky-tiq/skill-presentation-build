# skill-presentation-build

Một Claude Code skill dựng **cấu trúc** bài trình bày trước khi dựng bất kỳ slide nào.

[English](README.md) · **Tiếng Việt**

---

## Vấn đề nó xử lý

Bảo trợ lý "làm cho tôi bộ slide về X" thì ba mươi giây sau có slide — loại slide thực chất
là một văn bản trá hình, người nói cuối cùng đứng đọc lại, còn khán giả đã đọc xong trước
khi người nói tới dòng thứ ba.

Lỗi không nằm ở thẩm mỹ. Nó nằm ở cấu trúc, và xảy ra trước khi có slide đầu tiên.

Cấu trúc tồn tại để làm hai việc cùng lúc: giúp **người nghe** theo kịp lập luận và nhớ được
thông điệp, và giúp **người nói** bình tĩnh, đúng trọng tâm, chuyển ý mà không phải mò tìm
mối nối.

Nên skill này cố định lại thứ tự làm việc:

```
brief  →  section map  →  kịch bản nói  →  slide
```

Không mở công cụ slide cho tới khi section map đã viết ra và được duyệt.

---

## Nó làm gì

### 1. Brief — ba câu hỏi, hỏi từng câu một

| | |
|---|---|
| **Mục tiêu** | Không phải chủ đề. Là mục tiêu: thông tin, thuyết phục, bán, dạy, lấy quyết định, xin ngân sách. |
| **Người nghe** | Họ là ai và **đã biết gì rồi** — cái này quyết định phải xây bao nhiêu bối cảnh, thuật ngữ nào được dùng miễn phí. |
| **Một thông điệp** | Sau buổi này họ phải nhớ điều gì? Một câu. Nếu phải ba câu thì bài chưa có thông điệp. |

Cộng năm ràng buộc làm đổi hình dạng cấu trúc: thời lượng, mức độ tương tác, bối cảnh
(sân khấu / phòng họp / Zoom / lớp học), có demo hay không, và có sẵn tư liệu trực quan gì.

Mọi thứ phía sau đều bị chấm điểm dựa trên câu thông điệp đó.

### 2. Cấu trúc

Mặc định là năm phần kinh điển — chào hỏi, mở bài, thân bài, kết luận, cảm ơn & hỏi đáp —
và đổi sang phương án khác khi tình huống đòi hỏi:

| Cấu trúc | Khi nên dùng | Trình tự |
|---|---|---|
| **Cơ bản** | Đa số bài nói, báo cáo, giảng dạy | Chào → mở bài → thân bài → kết luận → Q&A |
| **Trình diễn** | Giới thiệu sản phẩm hoặc hệ thống | Giá trị → nhu cầu → vấn đề → demo → khả năng mở rộng |
| **Vấn đề – giải pháp** | Thuyết phục người nghe thay đổi | Vấn đề → tác động → giải pháp → hành động |
| **Kể chuyện** | Tạo cảm xúc, giữ chú ý | Bối cảnh → thử thách → hành trình → kết quả → bài học |
| **Loại trừ phương án** | Chủ đề nhiều quan điểm đối nghịch | Vấn đề → các lựa chọn → giới hạn từng cái → đề xuất |

Mỗi phần thân bài bắt buộc có **đủ bốn thứ**: một ý chính, bằng chứng, ý nghĩa với *chính
nhóm người nghe này*, và một câu tóm tắt nói ra miệng trước khi chuyển. Thiếu một là phần
đó chưa xong.

### 3. Section map — đây mới là sản phẩm chính

Một bảng bạn sửa trong một lượt, trước khi dựng bất cứ thứ gì:

| # | Phần | Ý chính | Bằng chứng | Ý nghĩa với họ | Câu chuyển ý | Phút |
|---|---|---|---|---|---|---|

Hai quy tắc gánh phần lớn kết quả:

- **Chia thời lượng trước, nhét nội dung vào sau.** Mở bài ≈ 10%, kết luận + Q&A ≈ 20%,
  phần còn lại cho thân bài. Bài 20 phút chỉ đỡ được **ba** phần thân bài. Không phải sáu.
- **Mỗi câu chuyển ý được viết ra thành câu.** Tóm tắt phần vừa xong → vì sao nó quan trọng
  → phần tiếp theo là gì → mối liên hệ giữa hai phần. Chuyển ý là chỗ người nói vừa mất
  khán giả vừa mất mạch của chính mình, nên không để ứng biến. Phần bàn giao trong thuyết
  trình nhóm cũng viết y như vậy.

Phần nào có thể cắt nếu trễ giờ thì đánh dấu **ngay bây giờ**, lúc còn bình tĩnh, không phải
lúc đang đứng trên sân khấu.

### 4. Kịch bản nói

Không phải bullet. Mỗi phần có: câu mở, ý chính nói thẳng, bằng chứng kèm số, ý nghĩa, câu
tóm tắt, câu chuyển ý viết sẵn, và mốc phút mục tiêu. **60 giây đầu và 60 giây cuối viết
nguyên văn** — đó là hai đoạn quyết định bài nói được tiếp nhận thế nào và còn lại gì.

Kèm bảng chuẩn bị Q&A: năm câu hỏi dễ gặp nhất, trong đó bắt buộc có câu khó chịu nhất.

### 5. Slide

Đến lúc này mới làm. Một slide một ý. Một hình hoặc sơ đồ thay cho một đoạn văn. Cỡ chữ tối
thiểu 30pt. Có slide chương trình và slide tổng kết, vì đó là tấm bản đồ của người nghe.
Quy tắc 10–20–30 của Kawasaki dùng để hiệu chỉnh, không phải luật — workshop ba tiếng đương
nhiên phá vỡ nó, nhưng cỡ chữ thì không bao giờ nhân nhượng.

Dựng vào đúng kênh mà bộ slide sẽ sống:

| Kênh | Chọn khi | Ra sản phẩm gì |
|---|---|---|
| **Slides MCP có sẵn** | Muốn có deck đẹp ngay, không cần định dạng file cụ thể | Deck online + speaker notes |
| **Gamma** | Nhanh nhất để có deck đẹp; còn sửa tiếp online | Link Gamma |
| **.pptx** | Phải mở bằng PowerPoint/Keynote, gửi mail, giao ban tổ chức | Một file |
| **Google Slides** | Team dùng Workspace, nhiều người cùng sửa hoặc comment | Link Drive |
| **Figma Slides** | Deck là sản phẩm thiết kế; designer sẽ tiếp quản | File Figma |
| **Canva / Adobe Express** | Marketing sẽ làm tiếp trong công cụ của họ | Bản thiết kế sửa được |
| **HTML Artifact** | Cần kiểm soát layout, hoặc cần link chia sẻ cố định | Một trang web |

Phần của mỗi kênh ghi rõ những cái bẫy có thật: Google Slides **không có API nội dung** nên
deck phải dựng bằng .pptx rồi để Drive tự chuyển đổi khi upload; Figma Slides đòi **ghế
Full** trên đúng plan và đúng tài khoản; slides MCP sẽ **thêm slide trùng** nếu sửa mà quên
`force_edit`. Còn việc chia sẻ deck cho người khác — cấp quyền Drive, mời vào Figma, publish
link — luôn là một bước riêng do bạn duyệt.

### 6. Checklist trước khi giao

Mười hai mục, trong đó quan trọng nhất: **chỉ đọc phần kết luận thôi có lấy lại được câu
thông điệp không?**

---

## Cài đặt

Hai lệnh trong Claude Code:

```
/plugin marketplace add vicky-tiq/skill-presentation-build
/plugin install presentation-build@skill-presentation-build
```

Hoặc chạy trong terminal:

```bash
claude plugin marketplace add vicky-tiq/skill-presentation-build
claude plugin install presentation-build@skill-presentation-build
```

Khởi động lại session để skill được nạp. `claude plugin list` để kiểm tra, còn
`claude plugin details presentation-build@skill-presentation-build` cho biết nó tốn bao
nhiêu: **một skill, ~310 token thường trực, ~2.5k khi thực sự chạy.**

Cập nhật sau này: `claude plugin update presentation-build@skill-presentation-build`.
Gỡ: `claude plugin uninstall presentation-build@skill-presentation-build`.

**Không dùng plugin** — copy thẳng thư mục skill:

```bash
git clone https://github.com/vicky-tiq/skill-presentation-build.git
cp -r skill-presentation-build/skills/presentation-build ~/.claude/skills/
```

Để ở `~/.claude/skills/` là chỉ mình bạn dùng trên máy này; để ở `.claude/skills/` trong
repo dự án thì ai clone repo đó cũng có.

---

## Chưa có Claude Code? Upload lên claude.ai

Skill dùng được trong app Claude. Áp dụng cho gói **Free, Pro, Max, Team và Enterprise**, với
điều kiện đã bật **code execution** trong Settings:

1. Tải **`presentation-build.zip`** ở
   [bản phát hành mới nhất](https://github.com/vicky-tiq/skill-presentation-build/releases/latest).
2. Trên claude.ai vào **Customize → Skills**, bấm **Add**, chọn file zip.

File zip đã đóng đúng chuẩn — thư mục `presentation-build/` là gốc của archive, `SKILL.md`
nằm bên trong.

Hai điều cần biết trước khi triển khai cho cả team:

- **Skill không đồng bộ giữa các nền tảng.** Upload lên claude.ai thì Claude Code và API
  không thấy, và ngược lại. Mỗi nơi phải nạp riêng.
- **Trên claude.ai skill là của từng người.** Không có cách phát cho cả tổ chức, admin cũng
  không quản lý tập trung được — mỗi người tự upload bản zip của mình.

**Không có cả hai?** SKILL.md là markdown thuần. Dán nó vào đầu cuộc trò chuyện với bất kỳ
trợ lý nào là dùng được như một bộ hướng dẫn — mất phần tự kích hoạt và các file
`references/` phải đưa thêm khi cần, nhưng phương pháp thì vẫn nguyên.

---

## Dùng

Skill tự kích hoạt với mọi yêu cầu có hình dạng "bài trình bày". Hoặc gọi thẳng:

```
/presentation-build
```

Từ khoá kích hoạt gồm *làm slide, bài thuyết trình, chuẩn bị bài nói, dàn ý bài trình bày,
kịch bản thuyết trình, bài giảng, buổi chia sẻ*, và tiếng Anh *presentation, slides, deck,
pitch deck, workshop, webinar, keynote, speaker notes*.

---

## Trong hộp có gì

```
skills/presentation-build/
├── SKILL.md                          quy trình sáu bước
└── references/
    ├── structures.md                 năm cấu trúc đầy đủ, các cách sắp xếp nội dung,
    │                                 mẫu câu chuyển ý, bàn giao nhóm,
    │                                 một ví dụ workshop làm trọn vẹn
    ├── script-template.md            mẫu kịch bản nói, timing, chuẩn bị Q&A
    └── slide-channels.md             cách dựng deck trong từng kênh
```

---

## Nguồn

Các nguyên tắc cấu trúc lấy từ bài
[How to Structure your Presentation](https://virtualspeech.com/blog/how-to-structure-your-presentation)
của VirtualSpeech, được chuyển thành một quy trình bắt buộc thi hành: thứ tự làm việc cố
định, ngân sách thời gian khống chế số phần, câu chuyển ý viết ra thay vì ứng biến, và một
checklist phải qua trước khi giao.

Giấy phép MIT.
