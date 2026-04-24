---
marp: true
theme: default
paginate: true
title: Syllabus → Canvas AI Workshop
author: David P. Adams, PhD
date: 2026-04-23
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

<span class="kicker">Faculty Development Workshop · 90 minutes</span>

# Syllabus → Canvas, with an AI Agent

**Turn a plain-text syllabus into a scaffolded Canvas course — modules, assignments, due dates, landing page — in one session.**

David P. Adams, PhD · <dpadams@fullerton.edu>

Slides + resources: **github.com/dadams-AU/canvas-workshop**

<!-- _footer: 'Sandbox only. No programming experience required. AI drafts; you verify; nothing publishes until you audit.' -->

---

# Who this workshop is for

- Faculty who want a **faster starting point** for a Canvas shell.
- You do **not** need to have used a terminal before.
- You do **not** need to have used Canvas's API before.
- You do **not** need to be a programmer.

<div class="warn">
<strong>Account note:</strong> CSUF-managed Google accounts block the Gemini CLI. Our OpenAI EDU accounts do work with <strong>Codex</strong>, so that's what we'll use today.
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
| 0:05 – 0:15 | Concept primer (CLI, agent, API token) |
| 0:15 – 0:30 | **Install** Node.js + Codex |
| 0:30 – 0:45 | **Canvas:** sandbox → token → course ID → env file |
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

Four words you'll hear all day: **terminal**, **agent**, **API token**, **sandbox**.

---

# What is a terminal / CLI?

- A **terminal** (macOS: Terminal; Windows: PowerShell) is a text window that runs commands.
- **CLI** = Command-Line Interface. Same idea: you type, it runs.
- Today we use it only to:
  1. Check that things are installed (`node --version`)
  2. Set three environment variables (your Canvas URL, token, course ID)
  3. Launch Codex

<span class="small">If you've copied a curl command from an email before — you've used a terminal.</span>

---

# What is an AI agent?

- A **chatbot** answers questions in a browser tab.
- An **agent** can **take actions** on your behalf: read files, make API calls, create things in Canvas.
- You approve each action it wants to take (or set auto-approve for safe ones).

> Think: a very fast teaching assistant who asks permission before touching anything.

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

# Codex — two ways to run it

<div class="two-col">

**Codex CLI (any OS)**

Runs in Terminal (mac) or PowerShell (win). Installed via `npm`. Authenticated with your OpenAI EDU account.

**Codex Mac app (macOS only)**

A regular desktop window. Same engine, no terminal required to interact. Good if typing in Terminal feels intimidating.

</div>

Pick whichever you prefer. Same prompt cards work in both.

---

<!-- _class: section -->

<span class="kicker">Part 2 · 15 minutes</span>

# Install software
### Node.js + Codex

---

# macOS — Install Homebrew

If you don't already have Homebrew, paste this into **Terminal** (one line, then press Return):

```bash
/bin/bash -c "$(curl -fsSL \
  https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then (Apple Silicon):

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
brew --version
```

<span class="small">Already have Homebrew? Skip this slide.</span>

---

# macOS — Install Node.js

```bash
brew install node
node --version
npm --version
```

You should see a version number for each. If you see "command not found," close the terminal and open a new window, then re-run.

---

# macOS — Install Codex

**Codex CLI**
```bash
brew install --cask codex || npm install -g @openai/codex
codex --version
```

**Or Codex Mac app:** download from <https://developers.openai.com/codex>, drag to `/Applications`, launch, sign in with your OpenAI EDU account.

---

# Windows — Install Node.js

Open **PowerShell** (not Command Prompt).

```powershell
winget install --id OpenJS.NodeJS.LTS -e
```

Close PowerShell, open a fresh PowerShell window, then:

```powershell
node --version
npm --version
```

<span class="small">If <code>winget</code> isn't recognized, install "App Installer" from the Microsoft Store and try again.</span>

---

# Windows — Install Codex CLI

```powershell
npm install -g @openai/codex
codex --version
```

Then sign in with your OpenAI EDU account when prompted.

<span class="small">Windows does not have the Codex desktop app — use the CLI.</span>

---

# Verify everything

Run these. You should see version numbers for all three:

```bash
node --version
npm --version
codex --version
```

If `codex --version` fails, close the terminal window, open a new one, and try again.

---

# Common install failures

| Symptom | Fix |
|---|---|
| `command not found` after install | Close terminal, open a new one |
| `EACCES` / permission error on `npm -g` | On macOS, prepend `sudo` once, or use `nvm` |
| `winget` not recognized | Install **App Installer** from Microsoft Store |
| Corporate laptop blocks install | Use a personal account / personal device |
| `401 Unauthorized` later | Token invalid or expired — regenerate |

