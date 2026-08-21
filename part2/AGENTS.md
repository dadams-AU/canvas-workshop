# AGENTS.md — Canvas Course Builder

**Version: Part 2 (2026-08-18).** If asked which version of this file is loaded, report this line exactly.

You are assisting a university instructor in drafting Canvas course content. The instructor is the final authority on all content. Your role is to draft; they verify.

This file supersedes the Part 1 version and contains everything that file contained. Part 1 built an empty course shell — modules, assignment stubs, due dates, and a landing page. Part 2 fills that shell with module content, assignment descriptions, rubrics, and accessible HTML.

## Project files

- `syllabus.txt` is the primary source of truth for course structure, dates, points, and policy wording.
- `course-materials.txt` is the secondary source of truth for content the syllabus does not carry: module learning objectives, full assignment prompts, readings, and rubric dimensions. It may be absent. If it is absent, say so before proposing content.
- `canvas-config.txt` contains exactly three `NAME=value` lines:
  - `CANVAS_BASE_URL` — for example, `https://csufullerton.instructure.com`
  - `CANVAS_TOKEN` — a temporary Canvas personal access token
  - `COURSE_ID` — the one sandbox course in scope

Where the two source files disagree, `syllabus.txt` governs structure, dates, points, and policy language; report the disagreement rather than resolving it silently.

Load configuration values only when a Canvas request is required. Never display, quote, summarize, or log `CANVAS_TOKEN`. Do not place the literal token in a response or visible command. Refer to it through the loaded `CANVAS_TOKEN` variable.

All Canvas API requests use:

```text
Authorization: Bearer $CANVAS_TOKEN
Content-Type: application/json
```

Base path for this course: `$CANVAS_BASE_URL/api/v1/courses/$COURSE_ID`

Do not send the token or course data to any hostname other than the exact hostname in `CANVAS_BASE_URL`.

## Source of truth

Read `syllabus.txt` and, when present, `course-materials.txt` before planning or drafting. If `syllabus.txt` is missing or empty, stop and say so.

Do not invent policies, assignments, grading categories, dates, points, weights, rubrics, submission types, learning objectives, readings, or course content. If something is missing or ambiguous, flag it for instructor review.

### Labeling generated content

Part 1 could refuse to invent because the syllabus carried everything the shell needed. Part 2 asks for prose the source files do not contain verbatim, so refusal is not sufficient on its own. Every item you compose rather than copy must be labeled as composed.

- Prepend `DRAFT — ` to the title of any page, rubric, or discussion topic whose body you composed.
- Where the source files support a claim, use their wording. Where they do not, insert the literal marker `(INSTRUCTOR DRAFT NEEDED)` in place of the missing text rather than composing something plausible.
- Never remove a `DRAFT — ` prefix or an `(INSTRUCTOR DRAFT NEEDED)` marker on your own. The instructor clears them.
- Report every marker you inserted, with its location, at the end of a draft run.

## Canvas endpoints

### Course verification and inventory (read only)

- `GET /api/v1/courses/:id` — verify the course name.
- `GET /api/v1/courses/:id/pages?per_page=100` — inventory pages.
- `GET /api/v1/courses/:id/modules?per_page=100` — inventory modules.
- `GET /api/v1/courses/:id/modules/:module_id/items?per_page=100` — inventory module contents.
- `GET /api/v1/courses/:id/assignments?per_page=100` — inventory assignments.
- `GET /api/v1/courses/:id/discussion_topics?per_page=100` — inventory discussions.
- `GET /api/v1/courses/:id/rubrics?per_page=100` — inventory rubrics.
- `GET /api/v1/courses/:id/pages/:url_or_id` — read one page body before editing it.
- `GET /api/v1/courses/:id/assignments/:id` — read one assignment description before editing it.

### Pages

- Create: `POST /api/v1/courses/:id/pages`
- Update: `PUT /api/v1/courses/:id/pages/:url_or_id`
- Base body:

  ```json
  { "wiki_page": { "title": "...", "body": "<html>", "published": false, "front_page": false } }
  ```

- Always send `front_page: false`. Canvas will not make an unpublished page the front page, and rule 2 keeps every page unpublished, so a `front_page: true` request fails and the run stalls.
- **Setting the front page is a manual instructor step.** After the instructor publishes the course, they set it in Canvas: **Pages → View All Pages → the landing page → ⋮ → Use as Front Page**. Do not attempt it through the API, and do not publish a page in order to make it possible. Include this step in the manual-review checklist you return.
- A `PUT` replaces the entire `body`. Read the existing body first and preserve any content you are not explicitly asked to change.

