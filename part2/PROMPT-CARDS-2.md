# Canvas workshop prompt cards — Part 2

Use these prompts one at a time in **Codex** inside the ChatGPT desktop app. Keep the permission mode set to **Ask for approval**.

Part 1 built an empty shell. Part 2 fills it. The cards below assume the sandbox you built in Part 1 still exists and still holds unpublished modules and assignment stubs.

## Card 0 — Verify the setup

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

The version line must read **Part 2**. If it reads Part 1, or if it is absent, the Part 2 files did not extract into the right folder. Fix that before Card 1.

## Card 1 — Connect and inventory

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

Stop if Codex reports a course name other than your sandbox.

## Card 2 — Expand before writing

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

Read the manifest against your own materials before approving it. Two things to look for: every `(INSTRUCTOR DRAFT NEEDED)` marker is somewhere you agree the source is silent, and every rubric total matches its assignment.

## Card 3 — Draft the approved content

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

Approve a network request only when it targets your institution's Canvas hostname and matches the approved manifest.

## Card 4 — Accessibility and fidelity audit

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

An automated pass finds markup failures. It does not find alt text that is present and wrong, link text that reads well and points somewhere else, or a heading structure that is valid and meaningless. Those are yours.

## Card 5 — Finalize approved corrections

```text
Apply only these corrections that I explicitly approved:
- [paste the approved items here]

Keep everything UNPUBLISHED. Do not change any other item. Do not
remove any DRAFT — prefix or (INSTRUCTOR DRAFT NEEDED) marker unless
I listed it above.

Return a final manual-review checklist and report any failures.
```

"Finalize" means complete the draft. It does not mean publish.

## Manual review checklist

Content

- [ ] Every module overview page states objectives that came from your materials, not from the agent.
- [ ] Every assignment description matches the prompt you actually assign.
- [ ] Readings are attributed correctly and none were added.
- [ ] Policy language matches the original syllabus verbatim.

Rubrics

- [ ] Each rubric is attached to the intended assignment.
- [ ] Each rubric total equals that assignment's points.
- [ ] Each criterion's top rating equals that criterion's points.
- [ ] You have decided whether the rubric calculates the grade. The default is no.

Accessibility

- [ ] Body headings start at level 2 and skip no levels.
- [ ] Lists use list markup.
- [ ] Every link's text describes where it goes.
- [ ] Every table has a caption and header cells with scope.
- [ ] No meaning is carried by color alone.
- [ ] Every image has alt text you wrote after looking at the image.

Before it leaves draft

- [ ] Every `DRAFT — ` prefix has been resolved or deliberately kept.
- [ ] Every `(INSTRUCTOR DRAFT NEEDED)` marker has been resolved.
- [ ] Every `(DATE NEEDED)` flag from Part 1 has been resolved.
- [ ] Every `(ALT TEXT NEEDED)` marker has been resolved.
- [ ] Pages, modules, assignments, module items, and discussions remain unpublished.

## Cleanup

When you finish, revoke the temporary token in Canvas and delete `canvas-config.txt` from your computer.
