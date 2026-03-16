# Đề xuất nâng cấp AG-SKILL v3.0
> Tập trung: Vibe Code · Brainstorm · Code chuẩn · Tự test · Tự sửa lỗi · Quản lý Context

---

## 1. Bức tranh tổng thể — AG-SKILL v2.0 đang thiếu gì?

AG-SKILL v2.0 của bạn đã có nền tảng tốt (TDD, search-first, 5-layer memory, instinct system).  
Tuy nhiên, so với các repo hàng đầu năm 2026, còn **4 lỗ hổng cốt lõi** trực tiếp ảnh hưởng đến ưu tiên của bạn:

| Lỗ hổng | Biểu hiện thực tế | Mức độ |
|---|---|---|
| **Verification Loop** chưa khép kín | Build xong không tự kiểm tra, lỗi phát hiện muộn | 🔴 Cao |
| **Brainstorm → Spec → Code** còn rời rạc | `/plan` và `/build` chưa có gate bắt buộc viết spec trước | 🔴 Cao |
| **Context compaction** thụ động | Không có ngưỡng tự động nhắc compact, dễ mất chất lượng cuối session | 🟡 Trung |
| **Auto-fix loop** khi test thất bại | Sau khi test fail, agent chưa tự vào vòng lặp sửa-test lại | 🔴 Cao |

---

## 2. Các skill/pattern cần bổ sung theo từng mục tiêu

### 🎯 Ưu tiên 1 — Code chuẩn, tự test, tự sửa lỗi

#### Cần thêm: **`verification-loop`** skill
Đây là skill quan trọng nhất thiếu trong AG-SKILL v2.0.

```
Vòng lặp: Build → Test → Lint → Typecheck → Security → Nếu fail → Auto-fix → Lặp lại
```

**Nguồn học:**
- `affaan-m/everything-claude-code` → `skills/verification-loop/SKILL.md`
  - Đây là vòng lặp 5 bước: build, test, lint, typecheck, security. Nếu bất kỳ bước nào fail, agent tự phân tích root cause và fix trước khi tiếp tục.
- `affaan-m/everything-claude-code` → `skills/eval-harness/SKILL.md`
  - Checkpoint vs continuous eval. Dùng pass@k metrics để đánh giá chất lượng output.
- `affaan-m/everything-claude-code` → `commands/verify.md` (`/verify`)
  - Command trigger toàn bộ verification loop từ một lệnh duy nhất.

#### Cần thêm: **`plankton-code-quality`** skill (PostToolUse hook)
Kiểm tra code *ngay khi viết xong từng file*, không đợi đến cuối.

```
Mỗi lần edit file → Auto-format → Chạy linters → Nếu vi phạm → Spawn subprocess sửa
```

**Nguồn học:**
- `affaan-m/everything-claude-code` → `skills/plankton-code-quality/SKILL.md`
  - 3-phase: auto-format (40-50% lỗi), collect violations as JSON, delegate fixes to subprocess.
  - Có config protection: ngăn agent sửa linter config để "pass" thay vì sửa code thật.

#### Cần thêm: **`autonomous-loops`** skill
Pattern cho agent tự chạy pipeline tuần tự mà không cần người giám sát.

**Nguồn học:**
- `affaan-m/everything-claude-code` → `skills/autonomous-loops/SKILL.md`
  - Các pattern: sequential pipeline, PR loop, DAG orchestration.

---

### 🎯 Ưu tiên 2 — Vibe Code & Brainstorm ra idea chất lượng

#### Nâng cấp `/plan` thành **Plan với Brainstorm Gate**

Hiện tại `/plan` trong AG-SKILL thiếu bước bắt buộc phải *diverge* ý tưởng trước khi *converge* vào spec.

**Pattern cần học:**
```
/plan [idea] →
  1. Brainstorm Gate: Liệt kê 3-5 hướng tiếp cận khác nhau
  2. Tradeoff Matrix: So sánh theo: complexity / maintainability / time-to-ship
  3. ADR tự động cho hướng được chọn
  4. Spec 15-section (bạn đã có trong /spec)
  5. Gate: Không được /build nếu chưa có spec
```

**Nguồn học:**
- `affaan-m/everything-claude-code` → `agents/planner.md` + `agents/architect.md`
  - Planner tạo implementation blueprint. Architect đưa ra system design decisions. Hai agent phối hợp trước khi code.
- `shanraisshan/claude-code-best-practice` → Pattern: "spin up a second Claude to review your plan as a staff engineer"
  - Dùng cross-model review: một instance lên kế hoạch, một instance phản biện.
