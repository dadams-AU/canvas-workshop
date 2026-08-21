# Canvas workshop prompt cards

Use these prompts one at a time in **Codex** inside the ChatGPT desktop app. Keep the permission mode set to **Ask for approval**.

## Card 1 — Connect safely

```text
Use canvas-config.txt without displaying its values.

1. Confirm this project contains syllabus.txt and AGENTS.md.
2. Connect to the one Canvas course in COURSE_ID using GET only.
3. Report the course name and the current counts of modules,
   pages, and assignments.

Do not create or change anything. Never display CANVAS_TOKEN.
```

Stop if Codex reports the wrong course name.

## Card 2 — Preview before writing

```text
Read syllabus.txt and propose a manifest of everything you would
create: landing page, weekly modules, overview pages, assignments,
points, due dates, and module placement.

Use the syllabus week labels verbatim, including any exam or break
weeks. Flag missing or ambiguous information; do not guess.

Do not make Canvas changes. Wait for my approval.
```

Compare the manifest with your syllabus before approving it.

## Card 3 — Build the approved manifest

```text
Build only the manifest I approved in my Canvas sandbox.

Before creating anything, stop if an existing Canvas item has the
same title. Keep every page, module, assignment, and module item
UNPUBLISHED. Preserve syllabus policy wording verbatim.

Return counts, items needing review, and any failed operations.
Never display CANVAS_TOKEN.
```

Approve a network request only when it targets your institution's Canvas hostname and matches the task.

## Card 4 — Audit without changing

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

## Card 5 — Finalize approved corrections

```text
Apply only these corrections that I explicitly approved:
- [paste the approved items here]

Keep everything UNPUBLISHED. Do not change any other item.
Return a final manual-review checklist and report any failures.
```

“Finalize” means complete the draft. It does not mean publish.

## Manual review checklist

- [ ] The course name and course ID identify the intended sandbox.
- [ ] Every assignment name appears exactly once.
- [ ] Points, due dates, and submission types match the syllabus.
- [ ] Module names, sequence, and assignment placement match the syllabus.
- [ ] Policy language matches the original syllabus verbatim.
- [ ] Grading weights match the syllabus, if weights are specified.
- [ ] Every `(DATE NEEDED)` flag is resolved.
- [ ] Pages, modules, assignments, and module items remain unpublished.
- [ ] The landing page is set as the course front page. The agent cannot do this: in Canvas, go to **Pages → View All Pages**, open the landing page, and choose **⋮ → Use as Front Page** after you publish.

## Cleanup

When you finish, revoke the temporary token in Canvas and delete `canvas-config.txt` from your computer.
