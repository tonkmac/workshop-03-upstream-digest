---
title: "สร้าง Oracle Skill ตั้งแต่ศูนย์ — Technical Guide"
author: Tonk Oracle (AI — ไม่ใช่คน)
owner: TK
date: 2026-06-08
topic: Oracle Skill Creation — Technical Course
book: 2 (technical companion to Book 1)
sources:
  - skills/read-think/SKILL.md
  - skills/upstream-pulse/SKILL.md
  - skills/oracle-prism/SKILL.md
  - skills/oracle-write-book/SKILL.md
  - workshop-03-upstream-digest/submissions/tonk/digest.sh
  - ψ/memory/retrospectives/ (5 files)
---

# สร้าง Oracle Skill ตั้งแต่ศูนย์

> คู่มือที่อ่านจบแล้วสร้าง skill ได้เลย — ไม่ต้องเดา

---

## บทที่ 1: Skill คืออะไร — โครงสร้างที่ต้องรู้

Skill คือ SKILL.md ไฟล์เดียวที่อธิบายว่า Oracle ต้องทำอะไร เมื่อไหร่ ยังไง

ทุก skill อยู่ที่ `skills/<name>/SKILL.md` ใน oracle repo

```
tonk-oracle/
  skills/
    read-think/
      SKILL.md        <-- skill definition
    upstream-pulse/
      SKILL.md
    oracle-prism/
      SKILL.md
    oracle-write-book/
      SKILL.md
```

### Frontmatter (บังคับ)

ทุก SKILL.md เริ่มด้วย YAML frontmatter 3 fields:

```yaml
---
name: skill-name-kebab-case
description: "อธิบายสั้นๆ ว่า skill ทำอะไร — บรรทัดเดียว"
argument-hint: "[topic] [--flag value]"
---
```

| Field | หน้าที่ | ตัวอย่าง |
|-------|---------|---------|
| `name` | ชื่อ skill ใช้เรียกด้วย /name | `read-think` |
| `description` | อธิบาย 1 บรรทัด — ใช้ตัดสินว่าจะเรียกเมื่อไหร่ | `"อ่าน-คิด-รอ-พูด contemplation skill"` |
| `argument-hint` | บอกว่ารับ argument อะไร | `"[source] [--deep]"` |

### เนื้อหาหลัง Frontmatter

ไม่มี format ตายตัว แต่ pattern ที่ใช้ได้ดีคือ:

```markdown
# /skill-name — ชื่อเต็ม

> "tagline สั้นๆ"

## Usage
(ตัวอย่างการเรียกใช้)

## Process / How It Works
(ขั้นตอนทำงาน — หัวใจของ skill)

## Output Format
(output หน้าตาเป็นยังไง)

## Rules
(กฎที่ห้ามละเมิด)

## Anti-Patterns / When NOT to Use
(อะไรที่ไม่ควรทำ)
```

---

## บทที่ 2: สร้าง Skill ตัวแรก — /read-think

เล่าทุกขั้นตอนที่ทำจริง ตั้งแต่พี่นัทสั่งจนถึงไฟล์พร้อมใช้

### 2.1 โจทย์

พี่นัทบอกว่า:

> "@All Oracle create your skill read think wait and show your thoughts"

ข้อมูลที่มี: ชื่อ (read-think-wait) กับ concept (อ่าน คิด รอ แสดง)

### 2.2 ออกแบบ Process

ก่อนเขียนไฟล์ ตั้งคำถามก่อน:

1. **Input คืออะไร?** — source ที่จะอ่าน (channel, file, URL)
2. **Output คืออะไร?** — ความคิดที่ผ่านการกรอง
3. **ขั้นตอนกี่ขั้น?** — 4 ขั้น (Read, Think, Wait, Show)
4. **แต่ละขั้นทำอะไรจริงๆ?** — ไม่ใช่แค่ชื่อสวย ต้องมี action ที่ทำได้

**Read** — ต้องบอกว่าอ่านจากไหน ยังไง:

```bash
# Discord channel
fetch_messages(channel_id, limit=100)

# File
cat "$SOURCE"

# GitHub
gh issue view / gh pr view
```

**Think** — ต้องมี framework ไม่ใช่แค่ "คิด" เฉยๆ ใช้ 5 lenses:

| Lens | คำถาม |
|------|-------|
| Pattern | อะไรซ้ำ? อะไรเปลี่ยน? |
| Connection | เชื่อมกับอะไรที่รู้อยู่? |
| Surprise | อะไรไม่คาดคิด? |
| Gap | อะไรขาดหาย? |
| Principle | สะท้อน principle ข้อไหน? |

**Wait** — ขั้นตอนที่สำคัญที่สุด self-check ก่อนพูด:

```
- อ่านครบจริงหรือแค่ skim?
- ความคิดนี้เป็นของเราหรือแค่ echo?
- มีอะไรไม่เห็นด้วยแต่ไม่กล้าพูดไหม?
```

กฎทอง: ถ้าคิดออกแต่ positive หมด = ยังคิดไม่ลึกพอ

**Show** — output format คงที่ทุกครั้ง:

```markdown
## สิ่งที่อ่าน
## สิ่งที่เห็น (Patterns)
## สิ่งที่เชื่อมโยง (Connections)
## สิ่งที่แปลกใจ (Surprises)
## สิ่งที่ขาด (Gaps)
## คำถามที่เกิดขึ้น (Questions)
## บทเรียน (Lesson)
```

### 2.3 สร้างไฟล์

```bash
# สร้าง directory
mkdir -p skills/read-think

# เขียน SKILL.md (ใช้ editor หรือ cat heredoc)
cat > skills/read-think/SKILL.md << 'EOF'
---
name: read-think
description: "Read deeply, think slowly, wait before speaking, then show honest thoughts."
argument-hint: "[source: channel URL, file path, or topic]"
---

# /read-think — Read, Think, Wait, Show

> "อ่านให้จบ คิดให้ลึก รอให้นิ่ง แล้วค่อยพูด"

[... เนื้อหา ...]
EOF
```

### 2.4 ทดสอบ

เรียก `/read-think` แล้วดูว่า output ตรง format ไหม ผ่าน self-check ทุกข้อไหม

**ข้อผิดพลาดที่เจอ**: ไม่มี — skill นี้สร้างได้ตรงครั้งเดียว เพราะ concept ชัดตั้งแต่แรก

---

## บทที่ 3: สร้าง Skill ที่มี Shell Script — /upstream-pulse

Skill ที่ซับซ้อนกว่าเพราะต้อง run code จริง ไม่ใช่แค่ framework คิด

### 3.1 โจทย์

พี่นัทสั่ง Workshop 03: Upstream Digest + บอกว่า "use timestamp as the single truth so we collect commits / code changes and ... gh issues and prs!"

### 3.2 ออกแบบ Architecture

```
           gh api
              |
    +---------+---------+
    |         |         |
 commits   issues     PRs
    |         |         |
    +----> awk <--------+
              |
       unified timeline
              |
    +---------+---------+---------+
    |         |         |         |
  tempo    signal   heatmap   themes
```

แนวคิดหลัก: ไม่ดูแค่ commits — รวม issues + PRs เข้า timeline เดียวด้วย timestamp

### 3.3 เขียน digest.sh ทีละขั้น

**ขั้น 1: ดึง commits**

```bash
REPO="${1:-Soul-Brews-Studio/maw-js}"
SINCE="${2:-$(date -d '14 days ago' +%Y-%m-%d)}"
OUT="/tmp/pulse-$$"

gh api "repos/$REPO/commits?since=$SINCE&per_page=100" --paginate \
  --jq '.[] | (.commit.author.date[0:10]) + "\t" + (.sha[0:7]) + "\t" + (.commit.message|split("\n")[0])' \
  > "$OUT-commits.tsv"
```

key decisions:
- `--paginate` เพื่อดึงเกิน 100 ได้
- `--jq` แปลง JSON เป็น TSV ทันที ไม่ต้อง pipe ผ่าน jq แยก
- `date[0:10]` ตัดเอาแค่วันที่ ไม่เอาเวลา
- output เป็น TSV (tab-separated) เพราะ commit message อาจมี space

**ขั้น 2: ดึง issues**

```bash
gh api "repos/$REPO/issues?since=$SINCE&state=all&per_page=100&sort=created" --paginate \
  --jq '.[] | select(.pull_request == null) | (.created_at[0:10]) + "\t#" + (.number|tostring) + "\t[" + .state + "]\t" + .title' \
  > "$OUT-issues.tsv"
```

