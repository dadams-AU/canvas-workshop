# From Syllabus to Canvas with Codex

Materials for a two-part faculty workshop series on using **Codex in the ChatGPT desktop app** to draft a Canvas course.

| | Session | What it does |
|---|---|---|
| **Part 1** | *From Syllabus to Canvas: Building Your Course Shell with an AI Agent* | Turns a plain-text syllabus into an unpublished shell: weekly modules, assignment stubs, points, due dates, landing page. Delivered April 24 and August 18, 2026. |
| **Part 2** | *From Shell to Course: Drafting Module Content, Rubrics, and Accessible Pages* | Fills that shell: module overview pages, assignment descriptions, rubrics, and accessible HTML, drafted from the instructor's own materials. Part 1 is a prerequisite. |

Part 1 materials are in the repository root. Part 2 materials are in [`part2/`](part2/).

**Audience:** Faculty with no programming, terminal, Git, GitHub, or Canvas API experience.

**Standard:** AI drafts. The instructor verifies. Nothing is published during the workshop.

## Start here during the Zoom

You do not need Git or a GitHub account. This page is only a place to download one file.

1. Click **`canvas-workshop-starter.zip`** in the file list above.
2. Click the download button on the next page.
3. Double-click the downloaded ZIP to extract it.
4. Open `README-FIRST.txt` inside the new `canvas-workshop` folder.

The ZIP contains a fictional practice syllabus, a blank configuration template, the prompt cards, and safety instructions. Every file in it is plain text. It never contains a real Canvas token.

To copy a prompt, open `PROMPT-CARDS.md` on GitHub, where each fenced block has a copy button. No download is needed for that.

## Distribution, and why the ZIPs are plain text only

At the August 18, 2026 session, several participants on managed Windows machines could not download the starter ZIP. Windows Defender blocked it.

The cause was in the artifact rather than in their configuration. Both ZIPs shipped `slides-app.html`, a self-contained Marp export carrying about 34 KB of minified JavaScript in two inline `<script>` blocks. That file was 85 percent of the archive by size. **An archive whose bulk is script-bearing HTML is the signature shape of HTML smuggling**, which is what Defender heuristics, SmartScreen download reputation, and Defender for Endpoint attack-surface-reduction rules are tuned to stop. On a managed device the block may not be overridable by the user, and it should not be overridden.

Three changes follow from that.

1. **Neither starter ZIP contains HTML.** Part 1 went from 174 KB to 8 KB, Part 2 from 208 KB to 16 KB. Every entry is now plain text: Markdown, `.txt`, and a `.gitignore`.
2. **The slides are a separate, optional download.** `slides-app.html` and `part2/slides-part2.html` stay in the repository for anyone who wants them, and neither is needed to complete the workshop. The prompt cards carry the same copyable text and render with copy buttons on GitHub.
3. **Both `README-FIRST` files document a no-download path.** Codex needs three plain-text files in a folder. A participant can view each on GitHub, click **Raw**, and save it out of Notepad with *Save as type: All Files*. That takes about four minutes and works when every download is blocked.

Participants are told explicitly not to disable Defender or SmartScreen and not to request an IT exception for a workshop file.

**Hosting the ZIP on a campus-trusted channel** — Canvas Files in an FDC or self-enroll course, or a OneDrive share from a `fullerton.edu` account — removes the SmartScreen reputation problem entirely, because the download no longer comes from an unfamiliar host. GitHub then serves as the public secondary copy. That is the durable fix and it is not yet done.

## Account

A university-managed **ChatGPT Edu** account is preferred. During the live session, participants should use only the fictional syllabus and an empty Canvas sandbox—never student records or other confidential data. Anyone without access to Codex can watch the demonstration and use the materials later.

## What is in this repository

