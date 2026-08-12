# From Syllabus to Canvas with Codex

Materials for **From Syllabus to Canvas: Building Your Course Shell with an AI Agent**, a 60-minute faculty Zoom workshop on August 18, 2026.

The workshop demonstrates how to use **Codex in the ChatGPT desktop app** to turn a plain-text syllabus into an unpublished Canvas course draft.

**Audience:** Faculty with no programming, terminal, Git, GitHub, or Canvas API experience.

**Standard:** AI drafts. The instructor verifies. Nothing is published during the workshop.

## Start here during the Zoom

You do not need Git or a GitHub account. This page is only a place to download one file.

1. Click **`canvas-workshop-starter.zip`** in the file list above.
2. Click the download button on the next page.
3. Double-click the downloaded ZIP to extract it.
4. Open `README-FIRST.txt` inside the new `canvas-workshop` folder.

The ZIP contains the copyable HTML slides, a fictional practice syllabus, blank configuration template, five prompt cards, and safety instructions. It never contains a real Canvas token.

For easier copying and pasting, double-click **`slides-app.html`** after extracting the ZIP. It opens the complete deck in a web browser, where participants can select the prompt-card text. `PROMPT-CARDS.md` provides the same prompts without the surrounding slides.

## Account

A university-managed **ChatGPT Edu** account is preferred. During the live session, participants should use only the fictional syllabus and an empty Canvas sandbox—never student records or other confidential data. Anyone without access to Codex can watch the demonstration and use the materials later.

## What is in this repository

| Path | Purpose |
|---|---|
| `canvas-workshop-starter.zip` | One-download participant bundle |
| `slides-app.pdf` | Current 60-minute presentation |
| `slides-app.md` / `slides-app.html` | Marp source and copyable browser version |
| `AGENTS.md` | Canvas API workflow and agent guardrails |
| `PROMPT-CARDS.md` | Five prompts and manual-review checklist |
| `README-FIRST.txt` | Plain-language participant setup |
| `canvas-config-template.txt` | Blank template for Canvas URL, token, and course ID |
| `syllabus-sample.txt` | Fictional syllabus included in the starter ZIP as `syllabus.txt` |
| `command-line-instructions/` | Archived CLI version for experienced users |

## The five-checkpoint workflow

1. **Connect:** Verify the one sandbox course using read-only requests.
2. **Preview:** Produce a proposed manifest from `syllabus.txt`; make no Canvas changes.
3. **Build:** Create only the instructor-approved manifest, unpublished.
4. **Audit:** Compare Canvas with the syllabus and propose corrections.
5. **Finalize:** Apply only explicitly approved corrections; keep everything unpublished.

The copy-and-paste prompts are in [PROMPT-CARDS.md](PROMPT-CARDS.md).

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

## Rebuild the materials

The slides use [Marp](https://marp.app/):

```bash
npx @marp-team/marp-cli slides-app.md
npx @marp-team/marp-cli slides-app.md --pdf
```

Rebuild the starter ZIP whenever any source file changes. It should contain:

- `AGENTS.md`
- `PROMPT-CARDS.md`
- `README-FIRST.txt`
- `slides-app.html`
- `canvas-config-template.txt`
- `.gitignore`
- `syllabus-sample.txt`, renamed to `syllabus.txt` inside the ZIP

## Current OpenAI references

- [ChatGPT desktop app quickstart](https://learn.chatgpt.com/docs/quickstart?setup=app)
- [Projects and chats](https://learn.chatgpt.com/docs/projects)
- [Permission modes](https://learn.chatgpt.com/docs/permission-modes)
- [Custom instructions with AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md)

## Contact

David P. Adams, PhD — <dpadams@fullerton.edu>

Materials licensed [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