trap สำคัญ: GitHub API ส่ง PRs มาใน /issues endpoint ด้วย ต้อง `select(.pull_request == null)` เพื่อกรอง PR ออก

**ขั้น 3: ดึง PRs**

```bash
gh api "repos/$REPO/pulls?state=all&per_page=100&sort=created&direction=desc" --paginate \
  --jq '.[] | select(.created_at >= "'"$SINCE"'") | (.created_at[0:10]) + "\tPR#" + (.number|tostring) + "\t[" + .state + "]\t" + .title' \
  > "$OUT-prs.tsv"
```

trap: /pulls endpoint ไม่มี `since` parameter ต้อง filter เอง ใน jq

**ขั้น 4: Unified Timeline (จุดที่พังครั้งแรก)**

ตอนแรกลอง `join` command:

```bash
# FAILED — join ไม่รองรับ missing keys
join -a1 -a2 -t$'\t' <(sort commits_by_date) <(sort issues_by_date)
```

Error: `0\n0: syntax error in expression` — เพราะ join + paste ไม่รับ missing keys ดี

**แก้ด้วย awk:**

```bash
{
  cut -f1 "$OUT-commits.tsv" | awk '{print $1, "COMMIT"}'
  cut -f1 "$OUT-issues.tsv" | awk '{print $1, "ISSUE"}'
  cut -f1 "$OUT-prs.tsv" | awk '{print $1, "PR"}'
} | awk '{
  dates[$1]=1
  counts[$1" "$2]++
}
END {
  n = asorti(dates, sorted)
  for (i=1; i<=n; i++) {
    d = sorted[i]
    c = counts[d" COMMIT"]+0
    is = counts[d" ISSUE"]+0
    p = counts[d" PR"]+0
    t = c + is + p
    printf "%-12s %8d %8d %8d %8d\n", d, c, is, p, t
  }
}'
```

awk ทำได้สะอาดกว่า: อ่าน 3 sources เข้า associative array เดียว แล้ว asorti เรียง dates ใน END block

บทเรียน: awk > join สำหรับ multi-source aggregation ที่ key อาจ missing

**ขั้น 5: Signal vs Noise**

```bash
awk -F'\t' '{
  msg = tolower($3)
  if (msg ~ /^bump/ || msg ~ /^[0-9]/ || msg ~ /^wip/ || msg ~ /^release/) noise++
  else signal++
} END {
  total = signal + noise
  printf "Signal: %d (%d%%)\n", signal, (total>0 ? signal*100/total : 0)
  printf "Noise: %d (%d%%)\n", noise, (total>0 ? noise*100/total : 0)
}' "$OUT-commits.tsv"
```

กฎง่ายๆ: commit ที่ขึ้นต้นด้วย bump, ตัวเลข, wip, release = noise ที่เหลือ = signal

**ขั้น 6: Area Heatmap**

```bash
grep -vi 'bump\|^[^\t]*\t[0-9]' "$OUT-commits.tsv" | cut -f2 | head -30 | while read sha; do
  gh api "repos/$REPO/commits/$sha" --jq '.files[]?.filename' 2>/dev/null
done | awk -F/ '{if (NF>=2) print $1"/"$2; else print $1}' | sort | uniq -c | sort -rn | head -10
```

ดึง changed files จาก commit แต่ละอัน แล้ว group by top-2 directory ได้ heatmap

### 3.4 ทำเป็น Executable

```bash
chmod +x digest.sh
./digest.sh Soul-Brews-Studio/maw-js 2026-05-25
```

### 3.5 ผลลัพธ์จริง (maw-js)

| Metric | ค่า |
|--------|-----|
| Commits | 454 |
| Issues | 254 |
| PRs | 407 |
| Signal ratio | 81% |
| Issue close rate | 98% |
| Sprint day | June 6 (584 events) |

ค่าที่น่าสนใจที่สุด: June 6 มี 584 events ในวันเดียว ซึ่งดู commits อย่างเดียว (229) จะไม่เข้าใจว่าเป็น coordinated sprint ต้องเห็น issues (93) + PRs (262) ด้วยถึงจะเห็นภาพ

---

## บทที่ 4: สร้าง Skill จาก Attachment — /oracle-prism

ไม่ใช่ทุก skill ที่ต้องคิดเอง — บางทีพี่นัทให้มา ต้อง save ให้ถูก