| Path | Purpose |
|---|---|
| `canvas-workshop-starter.zip` | One-download participant bundle |
| `slides-app.pdf` | Current 60-minute presentation |
| `slides-app.md` / `slides-app.html` | Marp source and browser version. **Not in the ZIP** |
| `AGENTS.md` | Canvas API workflow and agent guardrails |
| `PROMPT-CARDS.md` | Five prompts and manual-review checklist |
| `README-FIRST.txt` | Plain-language participant setup |
| `canvas-config-template.txt` | Blank template for Canvas URL, token, and course ID |
| `syllabus-sample.txt` | Fictional syllabus included in the starter ZIP as `syllabus.txt` |
| `command-line-instructions/` | Archived CLI version for experienced users |
| `canvas-workshop-part2-starter.zip` | Self-contained Part 2 participant bundle |
| `part2/slides-part2.pdf` | Part 2 presentation |
| `part2/slides-part2.md` / `.html` | Marp source and browser version. **Not in the ZIP** |
| `part2/AGENTS.md` | Part 2 guardrails: a superset of the Part 1 file |
| `part2/PROMPT-CARDS-2.md` | Cards 0 through 5 and the Part 2 review checklist |
| `part2/README-FIRST-PART2.txt` | Plain-language Part 2 setup |
| `part2/course-materials-sample.txt` | Fictional supplementary materials, included in the Part 2 ZIP as `course-materials.txt` |

## The five-checkpoint workflow

1. **Connect:** Verify the one sandbox course using read-only requests.
2. **Preview:** Produce a proposed manifest from `syllabus.txt`; make no Canvas changes.
3. **Build:** Create only the instructor-approved manifest, unpublished.
4. **Audit:** Compare Canvas with the syllabus and propose corrections.
5. **Finalize:** Apply only explicitly approved corrections; keep everything unpublished.

The copy-and-paste prompts are in [PROMPT-CARDS.md](PROMPT-CARDS.md).

## Part 2 — From Shell to Course

Part 2 assumes the participant still has the sandbox they built in Part 1. Its bundle is deliberately **self-contained rather than an add-on**: extracting it produces a complete `canvas-workshop-part2` folder, so no participant has to merge two archives or approve a file replacement. Setup is a new Canvas token and a course ID.

### What changes

Part 1 ran on a single rule, *do not invent*, and it worked because the syllabus already carried everything the shell needed. Module overview pages, assignment prompts, and rubric dimensions are not in most syllabi, so Part 2 adds a second source file and a fifth guardrail.

- `syllabus.txt` still governs structure, dates, points, and policy wording.
- `course-materials.txt` carries learning objectives, full assignment prompts, readings, and rubric dimensions.
- Composed content is labeled: `DRAFT — ` on any title the agent wrote, `(INSTRUCTOR DRAFT NEEDED)` wherever the sources are silent, `(ALT TEXT NEEDED)` for any image the agent has not seen.

### The Part 2 workflow

0. **Verify:** confirm the folder, files, and `AGENTS.md` version without touching Canvas.
1. **Connect:** verify the sandbox and inventory what Part 1 left, including empty modules and blank descriptions.
2. **Expand:** propose a content manifest that cites a source passage for every item.
3. **Draft:** write only the approved manifest, unpublished and labeled, editing narrowly.
4. **Audit:** check accessibility against WCAG 2.1 AA and fidelity against both source files.
5. **Finalize:** apply only explicitly approved corrections.

The prompts are in [part2/PROMPT-CARDS-2.md](part2/PROMPT-CARDS-2.md).

### Two deliberate traps in the sample materials

The fictional `course-materials.txt` is incomplete on purpose, and the demonstration depends on both gaps firing.

- **Week 2 is empty.** No objectives, no assignment prompt, no rubric dimensions, and the syllabus already leaves that week's due date unspecified. The agent should produce visible markers rather than plausible filler.
- **The Introduction post does not add up.** The syllabus says 10 points; the rubric dimensions sum to 12. The agent should stop and report the discrepancy rather than rescaling a dimension or editing the assignment.

### Part 2 run of show

