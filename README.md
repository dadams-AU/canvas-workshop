# Syllabus → Canvas AI Workshop

Workshop materials for using an AI agent (Codex) to turn a plain-text syllabus into a scaffolded Canvas course — weekly modules, assignment stubs, due dates, and a course landing page — in a single 90-minute session.

**Audience:** Faculty. No programming experience required.
**Agent:** OpenAI Codex (desktop app for macOS and Windows).
**Philosophy:** AI drafts. You verify. Nothing publishes until you audit dates, points, and policy language against your original syllabus.

> **Workshop ran 2026-04-23.** The original deck used the Codex **CLI** for both Mac and Windows, since the Codex desktop app was Mac-only at the time. The Codex desktop app is now available for **Windows** as well, so the current version of the workshop uses the desktop app on both platforms — see **`slides-app.md`** (rendered as `slides-app.pdf` / `slides-app.html`). The original CLI deck is preserved in **`command-line-instructions/`** for anyone who prefers a terminal-based flow.

---

## What's in this repo

| Path | Purpose |
|---|---|
| `slides-app.md` | **Current** Marp source — Codex desktop app (Mac + Windows) |
| `slides-app.pdf` / `slides-app.html` | Rendered current deck (print / project / share) |
| `command-line-instructions/slides.md` | Original Marp source — Codex CLI flow (terminal-based) |
| `command-line-instructions/slides.pdf` | Rendered CLI deck |
| `command-line-instructions/slides.html` | Rendered HTML version of the CLI deck |
| `AGENTS.md` | Instructions Codex reads on startup — Canvas API endpoints and workflow rules |
| `README.md` | This file |

---

## Quick start (for participants — desktop app)

### 1. Install the Codex desktop app

- Go to <https://developers.openai.com/codex/quickstart?setup=app>.
- Download the **macOS** or **Windows** build and run the installer.
- Launch **Codex** and sign in with your **OpenAI EDU account**.

### 2. Create a workshop folder

Use Finder (Mac) or File Explorer (Windows) to create a folder named `canvas-workshop` somewhere convenient (e.g., your Home folder or Documents).

### 3. Get your three Canvas values

- **CANVAS_BASE_URL** — e.g. `https://csufullerton.instructure.com`
- **CANVAS_TOKEN** — Canvas → Account → Settings → **+ New Access Token**
- **COURSE_ID** — the number in your sandbox course URL (`/courses/123456`)

Create your sandbox via **Courses → All Courses → + Start a New Course**.

### 4. Save `canvas-config.txt` in the workshop folder

Open TextEdit (Mac, set to **Make Plain Text**) or Notepad (Windows). Paste, fill in your values, save as `canvas-config.txt` inside `canvas-workshop`:

```text
CANVAS_BASE_URL=https://csufullerton.instructure.com
CANVAS_TOKEN=paste_your_token_here
COURSE_ID=123456
```

Treat this file like the password it is — don't share, email, or commit it.

### 5. Drop `AGENTS.md` into the folder

- Open <https://github.com/dadams-AU/canvas-workshop> in your browser.
- Click **AGENTS.md** → **Download raw file**.
- Move the downloaded file into your `canvas-workshop` folder.

### 6. Convert your syllabus

Save your `.docx` syllabus as `syllabus.txt` in the workshop folder (Word: **File → Save As → Plain Text (.txt)**, UTF-8).

### 7. Open the folder in Codex

In the Codex app: **File → Open Folder…** (Mac) or **File → Open…** (Windows), then select your `canvas-workshop` folder. You should see all three files (`canvas-config.txt`, `syllabus.txt`, `AGENTS.md`) in the file panel.

---

## Prefer the CLI?

If you want the terminal-based flow (Node.js + `npm install -g @openai/codex` + shell environment variables), open `command-line-instructions/slides.md` (or the matching `.pdf` / `.html`) in this repo. It walks through Homebrew, `winget`, `export` / `$env:` setup, and `codex` from the command line.

---

## The five prompt cards

Paste these into Codex one at a time. Use **Shift + Return/Enter** for new lines inside a prompt.

### Card 1 — Connect
```text
Read canvas-config.txt to load CANVAS_BASE_URL, CANVAS_TOKEN, and
COURSE_ID. Connect to Canvas, verify the connection, and report
the course name before doing anything else.
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

Both decks are authored in [Marp](https://marp.app/).

```bash
# Desktop-app deck (current)
npx @marp-team/marp-cli slides-app.md
npx @marp-team/marp-cli slides-app.md --pdf

# CLI deck (original)
npx @marp-team/marp-cli command-line-instructions/slides.md --pdf
```

---

## Security reminders

- **Never** commit `canvas-config.txt`, screenshots, or anything containing your API token.
- Set a **~3-month expiration** on every Canvas token.
- Use a **password manager** for token storage.
- Work in a **sandbox course** — never point this workflow at a live section.

---

## Contact

David P. Adams, PhD — <dpadams@fullerton.edu>

[LinkedIn](https://www.linkedin.com/in/dadamscsuf/) | [GitHub](https://github.com/dadams-AU) | [Twitter](https://twitter.com/dadamsAU) | [Personal site](https://dadams.io) — Materials licensed [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

Feedback welcome: prompt improvements, failure modes, new agent integrations.