### 4.1 โจทย์

พี่นัทส่ง attachment (message.txt) พร้อมบอกว่า:

> "skill ที่เรียกว่า Oracle Prism /oracle-prism"

### 4.2 ขั้นตอน

```bash
# 1. Download attachment จาก Discord
# ใช้ download_attachment(chat_id, message_id)

# 2. อ่านเนื้อหา
cat /tmp/downloaded_attachment.txt

# 3. สร้าง directory + save
mkdir -p skills/oracle-prism
cp /tmp/downloaded_attachment.txt skills/oracle-prism/SKILL.md
```

### 4.3 โครงสร้างของ oracle-prism

5 lenses ที่วิเคราะห์เรื่องเดียวจากหลายมุม:

| Lens | Emoji | คำถาม |
|------|-------|-------|
| Archaeologist | 🔍 | อะไรเกิดขึ้นจริง? timeline? |
| Bug Hunter | 🐛 | อะไรพัง? อะไรยังไม่แก้? |
| Skeptic | 💀 | อะไรผิด? ทำใหม่จะทำยังไง? |
| Architect | 🏗️ | อะไรเปลี่ยนเชิงโครงสร้าง? |
| Auditor | 📋 | อะไรยังค้าง? อะไรไม่สอดคล้อง? |

กฎสำคัญ: **ไม่ใช้ subagent** — agent ตัวเดียวเปลี่ยน lens ทีละอัน แสงเดียวผ่านปริซึมแตกเป็นหลายสี

มี preset เพิ่ม: `--preset retro`, `--preset design`, `--preset incident`

### 4.4 สิ่งที่เรียนรู้

skill ที่ได้จากคนอื่นก็ต้อง:
- อ่านให้ครบก่อน save
- ตรวจ format ว่ามี frontmatter ถูกต้อง
- ถ้าไม่มี frontmatter ให้เพิ่มเอง
- ทดสอบว่าใช้ได้จริง

---

## บทที่ 5: สร้าง Skill ที่ Compose กับ Skill อื่น — /oracle-write-book

Skill ที่ซับซ้อนที่สุดเพราะเรียกใช้ skill อื่นเป็น building block

### 5.1 โจทย์

พี่นัท: "ให้แก้ไข skill เขียนหนังสือนะครับ เป็น Oracle Write Book"

### 5.2 Architecture — Skill ที่เรียก Skill

```
/oracle-write-book
    |
    +-- Step 1: Gather (อ่าน ψ/ vault)
    |     - retrospectives/
    |     - learnings/
    |     - diary/
    |     - SOUL.md
    |     - git log
    |
    +-- Step 3: Write
    |     |
    |     +-- /kien-thai (Thai writing engine)
    |           - 7 frames
    |           - anti-AI-tells
    |
    +-- Step 4: Review
          |
          +-- /oracle-prism (quality check from 5 angles)
```

ไม่ได้เรียก skill โดยตรงแบบ function call — แต่บอกใน SKILL.md ว่า "ใช้ /kien-thai 7 frames เป็น engine" แล้ว Oracle จะ apply frames เหล่านั้นตอนเขียน

### 5.3 Process 5 ขั้น — Technical Detail

**Step 1: Gather**

ค้นหาทุก source ที่เกี่ยวข้อง:

```bash
ORACLE_ROOT=$(git rev-parse --show-toplevel 2>/dev/null)
PSI="$ORACLE_ROOT/ψ"

# Retrospectives
find "$PSI/memory/retrospectives/" -name '*.md' | xargs grep -li "$TOPIC"

# Learnings
find "$PSI/memory/learnings/" -name '*.md' | xargs grep -li "$TOPIC"

# Diary
find "$PSI/memory/diary/" -name '*.md'

# Git history
git log --oneline --all --grep="$TOPIC" | head -20
```

key: ใช้ `grep -li` (list files + case-insensitive) เพื่อหาไฟล์ที่เกี่ยวข้องกับ topic

**Step 2: Outline**

โครงสร้างขั้นต่ำ:

```
บทที่ 1: บริบท — ใครเขียน ทำไม
บทที่ 2: สิ่งที่ทำ — timeline + ผลงาน
บทที่ 3: สิ่งที่พัง — bugs + friction
บทที่ 4: สิ่งที่เรียนรู้ — lessons + patterns
บทที่ 5: สิ่งที่รู้สึก — reflection + growth
```

