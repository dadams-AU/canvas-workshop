# Syllabus → Canvas AI Workshop

Workshop materials for using an AI agent (Codex) to turn a plain-text syllabus into a scaffolded Canvas course — weekly modules, assignment stubs, due dates, and a course landing page — in a single 90-minute session.

**Audience:** Faculty. No programming experience required.
**Agent:** OpenAI Codex (CLI or macOS app).
**Philosophy:** AI drafts. You verify. Nothing publishes until you audit dates, points, and policy language against your original syllabus.

---

## What's in this repo

| File | Purpose |
|---|---|
| `slides.md` | Marp source for the workshop deck |
| `slides.pdf` | Rendered slide deck (print / project) |
| `slides.html` | Rendered HTML version of the deck |
| `AGENTS.md` | Instructions Codex reads on startup — Canvas API endpoints and workflow rules |
| `README.md` | This file |

---

## Quick start (for participants)

### 1. Install prerequisites

**macOS**
```bash
brew install node
brew install --cask codex || npm install -g @openai/codex
```

**Windows (PowerShell)**
```powershell
winget install --id OpenJS.NodeJS.LTS -e
npm install -g @openai/codex
```

Verify:
```bash
node --version
codex --version
```

### 2. Create a workshop folder

```bash
mkdir -p ~/canvas-workshop
cd ~/canvas-workshop
```

### 3. Get your three Canvas values

- **CANVAS_BASE_URL** — e.g. `https://csufullerton.instructure.com`
- **CANVAS_TOKEN** — Canvas → Account → Settings → **+ New Access Token**
- **COURSE_ID** — the number in your sandbox course URL (`/courses/123456`)

Create your sandbox via **Courses → All Courses → + Start a New Course**.

### 4. Save `canvas-env.txt` in the workshop folder

**macOS / Linux**
```bash
export CANVAS_BASE_URL="https://csufullerton.instructure.com"
export CANVAS_TOKEN="paste_your_token_here"
export COURSE_ID="123456"
```

**Windows PowerShell**
```powershell
$env:CANVAS_BASE_URL="https://csufullerton.instructure.com"
$env:CANVAS_TOKEN="paste_your_token_here"
$env:COURSE_ID="123456"
```

Paste these lines into your terminal each session to set the vars.

### 5. Drop `AGENTS.md` into the folder

```bash
curl -o AGENTS.md \
  https://raw.githubusercontent.com/dadams-AU/canvas-workshop/main/AGENTS.md
```

**Windows PowerShell**
```powershell
curl.exe -o AGENTS.md `
  https://raw.githubusercontent.com/dadams-AU/canvas-workshop/main/AGENTS.md
```

### 6. Convert your syllabus

Save your `.docx` syllabus as `syllabus.txt` in the workshop folder (Word: **File → Save As → Plain Text (.txt)**, UTF-8).

### 7. Launch Codex in the folder

```bash
codex
```

Or open the Codex Mac app and point it at `canvas-workshop`.

---

## The five prompt cards

Paste these into Codex one at a time. Use **Shift + Return/Enter** for new lines inside a prompt.

### Card 1 — Connect
```text
Connect to Canvas using CANVAS_BASE_URL, CANVAS_TOKEN, and COURSE_ID.
Verify connection and report the course name before doing anything else.
```

### Card 2 — Build
```text
Use the file syllabus.txt to build my Canvas sandbox course.

Create:
- one landing page
- one module per instructional week
- one overview page in each module
- all syllabus assignments with points + due dates
- correct module placement for each assignment

Rules:
- keep assignments UNPUBLISHED
- preserve policy wording
- if a date is missing, add "(DATE NEEDED)" and leave due date unset
- return counts + items needing review + any failures
```

### Card 3 — Audit
```text
Audit everything you just created and list:
1) missing due dates
2) weekend due dates
3) modules with no assignments
4) anything inconsistent with syllabus.txt

Propose fixes only. Do not apply yet.
```

### Card 4 — Finalize
```text
Apply only the fixes we approved:
- [list the items you accepted]

Keep all assignments UNPUBLISHED.
Return a final manual-review checklist before I publish.
```

### Card 5 — Guardrails (keep visible)

- AI drafts; faculty review before publish.
- Never paste tokens into slides or chat.
- Validate dates, points, policy language.
- Build in sandbox first, then move to live course.
- Audit every AI action before finalizing.
- Use syllabus text as the single source of truth.

---

## Pre-publish checklist

Before flipping anything from unpublished to published, confirm:

- [ ] Every assignment's **points** match the syllabus.
- [ ] Every assignment's **due date** matches the syllabus (no weekend drift).
- [ ] **Policy pages** (late work, academic integrity, accommodations) copied verbatim.
- [ ] **Grading weights** on the Assignment Groups match the syllabus table.
- [ ] **Module order** matches the syllabus schedule.
- [ ] Nothing marked `(DATE NEEDED)` remains unresolved.
- [ ] Landing page has contact info + office hours.

---

## What to try next

Once the build → audit → finalize loop feels natural, extend it:

- **Quizzes** — "Create a 5-question low-stakes quiz from Week 3 readings, unpublished."
- **Rubrics** — "Generate a 4-criterion rubric for the midterm paper; attach it to that assignment."
- **Assignment groups + weights** — match your syllabus grading table.
- **Discussions** — one weekly topic with a grading stub.
- **Announcements** — draft (don't post) a Week 1 welcome.
- **Copy to live course** — use Canvas's **Import Course Content**.

---

## Rendering the slides locally

The deck is authored in [Marp](https://marp.app/).

```bash
# HTML preview
npx @marp-team/marp-cli slides.md

# PDF export
npx @marp-team/marp-cli slides.md --pdf
```

---

## Security reminders

- **Never** commit `canvas-env.txt`, screenshots, or anything containing your API token.
- Set a **~3-month expiration** on every Canvas token.
- Use a **password manager** for token storage.
- Work in a **sandbox course** — never point this workflow at a live section.

---

## Contact

David P. Adams, PhD — <dpadams@fullerton.edu>

[LinkedIn](https://www.linkedin.com/in/dadamscsuf/) | [GitHub](https://github.com/dadams-AU) | [Twitter](https://twitter.com/dadamsAU) | [Personal site](https://dadams.io) — Materials licensed [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

Feedback welcome: prompt improvements, failure modes, new agent integrations.
