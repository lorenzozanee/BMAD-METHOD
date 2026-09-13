---
name: bmad-walkthrough-with-bucket-of-tools
description: 'Guide a human review of a commit, PR, file, or directory. Use when invoked by name'
---

Help the user review a target, one block at a time. They may stop
to inspect, edit, or test. Keep track. The review is done when the
user says it is.

# Human attention is scarce

Show only what they need to see now. Do not distract them. Still do
the rest — write the log, revise the narrative, look things up,
reason — but do not put it in the session.

# Write for a human

The session and the review narrative are for a human. Assume that they
have reasonable understanding of the surrounding context, but don't know
anything about the target unless they have already seen it in this
session. Leave the brief log style to the log.

Never write a file or `file:line` reference as plain text. Always make
it a clickable link. Examples: a markdown link relative to that file
(`[label](../src/foo.ts)`); a Cursor code citation
(`startLine:endLine:path` on the opening fence);
a VS Code markdown link or `#file:path`; a CWD-relative `path:line` with
no leading `/` in a terminal. If unsure, use the CWD-relative `path:line`
form.

# Terms

- **Target:** The commit, PR, file, or directory being reviewed.
- **Review:** The session. Done when the user says it is.
- **Block:** One slice of the walkthrough. Accepted only when the user
  says so.
- **Review narrative:** The human-facing writeup. Organized in blocks.
  Owns block review status.
- **Review log:** Append-only record of review activities and outcomes.
- **Finding:** A concrete issue from inspection.
- **Move:** A user-selected action, may be maybe from a repertoire of 
  moves above.

# Orientation

Understand what the target is and what it is for. Use the target's
spec, PR description, and commit messages when they exist. Ask the
user questions until you know both.

# Review files

After orientation, write the review narrative and the review log.
Follow the project's artifact conventions; if there are none, use the
project root. Prefix both files with a shared short review slug and
check that their names are unused before creating them.

- **Review narrative:** Order blocks: intent, then broad strokes for
  the gist, then vertical slices of the main work, then periphery.
  Organize by concern, not by file. If the work is a mechanical
  fan-out: intent, broad strokes, then one block per kind of change
  — what was done to that group, one or two example slices, then a
  clickable list of the rest that got the same treatment. Then
  periphery.
  Use unchecked boxes for unvisited, in-progress, or reopened blocks,
  labeling their state; check a block when the user indicates they
  are satisfied with it. Note whether it changed during review and
  identify the current block. Work performed on a block does not
  itself mean it is accepted.
- **Review log:** Read and use [the log template](./templates/log-template.md).
  Keep findings, decisions, edits, and test results out of the review
  narrative.

# Walkthrough

Present the next block, with a clickable link to its place in the
review narrative. Suggest a couple of moves that fit. Stop there.
The named moves are not exhaustive; if something else is more
obvious, suggest that instead. The user may choose something you
did not suggest. Do what the user says. Stay with the current block
until the user explicitly says it is done.

When they say the block is done, revise the remaining narrative if
it needs to change. If the tree is dirty, ask the user whether to
commit. A dirty tree is generally undesirable; the user can still
move on. Then present the next block.

When every block has been gone through, suggest wrap-up.

# Moves

A repertoire the user may select from. Do not start a move unless the user 
picks it. Record the outcome in the review log and keep their place in 
the review narrative.

- **Thoughts:** In this session, look at the requested area and say
  what you think. Report concrete findings with clickable
  references. Do not use any formal review skills.
- **Second opinion:** The same question, in a fresh subagent that
  does not have this review's conversation. Do not use any formal review 
  skills.
- **Formal review:** Use the most appropriate formal review skill
  available. If it's code and `bmad-code-review` skill is installed, prefer 
  that unless the user says otherwise.
- **Test:** Help test the part under discussion. Identify useful checks
  and expected behavior, run what you can, and guide the user through
  observations that need them. Record what was actually tested, the
  results, and anything still unverified.
- **Drive:** Start the app and tell the user which buttons to push to
  see the target do its thing.
- **Wrap-up:** The review is finished. Guess the follow-through
  this work was for (e.g. merge the PR, write the review, commit
  and push if they edited) and ask the user if that is what they
  want. Do not do it until they say so. Do not end with only a
  summary in chat.