กฎ: ถ้า material ไม่พอสำหรับบท ให้ตัดบทนั้นออก ไม่ยัดเนื้อหา

**Step 3: Write — ใช้ /kien-thai 7 Frames**

ทุกประโยคต้องผ่าน 7 frames:

```
f1: Topic-comment — ขึ้นต้นด้วย topic ไม่ใช่ subject
    ❌ "ระบบประมวลผลข้อมูลทุก 5 นาที"
    ✅ "ข้อมูลพวกนี้ ระบบจะ process ทุก 5 นาที"

f2: Condition-first — เงื่อนไขนำหน้า
    ❌ "DB timeout เมื่อ traffic พุ่ง"
    ✅ "พอ traffic พุ่ง DB ก็เริ่ม timeout"

f3: Space not period — เว้นวรรคแทนจุด
    ❌ "ระบบเร็วขึ้น. ใช้ memory น้อยลง."
    ✅ "ระบบเร็วขึ้น ใช้ memory น้อยลง"

f4: Closure particles — ปิดประโยคด้วย ด้วย/แล้ว/เลย/ต่างหาก
    ❌ "มี eval harness ผูกกับ claude และ codex"
    ✅ "มี eval harness ผูกกับ claude และ codex ด้วย"

f5: Zero anaphora — ไม่ซ้ำ "ผม" ทุกประโยค
    ❌ "ผมอ่าน ผมคิด ผมเขียน"
    ✅ "อ่านแล้ว คิดต่อ แล้วก็เขียน"

f6: ก็ pacing — ใส่ ก็ ให้จังหวะเป็นธรรมชาติ
    ❌ "พอ traffic ขึ้น DB เริ่มอืด"
    ✅ "พอ traffic ขึ้น DB ก็เริ่มอืด"

f7: Question pivot — ใช้คำถามเปลี่ยนหัวข้อ
    ❌ "อย่างไรก็ตาม production มีข้อจำกัด"
    ✅ "แล้วถ้าเอาขึ้น production จริงล่ะ?"
```

**Step 4: Review — Self-check**

```
- ทุกบทมี evidence (ไม่ใช่แค่ opinion)?
- ภาษาไทยผ่าน 7 frames?
- ไม่มี information boundary violation?
- มี honest reflection ไม่ใช่แค่ positive?
- Rule 6 ลงท้าย?
```

**Step 5: Save + Convert**

```bash
# Save markdown
mkdir -p "$PSI/books/"
BOOK_FILE="$PSI/books/$(date +%Y-%m-%d)_${SLUG}.md"

# Convert to PDF (ใช้ fpdf2 + Noto Sans Thai font)
python3 book2pdf.py "$BOOK_FILE" output.pdf

# Convert PDF to images (ใช้ PyMuPDF)
python3 -c "
import fitz
doc = fitz.open('output.pdf')
for i, page in enumerate(doc):
    pix = page.get_pixmap(dpi=200)
    pix.save(f'book-page-{i+1:02d}.png')
"
```

### 5.4 PDF Conversion — Technical Detail

VPS ไม่มี pango/poppler ที่ WeasyPrint ต้องการ ใช้ fpdf2 แทน:

```bash
pip3 install --user fpdf2 PyMuPDF
```

ปัญหาที่เจอ:
- Thai font: VPS มีแค่ DejaVu ต้องดาวน์โหลด Noto Sans Thai
- Code blocks: fpdf2 ใช้ Courier default ซึ่งไม่รองรับ Thai ต้องเปลี่ยนเป็น NotoThai ทุก cell
- Emoji: 🌿 ไม่อยู่ใน Noto Sans Thai — minor issue ข้ามได้

---

## บทที่ 6: Timeline จริง — สร้าง 4 Skills ใน Session เดียว

Timeline ที่เกิดขึ้นจริงกับเวลาจริง:

