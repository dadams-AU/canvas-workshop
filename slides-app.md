---
marp: true
theme: default
paginate: true
title: Syllabus → Canvas AI Workshop (Codex Desktop App)
author: David P. Adams, PhD
date: 2026-04-24
style: |
  section { font-size: 26px; }
  section h1 { font-size: 44px; }
  section h2 { font-size: 34px; }
  code { font-size: 22px; }
  pre { font-size: 20px; line-height: 1.35; }
  .small { font-size: 20px; color: #475569; }
  .kicker { font-size: 18px; letter-spacing: .08em; text-transform: uppercase; color: #0e7490; }
  .two-col { display: grid; grid-template-columns: 1fr 1fr; gap: 24px; }
  .warn { background: #fef3c7; border-left: 5px solid #b45309; padding: 10px 14px; border-radius: 6px; }
  .ok { background: #ecfdf5; border-left: 5px solid #047857; padding: 10px 14px; border-radius: 6px; }
  .section { background: #0f172a; color: #f8fafc; }
  .section h1 { color: #f8fafc; }
---

<!-- _class: section -->

<span class="kicker">Faculty Development Workshop · 90 minutes · Desktop app edition</span>

# Syllabus → Canvas, with an AI Agent

**Turn a plain-text syllabus into a scaffolded Canvas course — modules, assignments, due dates, landing page — in one session.**

David P. Adams, PhD · <dpadams@fullerton.edu>

Slides + resources: **github.com/dadams-AU/canvas-workshop**

<!-- _footer: 'Sandbox only. No terminal required. AI drafts; you verify; nothing publishes until you audit.' -->

---

# Who this workshop is for

- Faculty who want a **faster starting point** for a Canvas shell.
- You do **not** need to open a terminal.
- You do **not** need to have used Canvas's API before.
- You do **not** need to be a programmer.

<div class="warn">
<strong>Account note:</strong> CSUF-managed Google accounts block the Gemini CLI. Our OpenAI EDU accounts work with <strong>Codex</strong>, so that's what we'll use today — through the desktop app for Mac and Windows.
</div>

---

# What you will leave with

- A **sandbox Canvas course** scaffolded from your own syllabus.
- A reusable set of **five prompt cards**.
- A **pre-publish checklist** you can adapt to any course.
- Everything on GitHub: **github.com/dadams-AU/canvas-workshop**

<div class="ok">
<strong>Our standard:</strong> The agent drafts. You verify. Nothing goes live until dates, points, and policy language have been audited against your original syllabus.
</div>

---

# Agenda (90 min)

| Time | Segment |
|---|---|
| 0:00 – 0:05 | Welcome + outcome preview |
| 0:05 – 0:15 | Concept primer (agent, API token, sandbox) |
| 0:15 – 0:25 | **Install** the Codex desktop app |
| 0:25 – 0:45 | **Canvas:** sandbox → token → course ID → config file |
| 0:45 – 0:55 | Prep syllabus + AGENTS.md |
| 0:55 – 1:15 | Live demo: connect → build → audit → finalize |
| 1:15 – 1:25 | Hands-on lab |
| 1:25 – 1:30 | What to try next + checklist + resources |

---

# The faculty-first workflow

```text
  syllabus.docx  →  syllabus.txt  →  Codex agent  →  Canvas sandbox
                                          ↓
                                   you audit (dates,
                                   policy, points)
                                          ↓
                                   publish (when ready)
```

Your judgement is the final gate. The agent's job is to **save you typing**, not to make teaching decisions.

---

# Guardrails (we'll repeat these)

- **Sandbox only** during the workshop.
- **Unpublished by default** — the agent never publishes for you.
- **Never paste tokens** into chat, slides, screenshots, or screen shares.
- **Syllabus is the source of truth** — if it's not in the syllabus, it doesn't belong in Canvas.
- **Audit before publish** — dates, grading weights, policy wording.

---

<!-- _class: section -->

<span class="kicker">Part 1 · 10 minutes</span>

# Concept primer

Three words you'll hear all day: **agent**, **API token**, **sandbox**.

---

# What is an AI agent?

- A **chatbot** answers questions in a browser tab.
- An **agent** can **take actions** on your behalf: read files, make API calls, create things in Canvas.
- You approve each action it wants to take (or set auto-approve for safe ones).

> Think: a very fast teaching assistant who asks permission before touching anything.

The Codex desktop app is the agent. It opens a project folder on your computer and works inside it.

---

# What is an API token?

- A **password Canvas gives you** that lets programs act **as you**.
- If someone else gets it, they can see and change everything you can — so treat it like a password.
- We'll set an **expiration** and give it a **name** we'll recognize.
- Store it in a **password manager** (Bitwarden, 1Password, LastPass).

<div class="warn">
Never paste a token into Slack, email, a slide, a Zoom chat, or a screenshot.
</div>

---

# What is a sandbox course?

- A Canvas shell with **no students** that only you can see.
- **You can create one yourself** — we'll do that in a few minutes.
- Everything today happens here. Later, you copy content to your live course using Canvas's **Import Course Content**.

---

# About the Codex desktop app

- A regular desktop window — **no terminal required**.
- Available for **macOS** and **Windows**.
- Sign in with your **OpenAI EDU account**.
- You point it at a folder on your computer; it reads the files there and acts on your instructions.

<span class="small">There is also a Codex CLI for people who like the terminal. The earlier version of this workshop used the CLI — see <code>command-line-instructions/</code> in the repo if you want those instructions.</span>

---

<!-- _class: section -->

<span class="kicker">Part 2 · 10 minutes</span>

# Install the Codex desktop app
### macOS + Windows

---

# macOS — Install the Codex app

1. Open Safari or Chrome and go to **<https://developers.openai.com/codex/quickstart?setup=app>**.
2. Download the **macOS** build.
3. Open the `.dmg` and **drag Codex into your Applications folder**.
4. Launch **Codex** from Applications (or Spotlight: ⌘ Space → "Codex").
5. Click **Sign in** and use your **OpenAI EDU account**.

<div class="ok">
You'll know it worked when you see the Codex home window with a "Open folder" or "New project" option.
</div>

---

# Windows — Install the Codex app

1. Open Edge or Chrome and go to **<https://developers.openai.com/codex/quickstart?setup=app>**.
2. Download the **Windows** installer (`.exe` or `.msi`).
3. Double-click the installer and follow the prompts. Accept the defaults.
4. Launch **Codex** from the Start menu.
5. Click **Sign in** and use your **OpenAI EDU account**.

<div class="warn">
If Windows SmartScreen warns about an unrecognized app, click <strong>More info → Run anyway</strong> — only after confirming the download came from <code>developers.openai.com/codex</code>.
</div>

---

# Verify it launches

You should now have:

- The **Codex** app installed
- A **signed-in session** tied to your OpenAI EDU account
- A home screen offering to **open a folder** or **start a new project**

If sign-in fails: confirm you're using your **EDU** account (not a personal one) and that pop-ups aren't blocked.

---

# Common install failures

| Symptom | Fix |
|---|---|
| Mac says "Codex can't be opened, unidentified developer" | Right-click Codex in Applications → **Open** → confirm |
| Windows SmartScreen blocks the installer | **More info → Run anyway** (after confirming the source) |
| Sign-in loops or fails | Switch browsers, allow pop-ups, confirm EDU account |
| Corporate laptop blocks install | Use a personal device for the workshop |
| `401 Unauthorized` later (in Codex) | Canvas token invalid or expired — regenerate |

---

# Create your workshop folder

Make a folder on your computer — we'll put everything in it.

**macOS (Finder)**
- Open Finder → go to your **Home** folder.
- **File → New Folder** → name it `canvas-workshop`.

**Windows (File Explorer)**
- Open File Explorer → go to **This PC → Documents** (or your home folder).
- **Right-click → New → Folder** → name it `canvas-workshop`.

We'll come back to this folder in a few minutes.

---

<!-- _class: section -->

<span class="kicker">Part 3 · 20 minutes</span>

# Canvas side
### Sandbox course → API token → course ID → config file

---

# Step 1 — Create an empty sandbox course

In Canvas:

1. Click **Courses** in the left navigation.
2. Click **All Courses** at the bottom of the flyout.
3. Click **+ Start a New Course** (top right).
4. Name it something like `SANDBOX — [your name] — AI Workshop`.
5. Leave it **unpublished**. Do not enroll any students.

<div class="ok">
You only need to do this once. Re-use the same sandbox for future workshops.
</div>

---

# Step 2 — Account → Settings → New Access Token

- Click your **profile icon** (top-left avatar) → **Account** → **Settings**.
- Scroll down to **Approved Integrations**.
- Click **+ New Access Token**.
- **Purpose:** `Syllabus to Canvas AI Workshop`
- **Expires:** pick a date ~3 months out. Don't use "never."
- Click **Generate Token**.
- **Copy the entire string** — Canvas only shows it to you **once**.

<div class="warn">
If you close the dialog without copying, you must delete this token and generate a new one.
</div>

---

# Step 3 — Save the token securely

- Paste it into your **password manager** as a new entry.
  - Title: `Canvas API token — workshop`
  - Notes: the expiration date
- **Do not** email it to yourself. **Do not** put it in a shared doc.

We'll paste the token one more time — into a local file in your `canvas-workshop` folder — in two slides.

---

# Step 4 — Find your Course ID

Open your new sandbox course. Look at the URL:

```
https://csufullerton.instructure.com/courses/123456
                                             ^^^^^^
                                       this is your COURSE_ID
```

Write it down. You now have the **three values** you need.

---

# Step 5 — Create `canvas-config.txt`

Open a plain-text editor:

- **macOS:** TextEdit → Format menu → **Make Plain Text**
- **Windows:** **Notepad**

Type the three lines below, fill in **your** values, then save the file as **`canvas-config.txt`** inside your `canvas-workshop` folder.

```text
CANVAS_BASE_URL=https://csufullerton.instructure.com
CANVAS_TOKEN=paste_your_token_here
COURSE_ID=123456
```

<span class="small">Codex will read this file when you tell it to. No terminal, no environment variables.</span>

---

# Don't share or commit this file

`canvas-config.txt` contains your real Canvas token — treat it like the password it is.

- **Don't** email it.
- **Don't** drop it in a shared OneDrive / Google Drive folder.
- **Don't** commit it to GitHub.
- If you accidentally share it, **delete the token in Canvas immediately** and generate a new one.

---

<!-- _class: section -->

<span class="kicker">Part 4 · 10 minutes</span>

# Project setup
### Syllabus + agent instructions

---

# Convert `syllabus.docx` → `syllabus.txt`

**In Microsoft Word (works everywhere):**
1. Open your syllabus.
2. **File → Save As**.
3. File type: **Plain Text (.txt)**.
4. Save as `syllabus.txt` in `canvas-workshop`. Choose **UTF-8** if prompted.

**On macOS** you can also right-click the `.docx` in Finder → **Quick Actions → Convert to TXT**, then rename to `syllabus.txt` and move it into the folder.

Open the file in TextEdit / Notepad to spot-check that headings and the schedule survived the conversion.

---

# Teach Codex the Canvas API — `AGENTS.md`

Codex reads an `AGENTS.md` file from the project folder on startup. It's a plain-text file that tells the agent what Canvas endpoints to use, where to find the three Canvas values, and our rules (unpublished default, preserve policy wording, `(DATE NEEDED)` for missing dates).

**Easiest: download from the workshop repo in your browser**

1. Go to <https://github.com/dadams-AU/canvas-workshop>.
2. Click **AGENTS.md**.
3. Click the **Download raw file** button (the small download icon, top right of the file view).
4. Move the downloaded `AGENTS.md` into your `canvas-workshop` folder, next to `syllabus.txt` and `canvas-config.txt`.

---

# What's in your `canvas-workshop` folder now

By the end of Part 4 you should see **three files**:

```text
canvas-workshop/
  ├── canvas-config.txt   ← your three Canvas values
  ├── syllabus.txt        ← your plain-text syllabus
  └── AGENTS.md           ← agent instructions
```

That's everything Codex needs.

---

<!-- _class: section -->

<span class="kicker">Part 5 · 20 minutes · Live Demo</span>

# Connect → Build → Audit → Finalize

Five prompt cards. Slides are on GitHub so you can copy them after the session.

---

# Open the workshop folder in Codex

1. Launch **Codex**.
2. **File → Open Folder…** (mac) or **File → Open…** (win).
3. Select your **`canvas-workshop`** folder and open it.
4. You should see `canvas-config.txt`, `syllabus.txt`, and `AGENTS.md` listed in the file panel.

<div class="warn">
Codex must be opened on the folder that contains <code>syllabus.txt</code>, <code>canvas-config.txt</code>, and <code>AGENTS.md</code>. If the file panel is empty, you opened the wrong folder.
</div>

<div class="ok">
<strong>Pasting multi-line prompts:</strong> Press <strong>Shift + Return</strong> (mac) or <strong>Shift + Enter</strong> (win) to add a new line inside a prompt. Return / Enter on its own will submit.
</div>

---

# If you don't have `AGENTS.md` yet

If the download in Part 4 didn't work, paste this as your **first** prompt — Codex will write its own instructions:

```text
Create an AGENTS.md in this folder that tells you how to use the
Canvas LMS REST API. Read CANVAS_BASE_URL, CANVAS_TOKEN, and
COURSE_ID from canvas-config.txt in this folder. Include endpoints
for courses, modules, pages, assignments, and module items.

Include these rules:
- keep all assignments unpublished
- preserve syllabus policy language verbatim
- use "(DATE NEEDED)" for missing due dates
- never invent policies or grading categories
- the syllabus.txt file in this folder is the single source of truth

Then summarize what you wrote.
```

<span class="small">⚠️ If you already downloaded <code>AGENTS.md</code>, skip this slide and go straight to Card 1.</span>

---

# Card 1 — Connect

```text
Read canvas-config.txt to load CANVAS_BASE_URL, CANVAS_TOKEN, and
COURSE_ID. Connect to Canvas, verify the connection, and report
the course name before doing anything else.
```

**Expected:** Codex prints the course name from your sandbox and waits for your next instruction.

<div class="warn">
<span class="small">If it prints someone else's course name, your COURSE_ID is wrong. Stop and fix it.</span>
</div>

---

# Card 2 — Build from syllabus

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

---

# What Codex is actually doing

It's making a series of Canvas API calls:

```text
POST  /api/v1/courses/:id/pages            (landing page)
POST  /api/v1/courses/:id/modules          (weekly modules)
POST  /api/v1/courses/:id/pages            (module overviews)
POST  /api/v1/courses/:id/assignments      (each assignment)
POST  /api/v1/courses/:id/modules/:mid/items  (link to module)
```

Watch the action panel scroll by. Approve each one, or allow-list common safe ones.

---

# Card 3 — Audit

```text
Audit everything you just created and list:
1) missing due dates
2) weekend due dates
3) modules with no assignments
4) anything inconsistent with syllabus.txt

Propose fixes only. Do not apply yet.
```

Codex returns a **proposed diff** — no changes are made until you approve.

---

# Card 4 — Finalize

```text
Apply only the fixes we approved:
- [list the items you accepted]

Keep all assignments UNPUBLISHED.
Return a final manual-review checklist before I publish.
```

Codex now applies the subset you approved. Everything is still unpublished.

---

# Card 5 — Guardrails

- AI drafts; **faculty review** before publish.
- **Never paste tokens** into slides or chat.
- Validate **dates, points, policy language**.
- Build in **sandbox first**, then move to live course.
- **Audit** every AI action before finalizing.
- Use **syllabus text** as the single source of truth.

---

# Where Codex fails — and how we catch it

- **Hallucinated dates** — "Week 7: Oct 15" when syllabus said Oct 12.
  → Card 3 audit catches it.
- **Merged assignments** — two syllabus items collapsed into one.
  → Manual spot-check against syllabus TOC.
- **Policy drift** — softened late-work language.
  → Copy/paste compare your real policy before publish.
- **Missing prerequisites** — module items with no due dates.
  → Audit flags this.

---

<!-- _class: section -->

<span class="kicker">Part 6 · 10 minutes</span>

# Hands-on lab

---

# Try it now (10 min)

1. Open the `canvas-workshop` folder in Codex.
2. Paste **Card 1** (Connect). Confirm the course name.
3. Paste **Card 2** (Build). Approve actions as they come.
4. Paste **Card 3** (Audit). Read what it flags.
5. If you have time, paste **Card 4** with one fix you approved.

Use **Shift + Return/Enter** for newlines in multi-line prompts.

---

<!-- _class: section -->

<span class="kicker">Part 7 · 5 minutes</span>

# What to try next · checklist · resources

---

# What to try next

Once you're comfortable with the build → audit → finalize loop, extend it:

- **Quizzes** — "Create a 5-question low-stakes quiz from Week 3 readings, unpublished."
- **Rubrics** — "Generate a 4-criterion rubric for the midterm paper; attach it to that assignment."
- **Assignment groups + weights** — "Create groups matching my syllabus grading table; assign each item to a group."
- **Discussions** — "Create one weekly discussion topic with a grading stub."
- **Announcements** — "Draft (don't post) a Week 1 welcome announcement from the syllabus landing page."
- **Copy to live course** — use Canvas's **Import Course Content** from your sandbox.

---

# Pre-publish checklist

Before flipping anything from unpublished to published, confirm:

- [ ] Every assignment's **points** match the syllabus.
- [ ] Every assignment's **due date** matches the syllabus (no weekend drift).
- [ ] **Policy pages** (late work, academic integrity, accommodations) are copied verbatim from the syllabus.
- [ ] **Grading weights** on the Assignment Groups match the syllabus table.
- [ ] **Module order** matches the syllabus schedule.
- [ ] Nothing marked `(DATE NEEDED)` remains unresolved.
- [ ] Landing page has contact info + office hours.

---

# Resources

- **Workshop repo (slides, `AGENTS.md`, prompt cards, checklist):**
  <https://github.com/dadams-AU/canvas-workshop>
- **Codex desktop app (macOS + Windows):** <https://developers.openai.com/codex/quickstart?setup=app>
- **Canvas API docs:** <https://canvas.instructure.com/doc/api/>
- **Prefer the terminal?** The earlier CLI version of this workshop is in `command-line-instructions/` in the same repo.

---

# Contact + follow-up

**David P. Adams, PhD** · <dpadams@fullerton.edu>

What to send back:

- What you built (link or screenshot — with **tokens and course IDs redacted**).
- One improvement to the prompt cards you'd propose for the next cohort.
- One question the workshop didn't answer.

<div class="ok">
Thank you — and remember: sandbox first, audit always, publish last.
</div>