- `FlorianBruniaux/claude-code-ultimate-guide` → Skill: **Claudeception**
  - Meta-skill: Agent tự sinh ra skills mới từ discoveries trong session. Rất phù hợp để kết hợp với `/evolve` của bạn.

#### Cần thêm: **`search-first`** skill (bạn đang có `/search` nhưng chưa đủ)

```
Trước khi code bất kỳ thứ gì → Research context → Check existing solutions → Tìm patterns
```

**Nguồn học:**
- `affaan-m/everything-claude-code` → `skills/search-first/SKILL.md`
  - Research-before-coding workflow. Bắt buộc agent tìm kiếm trước, không code ngay từ memory.
- `affaan-m/everything-claude-code` → `skills/iterative-retrieval/SKILL.md`
  - Progressive context refinement cho subagents: lấy context theo nhiều vòng, mỗi vòng tinh chỉnh hơn.

---

### 🎯 Ưu tiên 3 — Quản lý Context thông minh

#### Nâng cấp `/session` với **Context % Monitoring**

AG-SKILL v2.0 có `/checkpoint` nhưng chưa có ngưỡng tự động.

**Strategy cần implement:**

| Ngưỡng context | Hành động |
|---|---|
| 0–50% | Làm bình thường |
| 50–70% | Cảnh báo, gợi ý `/checkpoint` |
| 70–90% | Bắt buộc `/compact` trước khi tiếp tục |
| 90%+ | Bắt buộc `/save` và bắt đầu session mới |

**Nguồn học:**
- `affaan-m/everything-claude-code` → `skills/strategic-compact/SKILL.md`
  - Manual compaction suggestions tại logical breakpoints. Nguyên tắc: compact *sau* research, *trước* implementation. Không compact giữa chừng khi đang code.
- `affaan-m/everything-claude-code` → `hooks/strategic-compact/`
  - Hook PostToolUse tự động gợi ý compact khi context vượt ngưỡng.
- `FlorianBruniaux/claude-code-ultimate-guide` → Context strategy: 0-50 / 50-70 / 70-90 / 90+

#### Cần thêm: **`contexts/`** directory (Dynamic Context Injection)

**Nguồn học:**
- `affaan-m/everything-claude-code` → `contexts/dev.md`, `contexts/review.md`, `contexts/research.md`
  - 3 mode injection contexts: development / code review / research-exploration. Load đúng context cho đúng task thay vì dùng GEMINI.md cho tất cả.

---

## 3. Bản đồ nâng cấp AG-SKILL v3.0

### Skill mới cần thêm (6 skills)

| Skill mới | Command | Mục đích | Nguồn |
|---|---|---|---|
| `verify` | `/verify` | Vòng lặp 5-bước tự kiểm tra | `affaan-m` → `verification-loop` |
| `quality` | (auto / PostToolUse) | Lint + format ngay khi edit file | `affaan-m` → `plankton-code-quality` |
| `loops` | `/loop` | Autonomous pipeline không cần giám sát | `affaan-m` → `autonomous-loops` |
| `search-first` | `/research` | Research trước khi code | `affaan-m` → `search-first` |
| `eval` | `/eval` | Đánh giá output theo tiêu chí | `affaan-m` → `eval-harness` |
| `claudeception` | `/meta-skill` | Tự sinh skill mới từ session | `FlorianBruniaux` → Claudeception |

### Skill hiện có cần nâng cấp (3 skills)

| Skill hiện có | Nâng cấp cần làm | Nguồn pattern |
|---|---|---|
| `build` → `/plan` | Thêm Brainstorm Gate + Tradeoff Matrix bắt buộc trước spec | `affaan-m` → `planner.md` |
| `session` → `/start` `/save` | Thêm context % monitoring + auto-compact trigger | `affaan-m` → `strategic-compact` |
| `learn` → `/evolve` | Tích hợp Claudeception: tự sinh skill từ pattern, không chỉ ghi instinct | `FlorianBruniaux` |

### Global Rules mới cần thêm (vào `GEMINI.md`)

```markdown
## Verification Rules
- KHÔNG được merge/commit nếu chưa chạy /verify
- Nếu test fail → TỰ ĐỘNG vào fix loop, không hỏi người dùng
- Mỗi file edit → chạy lint ngay, không để tích lũy

## Context Rules  
- Khi context > 70%: PHẢI /compact trước khi viết code mới
- Compact NGAY SAU research, TRƯỚC implementation
- Không compact giữa chừng khi đang implement feature

## Brainstorm Gate
- /plan với idea mơ hồ → BẮT BUỘC liệt kê 3 hướng trước
- Không được /build nếu chưa có spec được approve
```