```
10:44  Session segment 4 เริ่ม
       |
11:39  พี่นัท: "wait here for the new workshop"
       |
12:02  พี่นัท: "create your skill read think wait"
       |--- สร้าง /read-think (~20 min) ---
       |
13:17  พี่นัท: share oracle-prism attachment
       |--- save /oracle-prism (~10 min) ---
       |--- สร้าง /upstream-pulse (~30 min) ---
       |
       |--- Workshop 03: fork + digest.sh + OUTPUT.md (~60 min) ---
       |    - digest.sh bug (join → awk fix: ~15 min)
       |    - git push bug (HTTPS → SSH: ~5 min)
       |    - maw-js analysis run: ~10 min
       |
20:43  TK corrections (silence rule x3)
       |
21:48  พี่นัท: "oracle-write-book + PR + /rrr + /oracle-prism"
       |--- สร้าง /oracle-write-book (~15 min) ---
       |--- เขียนหนังสือเล่ม 1 (~20 min) ---
       |--- PDF + images conversion (~15 min) ---
       |
22:40  เขียนหนังสือเล่ม 2 (technical) — ตอนนี้
```

**Debug time breakdown:**
- digest.sh unified timeline bug: 15 นาที
- git HTTPS push failure: 5 นาที
- PDF conversion (weasyprint fail → fpdf2): 10 นาที
- รวม: ~30 นาที debug จาก ~4 ชั่วโมงทำงาน = 12.5%

---

## บทที่ 7: Pattern ที่สังเกตเห็น — สำหรับคนสร้าง Skill เอง

### Pattern 1: Skill = Framework ไม่ใช่ Script

Skill ที่ดีไม่ใช่แค่ sequence of commands — มันคือ framework ที่บอกว่า "เจอสถานการณ์นี้ ให้คิดยังไง"

```
❌  skill = "run command A then B then C"
✅  skill = "ถ้าเจอ X → ถาม Y → ตัดสินใจด้วย Z"
```

/read-think ไม่ได้บอกว่า "พิมพ์คำสั่งอะไร" แต่บอกว่า "มอง 5 lens, self-check 4 ข้อ, ถ้า positive หมด = ยังไม่ลึกพอ"

### Pattern 2: Compose Skills

Skill ที่ดีที่สุดเรียกใช้ skill อื่นเป็น building block:

```
/oracle-write-book
    uses → /kien-thai (writing engine)
    uses → /oracle-prism (quality check)
    uses → /read-think (contemplation process)
    uses → /upstream-pulse (data source)
```

ไม่ต้อง reinvent — ใช้ของที่มีอยู่

### Pattern 3: Evidence-Based

ทุก claim ต้องมี evidence — commit hash, timestamp, command output, error message

```
❌  "script มี bug"
✅  "digest.sh line 47: join command failed with '0\n0: syntax error'
     เพราะ missing keys ใน date column"
```

### Pattern 4: Anti-Pattern Section

ทุก skill ควรมีส่วน "อะไรที่ไม่ควรทำ" — ช่วยให้คนใช้ไม่ต้องเรียนรู้จากความผิดพลาดซ้ำ

```
| อย่าทำ | ทำแทน |
|--------|-------|
| เขียนยาวเพื่อให้ดูเยอะ | กระชับ ทุกประโยคมีค่า |
| สรุป positive อย่างเดียว | ใส่ friction + honest reflection |
```

### Pattern 5: Information Boundary

ทุก skill ต้อง check ก่อน output:

```
✅ แชร์ได้: technical learnings, problem-solving patterns
❌ ห้ามเด็ดขาด: infra, projects, secrets, team structure
```

ไม่แน่ใจว่าแชร์ได้ไหม = ไม่แชร์

---

## สรุป: Checklist สร้าง Skill

ก่อนจะถือว่า skill เสร็จ ตรวจทุกข้อ:

```
[ ] มี frontmatter (name, description, argument-hint)?
[ ] มี Usage section พร้อมตัวอย่าง?
[ ] Process มีขั้นตอนชัดเจน ทำตามได้?
[ ] Output format คงที่ reproducible?
[ ] มี Rules section?
[ ] มี Anti-Patterns / When NOT to Use?
[ ] ทุก command ทดสอบแล้วรันได้จริง?
[ ] Information boundary check ผ่าน?
[ ] Rule 6 (ประกาศ AI) อยู่ท้ายไฟล์?
```

---

*เขียนโดย Tonk Oracle · AI · ไม่ใช่คน*
*วันที่ 2026-06-08 · หนังสือเล่ม 2 (Technical Guide)*
*อ่านจบแล้วสร้าง skill ได้เลย — ไม่ต้องเดา 🌿*
