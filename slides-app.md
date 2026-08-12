---
marp: true
theme: default
paginate: true
title: From Syllabus to Canvas — Building Your Course Shell with an AI Agent
author: David P. Adams, PhD
date: August 18, 2026
style: |
  section { font-size: 28px; }
  section h1 { font-size: 44px; }
  section h2 { font-size: 34px; }
  code { font-size: 22px; }
  pre { font-size: 19px; line-height: 1.32; }
  table { font-size: 23px; }
  .small { font-size: 20px; color: #475569; }
  .kicker { font-size: 18px; letter-spacing: .08em; text-transform: uppercase; color: #0e7490; }
  .warn { background: #fef3c7; border-left: 5px solid #b45309; padding: 10px 14px; border-radius: 6px; }
  .ok { background: #ecfdf5; border-left: 5px solid #047857; padding: 10px 14px; border-radius: 6px; }
  .section { background: #0f172a; color: #f8fafc; }
  .section h1 { color: #f8fafc; }
---

<!-- _class: section -->

<span class="kicker">Faculty Development · Tuesday, August 18 · 1:00–2:00 pm · Zoom</span>

# From Syllabus to Canvas

## Building Your Course Shell with an AI Agent

David P. Adams, PhD · <dpadams@fullerton.edu>

Materials: **[github.com/dadams-AU/canvas-workshop](https://github.com/dadams-AU/canvas-workshop)**

<!-- _footer: 'Sandbox only. AI drafts; you verify. Nothing publishes during this workshop.' -->

---

# What you will see—and try

- A complete demonstration: **connect → preview → build → audit → finalize**.
- Time to try the safe first steps in your own Canvas sandbox.
- Five prompt cards and a pre-publish checklist to keep.

<div class="ok">
No programming, command line, Git, or GitHub account is required. We use GitHub only as a download page.
</div>

Download **`slides-app.html`** for a browser version that makes the prompt-card text easy to copy and paste.

<span class="small">If setup is blocked on your device, follow the demonstration and use the same materials later.</span>

---

# Our one-hour plan

| Time | Segment |
|---|---|
| 0:00–0:05 | Outcome + guardrails |
| 0:05–0:18 | Setup sprint: download, app, sandbox, token |
| 0:18–0:23 | Open the project safely |
| 0:23–0:40 | Complete live demonstration |
| 0:40–0:52 | Try it in your own sandbox |
| 0:52–1:00 | Manual review, cleanup, resources |

---

# Four guardrails

- **Sandbox only**—never point today’s workflow at a live section.
- **Unpublished by default**—nothing goes live during this session.
- **Syllabus is the source of truth**—missing information is flagged, not guessed.
- **Faculty review is the final gate**—the agent drafts; you decide.

<div class="warn">
Never show a Canvas token in chat, email, Zoom, slides, or screenshots.
</div>

---

<!-- _class: section -->

<span class="kicker">13-minute setup sprint</span>

# Get one folder ready

You may follow along—or simply watch if your device blocks a step.

---

# 1 · Download the starter ZIP

1. Go to **[github.com/dadams-AU/canvas-workshop](https://github.com/dadams-AU/canvas-workshop)**.
2. Click **`canvas-workshop-starter.zip`**.
3. Click the **download** button.
4. Double-click the downloaded ZIP to extract it.
5. Open the new **`canvas-workshop`** folder.

```text
AGENTS.md                  safety + Canvas instructions
PROMPT-CARDS.md            today's five prompts
README-FIRST.txt           take-home instructions
slides-app.html            copyable browser slides
canvas-config-template.txt blank Canvas settings
syllabus.txt               short fictional practice syllabus
```

---

# 2 · Install the desktop app

1. Open **<https://learn.chatgpt.com/docs/quickstart?setup=app>**.
2. Download the **ChatGPT desktop app** for macOS or Windows.
3. Follow the normal installation prompts.
4. Sign in. A university-managed **ChatGPT Edu** account is preferred.
5. Confirm that **Codex** appears in the ChatGPT dropdown.

<div class="warn">
Work only in a Canvas sandbox with the fictional syllabus today. If installation or account access is blocked, watch the demonstration—do not bypass university controls.
</div>

---

# 3 · Create a Canvas sandbox + token

**Sandbox course**

Canvas → Courses → All Courses → **Start a New Course**

Name it `SANDBOX — Your Name — AI Workshop`. Keep it unpublished.

**Temporary token**

Canvas → Account → Settings → **New Access Token**

Use the shortest practical expiration and copy the token once.

<span class="small">A Canvas token acts with your permissions. Today it should reach only your empty sandbox.</span>

---

# 4 · Complete the two local files

Rename `canvas-config-template.txt` to **`canvas-config.txt`** and fill in:

```text
CANVAS_BASE_URL=https://csufullerton.instructure.com
CANVAS_TOKEN=paste_your_temporary_token_here
COURSE_ID=123456
```

The starter already includes a fictional **`syllabus.txt`** for today’s practice.

<div class="warn">
Keep <code>canvas-config.txt</code> on your computer. Do not upload it to GitHub, cloud storage, email, or Zoom chat.
</div>

---

# 5 · Open the folder safely

1. Open the **ChatGPT desktop app**.
2. Select **Codex** from the ChatGPT dropdown.
3. Press **Cmd/Ctrl+O**, or choose **Add/Open project**.
4. Select the extracted **`canvas-workshop`** folder.
5. Start a **new chat** in that local project.
6. Beneath the message box, select **Ask for approval**.

<span class="small">Codex automatically discovers <code>AGENTS.md</code> from the project folder.</span>

---

<!-- _class: section -->

<span class="kicker">Live demonstration</span>

# Connect → Preview → Build → Audit → Finalize

---

# Card 1 · Connect safely

```text
Use canvas-config.txt without displaying its values.

1. Confirm this project contains syllabus.txt and AGENTS.md.
2. Connect to the one Canvas course in COURSE_ID using GET only.
3. Report the course name and the current counts of modules,
   pages, and assignments.

Do not create or change anything. Never display CANVAS_TOKEN.
```

**Stop immediately** if the reported course is not your sandbox.

---

# The five checkpoints

```text
CONNECT       Confirm the correct sandbox; make no changes
    ↓
PREVIEW       Turn the syllabus into a proposed manifest
    ↓
BUILD         Create only the approved manifest, unpublished
    ↓
AUDIT         Compare Canvas with the syllabus
    ↓
FINALIZE      Apply only explicitly approved corrections
```

---

# Card 2 · Preview before writing

```text
Read syllabus.txt and propose a manifest of everything you would
create: landing page, weekly modules, overview pages, assignments,
points, due dates, and module placement.

Use the syllabus week labels verbatim, including any exam or break
weeks. Flag missing or ambiguous information; do not guess.

Do not make Canvas changes. Wait for my approval.
```

---

# Pause and compare

Before approving the manifest:

- Are all syllabus weeks present and in order?
- Is every assignment represented exactly once?
- Are points and dates supported by the syllabus?
- Is missing information clearly flagged?
- Has any policy wording been changed?

<div class="ok">
This is the safest time to catch a mistake: nothing has been written to Canvas.
</div>

---

# Card 3 · Build the approved manifest

```text
Build only the manifest I approved in my Canvas sandbox.

Before creating anything, stop if an existing Canvas item has the
same title. Keep every page, module, assignment, and module item
UNPUBLISHED. Preserve syllabus policy wording verbatim.

Return counts, items needing review, and any failed operations.
Never display CANVAS_TOKEN.
```

---

# Read every approval request

Before selecting **Allow**, check:

- The destination is your institution’s Canvas hostname.
- The course ID is the sandbox you verified.
- The action matches the approved manifest.
- Nothing says **publish**, **delete**, or names another course.

<div class="warn">
Full access is not needed. You may deny an action, stop the run, or ask Codex to explain it.
</div>

---

# Card 4 · Audit without changing

```text
Compare the Canvas items with syllabus.txt and the approved manifest.
List:
1. missing or ambiguous dates and points
2. duplicate or missing assignments
3. incorrect module order or placement
4. altered policy wording
5. incomplete or failed operations

Propose fixes only. Do not apply them yet.
```

---

# Card 5 · Finalize approved corrections

```text
Apply only these corrections that I explicitly approved:
- [paste the approved items here]

Keep everything UNPUBLISHED. Do not change any other item.
Return a final manual-review checklist and report any failures.
```

**Finalize means complete the draft—not publish the course.**

---

<!-- _class: section -->

<span class="kicker">12-minute follow-along</span>

# Try it in your sandbox

1. Paste **Card 1** and verify the sandbox course name.
2. Paste **Card 2** and inspect the proposed manifest.
3. If the manifest is correct and time remains, approve it and paste **Card 3**.

<div class="warn">
If setup is incomplete, keep watching. Do not rush a token or approval decision to keep pace with the group.
</div>

---

# Check Canvas with your own eyes

Before publishing on another day, verify:

- Assignment names, points, dates, and submission types.
- Module names, sequence, and assignment placement.
- Policy language against the original syllabus.
- Grading weights, if the syllabus specifies them.
- Every `(DATE NEEDED)` flag is resolved.
- Pages, modules, assignments, and module items are unpublished.

If a run stopped midway, **inventory first**—never rerun the whole build blindly.

---

# Clean up before leaving Zoom

1. Confirm the sandbox course is still **unpublished**.
2. Revoke the temporary token in Canvas.
3. Delete `canvas-config.txt` from the workshop folder.
4. Keep the prompt cards, instructions, and sample syllabus.

<div class="ok">
Sandbox first. Preview before writing. Audit every result. Publish only after a separate manual review.
</div>

---

# Resources + follow-up

- **Workshop files:** <https://github.com/dadams-AU/canvas-workshop>
- **Copyable slides:** download **`slides-app.html`**, then open it in your browser
- **Prompt cards only:** open **`PROMPT-CARDS.md`** from the starter folder
- **Desktop app:** <https://learn.chatgpt.com/docs/quickstart?setup=app>
- **Canvas API documentation:** <https://canvas.instructure.com/doc/api/>

David P. Adams, PhD · <dpadams@fullerton.edu>

<span class="small">Next step: repeat the workflow in a fresh sandbox with your own syllabus. Keep the sample until that second run succeeds.</span>
