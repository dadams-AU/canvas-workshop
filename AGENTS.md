# AGENTS.md — Canvas Course Builder

You are assisting a university instructor in drafting a Canvas course shell from a plain-text syllabus. The instructor is the final authority on all content. Your role is to draft; they verify.

## Project files

- `syllabus.txt` is the single source of truth for course content.
- `canvas-config.txt` contains exactly three `NAME=value` lines:
  - `CANVAS_BASE_URL` — for example, `https://csufullerton.instructure.com`
  - `CANVAS_TOKEN` — a temporary Canvas personal access token
  - `COURSE_ID` — the one sandbox course in scope

Load these values only when a Canvas request is required. Never display, quote, summarize, or log `CANVAS_TOKEN`. Do not place the literal token in a response or visible command. Refer to it through the loaded `CANVAS_TOKEN` variable.

All Canvas API requests use:

```text
Authorization: Bearer $CANVAS_TOKEN
Content-Type: application/json
```

Base path for this course: `$CANVAS_BASE_URL/api/v1/courses/$COURSE_ID`

Do not send the token or course data to any hostname other than the exact hostname in `CANVAS_BASE_URL`.

## Source of truth

Read `syllabus.txt` before planning or building. If it is missing or empty, stop and say so.

Do not invent policies, assignments, grading categories, dates, points, weights, rubrics, submission types, or course content. If something is missing or ambiguous, flag it for instructor review.

## Canvas endpoints

### Course verification and inventory (read only)

- `GET /api/v1/courses/:id` — verify the course name.
- `GET /api/v1/courses/:id/pages?per_page=100` — inventory pages.
- `GET /api/v1/courses/:id/modules?per_page=100` — inventory modules.
- `GET /api/v1/courses/:id/assignments?per_page=100` — inventory assignments.

### Pages

- `POST /api/v1/courses/:id/pages`
- Base body:

  ```json
  { "wiki_page": { "title": "...", "body": "<html>", "published": false, "front_page": false } }
  ```

- Set `front_page: true` only for the landing page.

### Modules

- `POST /api/v1/courses/:id/modules`
- Body:

  ```json
  { "module": { "name": "Week 1 — ...", "position": 1, "published": false } }
  ```

### Assignments

- `POST /api/v1/courses/:id/assignments`
- Base body:

  ```json
  { "assignment": { "name": "...", "description": "<html>", "published": false } }
  ```

- Add `points_possible` only when the syllabus specifies points clearly.
- Add `due_at` only when the syllabus gives a clear date. When no time is given, use `23:59` in the course time zone.
- Add `submission_types` only when the syllabus specifies the submission method clearly.
- If a date is missing or ambiguous, append `(DATE NEEDED)` to the assignment title and omit `due_at`.

### Module items

- `POST /api/v1/courses/:id/modules/:module_id/items`
- Assignment item body:

  ```json
  { "module_item": { "type": "Assignment", "content_id": 123, "position": 1, "published": false } }
  ```

- A page item uses `type: "Page"` and `page_url` instead of `content_id`.

### Assignment groups (only when the syllabus specifies weighted groups)

- `GET /api/v1/courses/:id/assignment_groups`
- `POST /api/v1/courses/:id/assignment_groups`
- Body:

  ```json
  { "name": "...", "group_weight": 25 }
  ```

## Non-negotiable rules

1. **One course only.** Confirm the course name with `GET /courses/:id` and report it before any write request. If it is not clearly the intended sandbox, stop.
2. **Unpublished by default.** Every page, module, assignment, and module item must have `published: false`. Never publish without a separate, explicit instructor request and confirmation.
3. **Preserve policy wording.** Copy late-work, academic-integrity, accommodation, and attendance language verbatim. Do not summarize, soften, or rephrase it.
4. **Do not invent.** Omit unspecified optional fields and flag them for review.
5. **Time zone.** Use the course time zone when available. If the syllabus gives no time and the course uses `America/Los_Angeles`, default to `23:59` local.
6. **One module per syllabus week.** Use week labels verbatim. Include exam, break, and other non-instructional weeks when they appear in the syllabus.
7. **Landing page.** Use only syllabus essentials: welcome, instructor contact, office hours, grading summary, and schedule highlights. Do not reproduce the full syllabus.
8. **Clean HTML.** Use valid Canvas-safe headings, paragraphs, and lists. Do not use scripts or external CSS.
9. **No duplicates.** Inventory existing Canvas content before writing. If a proposed title already exists, stop and show the conflict rather than creating another item.
10. **Secret handling.** Never print, return, echo, or write `CANVAS_TOKEN`. If a command or error would expose it, stop and use a redacted approach.

## Workflow contract

### Connect

1. Confirm `syllabus.txt`, `canvas-config.txt`, and this `AGENTS.md` exist.
2. Load the configuration without displaying its values.
3. Verify the one course with a read-only request.
4. Inventory existing pages, modules, and assignments.
5. Report the course name and counts. Make no changes.

### Preview

Before a build, propose a manifest containing:

- landing page
- syllabus weeks and module names
- overview pages based only on syllabus content
- assignments, explicit points, explicit due dates, and module placement
- missing or ambiguous information needing review

Make no Canvas write requests during Preview. Wait for the instructor to approve or revise the manifest.

### Build

After the instructor explicitly approves a manifest:

1. Reconfirm the course and check for title conflicts.
2. Create in this order: landing page → modules → overview pages → assignments → module items.
3. Create only approved items and keep everything unpublished.
4. Return counts, review flags, and failed operations with redacted error messages.

If a build stops partway through, inventory Canvas again and propose a resume plan. Never rerun the entire build blindly.

### Audit

Compare Canvas with both `syllabus.txt` and the approved manifest. Return a proposed diff covering missing information, duplicates, incorrect order or placement, policy drift, and failed operations. Do not apply changes.

### Finalize

Apply only corrections the instructor explicitly lists as approved. Keep everything unpublished, make no unrelated changes, and return a manual-review checklist.

## Safety

- Never publish during the workshop.
- Never delete existing Canvas content unless the instructor identifies the exact item and explicitly approves deletion.
- If an action could affect more than the one verified course, stop and ask for direction.
- If the Canvas response or a tool output contains a credential, redact it from the response.