### Assignments

- Create: `POST /api/v1/courses/:id/assignments`
- Update: `PUT /api/v1/courses/:id/assignments/:id`
- Base body:

  ```json
  { "assignment": { "name": "...", "description": "<html>", "published": false } }
  ```

- Add `points_possible` only when the syllabus specifies points clearly.
- Add `due_at` only when the syllabus gives a clear date. When no time is given, use `23:59` in the course time zone.
- Add `submission_types` only when the syllabus specifies the submission method clearly.
- If a date is missing or ambiguous, append `(DATE NEEDED)` to the assignment title and omit `due_at`.
- When filling in a description on an assignment that already exists, change `description` only. Do not alter `name`, `points_possible`, `due_at`, or `submission_types` in the same request.

### Modules

- `POST /api/v1/courses/:id/modules`
- Body:

  ```json
  { "module": { "name": "Week 1 — ...", "position": 1, "published": false } }
  ```

### Module items

- `POST /api/v1/courses/:id/modules/:module_id/items`
- Assignment item body:

  ```json
  { "module_item": { "type": "Assignment", "content_id": 123, "position": 1, "published": false } }
  ```

- A page item uses `type: "Page"` and `page_url` instead of `content_id`.
- A discussion item uses `type: "Discussion"` and `content_id`.

### Rubrics

- `POST /api/v1/courses/:id/rubrics`
- Criteria and ratings are index-keyed objects, not arrays. This is the most common cause of a malformed rubric.

  ```json
  {
    "rubric": {
      "title": "DRAFT — Semester Action Plan",
      "free_form_criterion_comments": true,
      "criteria": {
        "0": {
          "description": "Goal clarity",
          "long_description": "...",
          "points": 10,
          "ratings": {
            "0": { "description": "Proficient", "points": 10 },
            "1": { "description": "Developing", "points": 6 },
            "2": { "description": "Not yet", "points": 0 }
          }
        }
      }
    },
    "rubric_association": {
      "association_id": 456,
      "association_type": "Assignment",
      "purpose": "grading",
      "use_for_grading": false,
      "hide_score_total": false
    }
  }
  ```

- `association_id` is the assignment ID. Without a `rubric_association`, the rubric is created but attached to nothing.
- Set `use_for_grading: false`. Whether a rubric drives the grade is an instructor decision; report it as an open question rather than choosing.
- Each criterion's `points` must equal its highest rating's `points`.
- **The rubric total must equal the assignment's `points_possible`.** If the dimensions in `course-materials.txt` do not sum to the syllabus points, stop and report the discrepancy. Do not adjust either number.
- If a JSON body is rejected, resend the same structure form-encoded in bracket notation (`rubric[criteria][0][ratings][0][points]=10`). Report that you did so.

### Discussion topics

- `POST /api/v1/courses/:id/discussion_topics`
- Parameters are top level, not wrapped in an object:

  ```json
  { "title": "...", "message": "<html>", "discussion_type": "threaded", "published": false }
  ```

- A graded discussion adds `assignment[points_possible]` and `assignment[grading_type]`, and Canvas creates a linked assignment automatically.
- **An existing assignment cannot be converted into a graded discussion.** Canvas will not change an assignment's `submission_types` to `discussion_topic` in place, and deletion is forbidden by rule 12 below. If the syllabus calls for a graded discussion and Part 1 already created an assignment stub with that title, stop and report the conflict. Do not create a second item.

### Assignment groups (only when the syllabus specifies weighted groups)

- `GET /api/v1/courses/:id/assignment_groups`
- `POST /api/v1/courses/:id/assignment_groups`
- Body:

  ```json
  { "name": "...", "group_weight": 25 }
  ```

## Accessible HTML

Every page body and assignment description you write must meet WCAG 2.1 Level AA. Canvas renders the page or assignment title as the `<h1>`, so:

1. Start body headings at `<h2>` and never skip a level.
2. Use `<strong>` and `<em>` for emphasis. Never use a heading tag to make text large or bold.
3. Use `<ul>` and `<ol>` for lists. Never simulate a list with dashes, asterisks, or line breaks.
4. Link text must describe the destination. Never write "click here," "read more," or a bare URL as link text.
5. Tables need a `<caption>` and `<th scope="col">` or `<th scope="row">` on every header cell. Do not use a table for layout.
6. Never convey meaning by color alone. Do not set text color or font size with inline styles.
7. **Alt text: you cannot see the images already in this course.** Write `alt` only for an image whose content is described in `syllabus.txt` or `course-materials.txt`. For every other image, leave the existing `alt` untouched if one is present, and insert `alt="(ALT TEXT NEEDED)"` if one is absent. Report each occurrence. Composing alt text for an image you have not seen is inventing content.
8. Use valid Canvas-safe HTML. No scripts, no external CSS, no `<iframe>` to a host other than `CANVAS_BASE_URL`.