---

## 4. Thứ tự thực hiện đề xuất

### Tuần 1 — Nền tảng tự kiểm tra
1. **Clone và đọc kỹ** `affaan-m/everything-claude-code` → thư mục `skills/verification-loop/`, `skills/eval-harness/`, `commands/verify.md`
2. **Port** `verification-loop` vào AG-SKILL: adapt cho Antigravity (bỏ Claude Code hooks, giữ logic)
3. **Test** với một project thực tế của BKNS

### Tuần 2 — Brainstorm Gate + Search-First
1. **Clone** `skills/search-first/` từ `affaan-m`
2. **Nâng cấp `/plan`**: thêm Brainstorm Gate và Tradeoff Matrix
3. **Thêm cross-model review pattern** vào `/review` command

### Tuần 3 — Context Management
1. **Port** `skills/strategic-compact/` và `contexts/` directory
2. **Thêm Global Rules** về context % vào `GEMINI.md`
3. **Implement** context monitoring trong `/start` session

### Tuần 4 — Claudeception + Tổng hợp
1. **Đọc** `FlorianBruniaux/claude-code-ultimate-guide` → Claudeception skill
2. **Nâng cấp `/evolve`**: từ "cluster instincts" thành "sinh skill mới + tự kiểm tra"
3. **Tag release** AG-SKILL v3.0

---

## 5. Nguồn tài liệu tham khảo

### Repo ưu tiên đọc theo thứ tự

| # | Repo | Đọc gì | Lý do |
|---|---|---|---|
| 1 | [`affaan-m/everything-claude-code`](https://github.com/affaan-m/everything-claude-code) | `skills/verification-loop`, `skills/eval-harness`, `skills/strategic-compact`, `skills/search-first`, `skills/plankton-code-quality`, `skills/autonomous-loops`, `contexts/` | Nguồn chính, đã battle-tested, 78k stars, cập nhật tháng 3/2026 |
| 2 | [`FlorianBruniaux/claude-code-ultimate-guide`](https://github.com/FlorianBruniaux/claude-code-ultimate-guide) | Claudeception skill, context % strategy, verification patterns | Chuyên sâu về quality gates và meta-skills |
| 3 | [`shanraisshan/claude-code-best-practice`](https://github.com/shanraisshan/claude-code-best-practice) | Command→Agent→Skill architecture, cross-model review pattern | Best practices tổng hợp từ community |
| 4 | [`obra/superpowers`](https://github.com/obra/superpowers) | TDD, systematic-debugging, root-cause-tracing | Battle-tested core skills từ Jesse Vincent |
| 5 | [`sickn33/antigravity-awesome-skills`](https://github.com/sickn33/antigravity-awesome-skills) | Browse enterprise skill patterns | 1,259+ skills, path native cho Antigravity |

### File cụ thể cần đọc trong `affaan-m`

```
skills/verification-loop/SKILL.md     ← Quan trọng nhất
skills/eval-harness/SKILL.md          ← Đánh giá output
skills/strategic-compact/SKILL.md     ← Context management
skills/search-first/SKILL.md          ← Research trước code
skills/plankton-code-quality/SKILL.md ← Auto-lint khi edit
skills/autonomous-loops/SKILL.md      ← Self-running pipeline
skills/continuous-learning-v2/SKILL.md ← Nâng cấp /evolve
contexts/dev.md                        ← Dynamic context injection
contexts/review.md
agents/planner.md                      ← Brainstorm gate pattern
agents/architect.md
commands/verify.md                     ← /verify command
commands/checkpoint.md                 ← /checkpoint pattern
the-longform-guide.md                  ← Token optimization + memory persistence
```

---

## 6. Token optimization cho Antigravity (bonus)

Từ `affaan-m` longform guide, adapt cho Antigravity:

```markdown
# Quản lý token hiệu quả
- Dùng Gemini 2.5 Flash cho tasks đơn giản (debug nhỏ, format)
- Chỉ dùng Gemini 2.5 Pro cho architecture decisions, complex debugging
- MAX_THINKING_TOKENS: giới hạn ở 10,000 thay vì để mặc định
- Compact ngay sau research phase, trước khi bắt đầu code
- Không enable quá 10 MCP tools cùng lúc
```

---

*Tài liệu này tổng hợp từ phân tích AG-SKILL v2.0 (tampd/skill) đối chiếu với:*  
*affaan-m/everything-claude-code v1.8.0 (Mar 2026), FlorianBruniaux/claude-code-ultimate-guide, shanraisshan/claude-code-best-practice*
