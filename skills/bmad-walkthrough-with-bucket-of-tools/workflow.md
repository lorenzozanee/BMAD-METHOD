# Walkthrough with a bucket of tools

**Goal:** Guide a human review of a target, one block at a time.

**CRITICAL:** If a step directs you to another snapshot file,
read it fully and follow it. No exceptions.

Help the user review a target, one block at a time. They may stop
to inspect, edit, or test. Keep track. The review is done when the
user says it is.

# Human attention is scarce

Show only what they need to see now. Do not distract them. Still do
the rest — write the log, revise the narrative, look things up,
reason — but do not put it in the session.

Do not call tools in this session. Spawn a cheap background subagent
for writing files, lookups, and any other tool work. Doing that work
yourself is not silent, even if you say nothing about it.

# Write for a human

The session and the review narrative are for a human. Assume that said
human has reasonable understanding of the surrounding context, but doesn't
know anything about the target except things that have been mentioned in
this session.
Leave the brief log style to the log.

Never write a file or `file:line` reference as plain text.

In the review narrative, every file and `file:line` is a markdown
link relative to that file (`[label](../src/foo.ts)`). No other
form.

In the session, never write a markdown link. Use a form the host
can click: a Cursor code citation (`startLine:endLine:path` on the
opening fence); a VS Code `#file:path`; or a CWD-relative
`path:line` with no leading `/`. If unsure, use `path:line`.

# Terms

- **Target:** The commit, PR, file, or directory being reviewed.
- **Review:** The session. Done when the user says it is.
- **Block:** One slice of the walkthrough. Accepted only when the user
  says so.
- **Review narrative:** The human-facing writeup. Organized in blocks.
  Owns block review status.
- **Review log:** Append-only record of review activities and outcomes.
- **Finding:** A concrete issue from inspection.
- **Move:** A user-selected action, maybe from a repertoire of
  moves in the walkthrough step.

# Block shapes

**Intent** (block 1). What the change is for and why it exists now.
If you found a target spec/plan file with an intent section, paste it
verbatim. Otherwise generate from what you know about the target, no
more than 300 tokens. Include a short note on where you got it from.

**Broad strokes** (block 2). What the change generally is, and its top
level: the three to five entry points a reader would open first, each
with one clickable reference and one clause saying what it is. This is
neither a second prose account of the intent nor an index of every
changed file. If you find yourself listing a layer's files, stop; that
belongs in the slices. Test: the reviewer can open the linked spots in
order and understand the mechanism without reading anything else.

**Slices** (middle blocks). One concern per block, not one file. Lead
with the mechanism in two or three sentences, then the specific places
with references.

For a simple change applied to a large number of files, group the
files by how they were changed (one or several groups). Treat each
group as a slice: one or two worked examples, plus a clickable list
of the rest that got the same treatment.

**Periphery** (last block). Docs, build registration, small enablers.
References only, one clause each.

# Conventions

- Every operational cross-file reference in this workflow is an
  absolute snapshot path. Open it directly; do not resolve it
  relative to a skill directory.
- `{project-root}`-prefixed paths resolve from the project working directory.

# On Activation

## Step 1: Execute Prepend Steps

Execute each of these steps in order before proceeding (`_None._` means skip):

{{ workflow.activation_steps_prepend }}

## Step 2: Load Persistent Facts

Treat every entry below as foundational context you carry for the rest
of the workflow run. Entries prefixed `file:` are paths or globs under
`{project-root}` -- load the referenced contents as facts. All other
entries are facts verbatim (`_None._` means none):

{{ workflow.persistent_facts }}

## Step 3: Execute Append Steps

Execute each of these steps in order (`_None._` means skip):

{{ workflow.activation_steps_append }}

Activation is complete after all activation steps have run.

# Workflow Execution

Follow the step files in order. Read one step fully, execute it, then
load the next step only when directed. Do not skip, reorder, or
pre-load steps.

# FIRST STEP

Read fully and follow: `{{ rendered("step-01-orientation.md") }}` to begin.