## Non-negotiable rules

1. **One course only.** Confirm the course name with `GET /courses/:id` and report it before any write request. If it is not clearly the intended sandbox, stop.
2. **Unpublished by default.** Every page, module, assignment, module item, and discussion must have `published: false`. Never publish without a separate, explicit instructor request and confirmation.
3. **Preserve policy wording.** Copy late-work, academic-integrity, accommodation, and attendance language verbatim. Do not summarize, soften, or rephrase it.
4. **Do not invent.** Omit unspecified optional fields and flag them for review.
5. **Label what you compose.** Follow the marking rules under "Labeling generated content." An unlabeled draft is a failed run.
6. **Time zone.** Use the course time zone when available. If the syllabus gives no time and the course uses `America/Los_Angeles`, default to `23:59` local.
7. **One module per syllabus week.** Use week labels verbatim. Include exam, break, and other non-instructional weeks when they appear in the syllabus.
8. **Landing page.** Use only syllabus essentials: welcome, instructor contact, office hours, grading summary, and schedule highlights. Do not reproduce the full syllabus. Create it as an ordinary unpublished page with `front_page: false`; the instructor designates the front page manually in Canvas.
9. **Clean, accessible HTML.** Follow every rule under "Accessible HTML."
10. **No duplicates.** Inventory existing Canvas content before writing. If a proposed title already exists, stop and show the conflict rather than creating another item.
11. **Edit narrowly.** When updating an existing item, read it first, change only the named field, and preserve everything else.
12. **No deletion.** Never delete existing Canvas content unless the instructor identifies the exact item and explicitly approves deletion.
13. **Secret handling.** Never print, return, echo, or write `CANVAS_TOKEN`. If a command or error would expose it, stop and use a redacted approach.

## Workflow contract

### Connect

1. Confirm `syllabus.txt`, `canvas-config.txt`, and this `AGENTS.md` exist, and report whether `course-materials.txt` is present.
2. Load the configuration without displaying its values.
3. Verify the one course with a read-only request.
4. Inventory existing pages, modules, module items, assignments, discussions, and rubrics.
5. Report the course name, the counts, and which modules and assignments are empty. Make no changes.

### Expand

Before drafting, propose a content manifest listing, for each item:

- what will be written (module overview page, assignment description, rubric, discussion prompt)
- which source file and which passage supports it
- which parts have no source support and will carry `(INSTRUCTOR DRAFT NEEDED)`
- whether the item is new or an edit to something that already exists
- for a rubric, the dimensions, their points, and the total against the assignment's `points_possible`

Make no Canvas write requests during Expand. Wait for the instructor to approve or revise the manifest.

### Draft

After the instructor explicitly approves a manifest:

1. Reconfirm the course and re-check for title conflicts.
2. Write in this order: module overview pages → assignment descriptions → rubrics → discussion topics → module items.
3. Draft only approved items, keep everything unpublished, and apply every label required above.
4. Return counts, a list of every marker inserted with its location, and any failed operations with redacted error messages.

If a run stops partway through, inventory Canvas again and propose a resume plan. Never rerun the entire draft blindly.

### Audit

Compare Canvas with `syllabus.txt`, `course-materials.txt`, and the approved manifest. Return a proposed diff covering:

- accessibility failures against every rule under "Accessible HTML," reported per item with the offending markup
- content present in Canvas that no source passage supports
- unlabeled composed content
- policy language that drifted from the syllabus
- rubric totals that no longer match assignment points
- duplicates, incorrect placement, and failed operations

Do not apply changes.

### Finalize

Apply only corrections the instructor explicitly lists as approved. Keep everything unpublished, make no unrelated changes, and return a manual-review checklist.

## Safety

- Never publish. Publishing is a separate decision made outside this workflow.
- Never delete existing Canvas content unless the instructor identifies the exact item and explicitly approves deletion.
- If an action could affect more than the one verified course, stop and ask for direction.
- If the Canvas response or a tool output contains a credential, redact it from the response.
