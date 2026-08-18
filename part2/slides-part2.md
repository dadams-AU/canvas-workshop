---
marp: true
theme: default
paginate: true
title: From Shell to Course — Drafting Module Content, Rubrics, and Accessible Pages
author: David P. Adams, PhD
date: 2026
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

<span class="kicker">Faculty Development · Part 2 of 2 · 60 minutes · Zoom</span>

# From Shell to Course

## Drafting Module Content, Rubrics, and Accessible Pages

David P. Adams, PhD · <dpadams@fullerton.edu>

Materials: **[github.com/dadams-AU/canvas-workshop](https://github.com/dadams-AU/canvas-workshop)**

<!-- _footer: 'Part 1 is a prerequisite. Sandbox only. AI drafts; you verify. Nothing publishes during this workshop.' -->

---

# Where Part 1 stopped

Your sandbox holds a shell: weekly modules, assignment stubs with points and due dates, a landing page. Everything unpublished.

Open every module and it is empty. Open every assignment and the description is blank.

<div class="ok">
That shell took twenty minutes to build and it is the easy half. Today is the half where the agent needs something from you that the syllabus does not contain.
</div>

---

# Our one-hour plan

| Time | Segment |
|---|---|
| 0:00–0:04 | What changes in Part 2 |
| 0:04–0:10 | Setup check: one card, five minutes |
| 0:10–0:15 | Inputs, not prompts |
| 0:15–0:34 | Demonstration: connect, expand, draft |
| 0:34–0:44 | Try it in your own sandbox |
| 0:44–0:54 | The accessibility audit |
| 0:54–1:00 | Finalize, cleanup, what comes next |

---

# The guardrail that carried Part 1 will not carry Part 2

Part 1 ran on one rule: **do not invent**. It worked because the syllabus already held everything the shell needed. Week labels, points, due dates, policy language. The agent copied.

A module overview page is different. Learning objectives are not in most syllabi. Neither are assignment prompts in full, or rubric dimensions, or readings by week.

So "do not invent" now has two possible meanings, and only one of them is useful.

- **Refuse and stop.** Correct, and you get an empty course.
- **Draft from what you supply, and mark everything you composed.** Also correct, and you get a course.

---

# Five guardrails

- **Sandbox only**—never point today's workflow at a live section.
- **Unpublished by default**—nothing goes live during this session.
- **The sources are the source of truth**—missing information is flagged, not guessed.
- **Faculty review is the final gate**—the agent drafts; you decide.
- **Composed content is labeled as composed**—every drafted title carries `DRAFT — `, every gap carries `(INSTRUCTOR DRAFT NEEDED)`.

<div class="warn">
The fifth is new today, and it is the one that makes the other four survive contact with real content. An unlabeled draft is a failed run.
</div>

---

<!-- _class: section -->

<span class="kicker">Five minutes</span>

# Setup check

Everything you installed in Part 1 still counts. Two things changed.

---

# One new folder, one new token

**Extract `canvas-workshop-part2-starter.zip`.** It makes a folder called `canvas-workshop-part2` that is complete on its own. Nothing merges with your Part 1 folder and nothing gets replaced. **If Windows blocks the download, see the next slide.**

**Make a new Canvas token.** Account → Settings → **New Access Token**, shortest practical expiration. The Part 1 token was revoked at the end of that session and will not work.

**Point it at your Part 1 sandbox.** Copy `canvas-config-template.txt`, rename the copy `canvas-config.txt`, and fill in the URL, the new token, and that sandbox's course ID.

<span class="small">Your Part 1 folder and your sandbox course both stay exactly as they are.</span>

---

# If Windows blocks the download

This happened to several of you in Part 1, and it was our fault rather than yours. That ZIP was mostly one HTML file carrying 34 KB of minified JavaScript, which is the shape Defender is trained to stop.

**Today's ZIP is 16 KB of plain text.** No HTML, no scripts, nothing to scan.

**If it is still blocked, you do not need it.** Codex needs three text files. Open `AGENTS.md`, `syllabus-sample.txt`, and `course-materials-sample.txt` on GitHub, click **Raw**, and copy each into Notepad using **Save as type: All Files**. About four minutes.

<div class="warn">
Do not switch off Defender or SmartScreen, and do not ask IT for an exception for a workshop file. The full copy path is written out in <code>README-FIRST-PART2.txt</code>.
</div>

---

# Card 0 · Verify the setup

```text
Do not connect to Canvas yet.

1. List the files in this project folder.
2. Report the version line at the top of AGENTS.md.
3. Confirm that syllabus.txt and course-materials.txt are both present
   and not empty.
4. Confirm that canvas-config.txt exists and contains three settings,
   without displaying any of their values.

Report what is missing. Do nothing else.
```

**The version line must read Part 2.** That single check catches nearly every setup failure.

---

# If Card 0 reports a problem

| What it says | What happened | Fix |
|---|---|---|
| Version reads Part 1 | Your Part 1 folder is open | Cmd/Ctrl+O, select `canvas-workshop-part2` |
| Cannot list any files | No folder is open | Same |
| `course-materials.txt` missing | Same | Same |
| No `canvas-config.txt` | Step 3 not done yet | Copy the template, rename it, fill it in |
| Codex not in the dropdown | Signed in to a personal account | Switch to the ChatGPT Edu workspace |
| Nothing downloaded at all | Defender blocked the ZIP | Copy the three files, previous slide |

<div class="ok">
Nothing here touches Canvas. You can run Card 0 as many times as you need.
</div>

---

<!-- _class: section -->

<span class="kicker">The actual skill</span>

# Inputs, not prompts

---

# Two files, two jobs

**`syllabus.txt`** governs structure. Weeks, points, due dates, submission types, and every word of policy language. It won Part 1 and it still governs.

**`course-materials.txt`** carries what the syllabus leaves out. Module learning objectives, assignment prompts in full, readings by week, rubric dimensions with points.

Where the two disagree, the syllabus governs and the agent reports the disagreement rather than resolving it.

<span class="small">Today's <code>course-materials.txt</code> is fictional, and it is deliberately incomplete. Week 2 has no objectives, no prompt, and no rubric. Watch what the agent does with that.</span>

---

# The prompts barely changed. The inputs did.

Compare Card 2 today against Card 2 in Part 1. Nearly the same sentence.

What changed is that you now hand the agent a second file, and everything good in the output traces back to something you wrote in it.

<div class="warn">
An empty <code>course-materials.txt</code> and a brilliant prompt produce a course full of confident, plausible, invented learning objectives. There is no prompt that fixes a missing input.
</div>

The take-home task is not learning better prompts. It is assembling the file.

---

<!-- _class: section -->

<span class="kicker">Live demonstration</span>

# Connect → Expand → Draft → Audit → Finalize

---

# The five checkpoints

```text
CONNECT       Verify the sandbox; inventory what Part 1 left
    ↓
EXPAND        Propose a content manifest with sources cited
    ↓
DRAFT         Write only the approved manifest, unpublished, labeled
    ↓
AUDIT         Check accessibility and fidelity against the sources
    ↓
FINALIZE      Apply only explicitly approved corrections
```

Same shape as Part 1. **Preview became Expand**, and it now has to say where every sentence came from.

---

# Card 1 · Connect and inventory

```text
Use canvas-config.txt without displaying its values.

Connect to the one Canvas course in COURSE_ID using GET only. Report:
1. the course name
2. counts of modules, pages, assignments, discussions, and rubrics
3. which modules contain no items
4. which assignments have an empty description
5. which assignments have no rubric attached

Do not create or change anything. Never display CANVAS_TOKEN.
```

**Stop immediately** if the reported course is not your sandbox.

---

# Card 2 · Expand before writing

```text
Read syllabus.txt and course-materials.txt and propose a content
manifest. For each item, give:

- what you would write: module overview page, assignment description,
  rubric, or discussion prompt
- which source file and which passage supports it
- which parts have no source support and will carry
  (INSTRUCTOR DRAFT NEEDED)
- whether the item is new or an edit to something that already exists
- for a rubric: the dimensions, their points, and the total against
  that assignment's points_possible

Where the two source files disagree, report the disagreement instead
of resolving it. Do not make Canvas changes. Wait for my approval.
```

---

# Read the manifest, not the output

Two questions decide whether to approve:

- Is every `(INSTRUCTOR DRAFT NEEDED)` marker somewhere you agree the source is silent?
- Does every rubric total match its assignment's points?

Today's sample fails the second one on purpose. The Introduction post is worth **10** points in the syllabus and the dimensions in `course-materials.txt` sum to **12**.

<div class="ok">
The agent should stop and report that, not quietly rescale a dimension or edit the assignment. Instructors make this error constantly. It is worth knowing your tooling will catch it.
</div>

---

# Card 3 · Draft the approved content

```text
Write only the manifest I approved into my Canvas sandbox.

Read each existing page or assignment before editing it, change only
the field named in the manifest, and preserve everything else. Keep
every item UNPUBLISHED. Preserve syllabus policy wording verbatim.

Prefix every title you composed with "DRAFT — ". Insert
(INSTRUCTOR DRAFT NEEDED) wherever the sources are silent rather
than composing text to fill the gap.

Return counts, every marker you inserted with its location, and any
failed operations. Never display CANVAS_TOKEN.
```

---

# Editing is narrower than creating

Part 1 only created. Part 2 mostly edits, and a Canvas page update **replaces the entire body**.

- Read the existing item first.
- Change only the field named in the manifest.
- Never touch `name`, `points_possible`, or `due_at` while filling in a description.

<div class="warn">
Approve a network request only when the destination is your institution's Canvas hostname, the course ID is your verified sandbox, and the action appears in the manifest you approved. Nothing should say <strong>publish</strong> or <strong>delete</strong>.
</div>

---

# What a labeled draft looks like in Canvas

```text
Week 1 — Getting Started                    (from your objectives)
Week 2 — Building a Plan
    DRAFT — Week 2 Overview
    Objectives: (INSTRUCTOR DRAFT NEEDED)
    Weekly planning reflection (DATE NEEDED)
        description: (INSTRUCTOR DRAFT NEEDED)
Week 3 — Committing to Action               (from your objectives)
```

Week 2 is empty because your materials are empty there. That is the system working.

<span class="small">A course that cannot show you where it is thin is worse than one that is thin.</span>

---

<!-- _class: section -->

<span class="kicker">Ten-minute follow-along</span>

# Try it in your sandbox

1. Run **Card 0**, then **Card 1**, and verify your course name.
2. Run **Card 2** and read the manifest against the sample materials.
3. If the manifest looks right and time remains, approve it and run **Card 3**.

<div class="warn">
If your setup is incomplete, keep watching. Do not rush a token or an approval decision to keep pace with the group.
</div>

---

<!-- _class: section -->

<span class="kicker">Ten minutes</span>

# The accessibility audit

Everything the agent wrote is new HTML in your course. All of it is your responsibility.

---

# Card 4 · Audit without changing

```text
Compare the Canvas items with syllabus.txt, course-materials.txt, and
the approved manifest. Report, without changing anything:

1. accessibility failures against the rules in AGENTS.md, quoting the
   offending markup for each: heading level, list markup, link text,
   table headers and caption, color and inline style, alt text
2. any image with missing or placeholder alt text
3. content in Canvas that no source passage supports
4. composed content that is not labeled
5. policy language that drifted from the syllabus
6. rubric totals that no longer match assignment points
7. duplicates, incorrect module placement, and failed operations

Propose fixes only. Do not apply them yet.
```

---

# What an automated pass finds, and what it cannot

| Caught by a checker | Left to you |
|---|---|
| Missing `alt` attribute | `alt` that is present and wrong |
| Skipped heading level | Headings that are valid and meaningless |
| Empty link text | Link text that reads well, points elsewhere |
| Table without headers | A table that should have been a list |
| Contrast below 4.5:1 | Whether the page is understandable |

Canvas ships an accessibility checker in its rich content editor. It sits in the left column. Run it too—it catches a different set of things than the agent does.

<span class="small">The standard is WCAG 2.1 Level AA, which is what the CSU Accessible Technology Initiative and Section 508 both point at.</span>

---

# Alt text is the one to watch

**The agent cannot see the images in your course.** It has the file name and nothing else.

Ask it for alt text and it will produce a fluent, specific, confident description of a photograph it has never seen. That description will pass every automated check ever written.

<div class="warn">
Today's <code>AGENTS.md</code> forbids it: alt text only for an image described in your source files, and <code>(ALT TEXT NEEDED)</code> for everything else. The sample materials mention a photograph that was never uploaded. Watch that flag fire.
</div>

Alt text is written by whoever looked at the image. That is you.

---

# Card 5 · Finalize approved corrections

```text
Apply only these corrections that I explicitly approved:
- [paste the approved items here]

Keep everything UNPUBLISHED. Do not change any other item. Do not
remove any DRAFT — prefix or (INSTRUCTOR DRAFT NEEDED) marker unless
I listed it above.

Return a final manual-review checklist and report any failures.
```

**Finalize means complete the draft—not publish the course.**

---

# Before this course meets a student

- Every `DRAFT — ` prefix resolved or deliberately kept.
- Every `(INSTRUCTOR DRAFT NEEDED)`, `(DATE NEEDED)`, and `(ALT TEXT NEEDED)` marker resolved.
- Every rubric attached to the right assignment, totals matching.
- You have decided whether rubrics calculate grades. The default we set is no.
- Objectives, prompts, and readings read as yours, because they came from your file.

<span class="small">The full checklist is in <code>PROMPT-CARDS-2.md</code> and it outlives the workshop.</span>

---

# Clean up before leaving Zoom

1. Confirm the sandbox course is still **unpublished**.
2. Revoke the temporary token in Canvas.
3. Delete `canvas-config.txt` from the workshop folder.
4. Keep the prompt cards, the instructions, and both sample files.

<div class="ok">
Sandbox first. Cite the source before writing. Label what was composed. Audit every result. Publish only after a separate manual review.
</div>

---

# What is left, and it is not small

Publishing is a separate decision and a separate workflow: availability dates, section-differentiated due dates, staged release module by module, and the term rollover that copies a shell forward and diffs it against next year's syllabus.

None of that happened today, deliberately. Everything in your sandbox is still unpublished.

<span class="small">Tell the Faculty Development Center if a third session on publishing and rollover would be useful to you.</span>

---

# Resources + follow-up

- **Workshop files:** <https://github.com/dadams-AU/canvas-workshop>
- **Copyable prompts:** open **`PROMPT-CARDS-2.md`** on GitHub, where every prompt has a copy button
- **Canvas API documentation:** <https://canvas.instructure.com/doc/api/>
- **WCAG 2.1 Level AA:** <https://www.w3.org/WAI/WCAG21/quickref/>

David P. Adams, PhD · <dpadams@fullerton.edu>

<span class="small">Next step: replace both sample files with your own syllabus and your own objectives, prompts, readings, and rubric dimensions. The second file is the assignment.</span>