---

# Create your workshop folder

Do this now — we'll put everything in it.

**macOS / Linux**
```bash
mkdir -p ~/canvas-workshop
cd ~/canvas-workshop
```

**Windows PowerShell**
```powershell
mkdir $HOME\canvas-workshop
cd $HOME\canvas-workshop
```

Leave this terminal window open. We'll come back to it after the Canvas side.

---

<!-- _class: section -->

<span class="kicker">Part 3 · 15 minutes</span>

# Canvas side
### Sandbox course → API token → course ID → env file

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

We'll paste the token one more time — into a local file on your own machine — in two slides.

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

# Step 5 — Save a reusable `canvas-env.txt`

Open a plain-text editor:

- **macOS:** TextEdit → Format menu → **Make Plain Text**
- **Windows:** **Notepad**

Paste the block that matches your OS (next slide), fill in your values, save the file as **`canvas-env.txt`** in your `canvas-workshop` folder.

<span class="small">Why save it? Environment variables don't persist across terminal sessions. Having this file lets you paste the three lines back in next time.</span>

---

# `canvas-env.txt` contents

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

Save. Close. Don't share this file.

---

# Step 6 — Set env vars in this terminal session

In the terminal window you already had open in `canvas-workshop`: open `canvas-env.txt`, copy its lines, paste into the terminal, press Return.

Verify they stuck (don't echo the token on a shared screen):

**macOS / Linux**
```bash
echo $CANVAS_BASE_URL
echo $COURSE_ID
```

**Windows PowerShell**
```powershell
echo $env:CANVAS_BASE_URL
echo $env:COURSE_ID
```

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

**macOS Terminal shortcut:**
```bash
textutil -convert txt "syllabus.docx" -output "syllabus.txt"
```

Quick look:
```bash
wc -l syllabus.txt
head -40 syllabus.txt
```

---

# Teach Codex the Canvas API — `AGENTS.md`

Codex reads an `AGENTS.md` file from the project folder on startup. We'll drop one in with Canvas endpoints and our rules (unpublished default, preserve policy wording, `(DATE NEEDED)` for missing dates).

**Easiest: download from the workshop repo**

```bash
curl -o AGENTS.md \
  https://raw.githubusercontent.com/dadams-AU/canvas-workshop/main/AGENTS.md
```

**Windows PowerShell:**
```powershell
curl.exe -o AGENTS.md `
  https://raw.githubusercontent.com/dadams-AU/canvas-workshop/main/AGENTS.md
```

---

<!-- _class: section -->

<span class="kicker">Part 5 · 20 minutes · Live Demo</span>

# Connect → Build → Audit → Finalize

Five prompt cards. Slides are on GitHub so you can copy them after the session.

---

# Open Codex in the workshop folder

**Codex CLI:** `cd` into `canvas-workshop` first, then:

```bash
codex
```

**Codex Mac app:** File → Open → select the `canvas-workshop` folder.

<div class="warn">
Codex must be launched <em>inside the folder that contains</em> <code>syllabus.txt</code> and <code>AGENTS.md</code>. Otherwise it can't read them.
</div>

<div class="ok">
<strong>Pasting multi-line prompts:</strong> Press <strong>Shift + Return</strong> (mac) or <strong>Shift + Enter</strong> (win) to add a new line inside a prompt. Return / Enter on its own will submit.
</div>

---

# If you don't have `AGENTS.md` yet

If the `curl` download in Part 4 didn't work, paste this as your **first** prompt — Codex will write its own instructions:

```text
Create an AGENTS.md in this folder that tells you how to use the
Canvas LMS REST API at $CANVAS_BASE_URL with bearer token
$CANVAS_TOKEN. Include endpoints for courses, modules, pages,
assignments, and module items.

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
Connect to Canvas using CANVAS_BASE_URL, CANVAS_TOKEN, and COURSE_ID.
Verify connection and report the course name before doing anything else.
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

Watch the tool-use lines scroll by. Approve each one, or allow-list common safe ones.

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

1. Launch Codex in the `canvas-workshop` folder.
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
- **Canvas API docs:** <https://canvas.instructure.com/doc/api/>
- **Node.js (LTS):** <https://nodejs.org/en/download>
- **Codex CLI:** <https://developers.openai.com/codex/cli>
- **Codex Mac app:** <https://developers.openai.com/codex>
- **Homebrew (macOS):** <https://brew.sh>

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