- **0:00–0:04:** What changes in Part 2
- **0:04–0:10:** Setup check, Card 0
- **0:10–0:15:** Inputs, not prompts
- **0:15–0:34:** Demonstration, Cards 1 through 3
- **0:34–0:44:** Participant follow-along in sandbox
- **0:44–0:54:** The accessibility audit, Card 4
- **0:54–1:00:** Finalize, cleanup, what comes next

Publishing, availability dates, section-differentiated due dates, and term rollover are all out of scope by design. Everything stays unpublished.

## Security design

The workshop deliberately uses an approachable text file for Canvas settings. Safeguards include:

- Use a temporary Canvas token with the shortest practical expiration.
- A university-managed ChatGPT Edu account is preferred.
- Use only the fictional syllabus during the workshop—never student records or other confidential data.
- Keep `canvas-config.txt` only on the participant's computer.
- Never display the token in chat, output, screenshots, or Zoom.
- Approve network access only to the institution's Canvas hostname.
- Verify the sandbox course name before any write request.
- Stop on duplicate-title conflicts rather than creating duplicates.
- Revoke the token and delete `canvas-config.txt` before leaving Zoom.
- Keep all Canvas objects unpublished until a separate manual review.

The included `.gitignore` is only an extra safeguard; participants do not need to understand or use Git.

## Facilitator run of show

- **0:00–0:05:** Outcome and guardrails
- **0:05–0:18:** Live setup sprint
- **0:18–0:23:** Open the local project and select Ask for approval
- **0:23–0:40:** Complete five-card demonstration
- **0:40–0:52:** Participant follow-along in sandbox
- **0:52–1:00:** Manual review, token cleanup, resources

Some managed computers will block installation or token creation. Those participants should watch the complete demonstration and use the same materials later; they should never bypass a device or campus security warning to keep pace.

## Facilitator preparation

1. Test the ZIP download using a logged-out browser window.
2. Test the complete workflow in a fresh sandbox.
3. Confirm the institution's ChatGPT Edu workspace exposes Codex.
4. Confirm Canvas allows faculty to create sandbox courses and personal access tokens.
5. Keep a completed private demo folder ready; never screen-share its token.
6. Put the repository link in Zoom chat as soon as the session opens.

## Rebuilding the starter ZIPs

Rebuild an archive whenever any file inside it changes.

`canvas-workshop-starter.zip` extracts to a `canvas-workshop/` folder containing `AGENTS.md`, `PROMPT-CARDS.md`, `README-FIRST.txt`, `canvas-config-template.txt`, `.gitignore`, and `syllabus-sample.txt` renamed to `syllabus.txt`.

`canvas-workshop-part2-starter.zip` extracts to a `canvas-workshop-part2/` folder containing `part2/AGENTS.md`, `part2/PROMPT-CARDS-2.md`, `PROMPT-CARDS.md`, `part2/README-FIRST-PART2.txt`, `canvas-config-template.txt`, `.gitignore`, `syllabus-sample.txt` renamed to `syllabus.txt`, and `part2/course-materials-sample.txt` renamed to `course-materials.txt`.

**Keep the HTML slides out of both archives.** Including `slides-app.html` or `slides-part2.html` is what got the ZIP blocked by Windows Defender in August 2026. Every entry in both archives should be Markdown or plain text. After rebuilding, confirm it:

```bash
unzip -p canvas-workshop-part2-starter.zip '*' | grep -c '<script'   # expect 0
unzip -l canvas-workshop-part2-starter.zip | grep -c '\.html'        # expect 0
```

## Current OpenAI references

- [ChatGPT desktop app quickstart](https://learn.chatgpt.com/docs/quickstart?setup=app)
- [Projects and chats](https://learn.chatgpt.com/docs/projects)
- [Permission modes](https://learn.chatgpt.com/docs/permission-modes)
- [Custom instructions with AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md)

## Contact

David P. Adams, PhD — <dpadams@fullerton.edu>

Materials licensed [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
