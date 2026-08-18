CANVAS + CODEX WORKSHOP, PART 2 — START HERE

Part 1 is a prerequisite. You should already have the ChatGPT desktop app
installed and a Canvas sandbox course with the shell you built in Part 1.

This folder is complete on its own. You do not merge it with your Part 1
folder, and you do not need Git, a command line, or a GitHub account.

Two things you need that are not in this folder:

  - A NEW Canvas token. The one from Part 1 was revoked at the end of
    that session and will not work.
  - The course ID of your Part 1 sandbox.


SETUP, FOUR STEPS

1. Get the folder. Extract canvas-workshop-part2-starter.zip anywhere you
   like. It makes a folder named canvas-workshop-part2.

   If the download is blocked, skip to NO-DOWNLOAD SETUP below. It takes
   about four minutes and needs nothing but Notepad.

2. In Canvas, create a new temporary access token:
   Account > Settings > New Access Token
   Use the shortest practical expiration date. Copy it once.

3. Make a copy of canvas-config-template.txt and rename the copy to
   canvas-config.txt. Open it in Notepad or TextEdit and fill in your
   Canvas URL, the new token, and your Part 1 sandbox course ID.

   Keep this file on your own computer. Do not email, upload, or share it.

4. Open the ChatGPT desktop app, select Codex from the ChatGPT dropdown,
   press Ctrl+O on Windows or Cmd+O on macOS, and select the
   canvas-workshop-part2 folder. Start a new chat. Set the permission
   control beneath the message box to Ask for approval.

Then open PROMPT-CARDS-2.md and run Card 0. Card 0 checks everything
above and tells you what is missing without touching Canvas. Run it
before the session starts if you can.


NO-DOWNLOAD SETUP

Some managed Windows computers block downloaded ZIP files. Nothing in
this workshop needs a ZIP. Every file is plain text, and you can build
the folder by copying and pasting.

You need exactly three files. Skip the rest; they are conveniences.

1. Make a new folder on your Desktop named canvas-workshop-part2.

2. Open each of these three pages in your browser and click the "Raw"
   button, which shows the plain text with nothing around it:

     AGENTS.md
     syllabus.txt        (shown in the repository as syllabus-sample.txt)
     course-materials.txt (shown as course-materials-sample.txt)

3. For each one: select all the text, copy it, paste it into Notepad, and
   use File > Save As to save it into your new folder under the name in
   the left column above. In the Save As dialog, set "Save as type" to
   "All Files" so Notepad does not add .txt to AGENTS.md.

4. Make a fourth file the same way, named canvas-config.txt, containing
   three lines. Type these yourself and fill in your own values:

     CANVAS_BASE_URL=https://csufullerton.instructure.com
     CANVAS_TOKEN=your_new_temporary_token
     COURSE_ID=your_sandbox_course_id

That folder is everything Codex needs. Go back to step 4 above and open
it in the ChatGPT desktop app.

You do not need PROMPT-CARDS-2.md on your computer. Read it in your
browser during the session. On GitHub each prompt has a copy button in
the top-right corner of its box, which is the easiest way to use them.


WHAT IS IN THIS FOLDER

- AGENTS.md: safety and Canvas instructions for Codex. This is the Part 2
  version. It contains everything the Part 1 version contained, plus
  rubrics, accessible HTML, and the labeling rules for drafted content.
- PROMPT-CARDS-2.md: Cards 0 through 5 for today.
- PROMPT-CARDS.md: the Part 1 cards, in case you need to rebuild a shell.
- README-FIRST-PART2.txt: this file.
- syllabus.txt: the same fictional syllabus from Part 1.
- course-materials.txt: the fictional instructor's learning objectives,
  assignment prompts, readings, and rubric dimensions. Deliberately
  incomplete.
- canvas-config-template.txt: a blank place for three Canvas values.

The slides are a separate download and are not required. Everything you
need to copy and paste is in PROMPT-CARDS-2.md.


IF SOMETHING IS MISSING

The download was blocked. Use NO-DOWNLOAD SETUP above. Do not turn off
Windows Defender, SmartScreen, or any other security control, and do not
ask your IT department to make an exception for a workshop file.

No sandbox, or an empty one. You can still follow the whole session. Point
canvas-config.txt at a fresh empty sandbox and run Cards 1 through 3 from
PROMPT-CARDS.md to rebuild the Part 1 shell first. That takes about ten
minutes. Or watch today and rebuild afterward.

Codex is missing from the dropdown. Confirm you are signed in to the
university-managed ChatGPT Edu account rather than a personal one.

Blocked by your device or account in some other way. Watch the
demonstration and use these materials later. Do not bypass a university
security control to keep pace with the group.


SAFETY

- Practice with the fictional syllabus and your empty Canvas sandbox. Do
  not use student records or other confidential data.
- Stop if Codex reports a course name other than your sandbox.
- Approve network access only to your institution's Canvas hostname.
- Keep everything unpublished.
- Never display or paste your token into chat.
- Revoke the token and delete canvas-config.txt before leaving Zoom.


AFTER THE WORKSHOP

Replace both fictional files with your own. Put a plain-text copy of your
syllabus in syllabus.txt, and put your learning objectives, assignment
prompts, readings, and rubric dimensions in course-materials.txt. Then
repeat the workflow in a fresh sandbox.

The quality of what the agent drafts is set by what is in those two files.
There is no prompt that fixes a missing input.

Questions: David P. Adams, PhD <dpadams@fullerton.edu>
