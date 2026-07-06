---
name: project-continuity
description: 'Never lose project context between sessions - maintain one PROJECT.md with decisions, current state, and next steps so any new Claude session (any model, any day) resumes in seconds instead of re-explaining everything. Use this skill at the START of every session on an existing project (read PROJECT.md first), at the END of every working session (update it), after every major decision, and IMMEDIATELY when the user says "waar waren we", "nieuwe sessie", "onthoud dit", "voor je weggaat", "schrijf alles op", or when the session/context is about to end. Also use it to produce a rapid handoff dump when a session must end abruptly.'
---

# Project Continuity

Claude sessions end. Models change. Context windows fill up. Without a written memory, every new session starts cold and the user pays the re-explanation tax — or worse, a new session quietly contradicts decisions an earlier session made. This skill fixes that with one living file: `PROJECT.md`.

## The core rule

Every project that spans more than one session gets a `PROJECT.md` in its root folder (or in the outputs folder if no project folder is connected). It is the single source of truth about the project. Not scattered notes, not chat history — one file.

## At session start

1. Look for `PROJECT.md` in the working folder. If it exists, read it BEFORE doing anything else.
2. Confirm briefly to the user what you understand the current state and next step to be ("We waren bezig met X, volgende stap was Y — klopt dat?").
3. If the file contradicts what the user now says, the user wins — update the file.

## The template

Keep this exact structure so every future session knows where to look:

```markdown
# [Projectnaam]

## Wat is dit
One paragraph: what the project is, for whom, and what "done" looks like.

## Stack & structuur
Tech choices + the 5-10 files/folders that matter, with one-line purpose each.

## Beslissingen
Newest first. Each entry: date — decision — WHY. The why is the valuable part;
it prevents future sessions from relitigating settled questions.
- 2026-07-06 — Supabase i.p.v. Firebase — betere SQL-queries nodig voor rapportage

## Huidige staat
What works, what is broken, what is half-finished. Be honest — "werkt bijna"
is useless to a cold-start session. Name exact files and symptoms.

## Volgende stappen
Prioritized, concrete, max 5. First item = where the next session starts.

## Conventies & voorkeuren
Everything learned about how the user wants things: language (NL/EN), tone,
formatting, naming, libraries to avoid, "geen bullet points in mails", etc.

## Niet aankomen
Things that look wrong but are intentional. Prevents helpful-but-destructive
"fixes" by future sessions.
```

## At session end (or after big decisions)

Update `PROJECT.md` — do not append endlessly, EDIT it:

- Move finished items out of "Volgende stappen"; update "Huidige staat".
- Add new decisions with their why.
- Prune anything stale. Target: under 200 lines. A bloated memory file is as useless as no file — future sessions skim it.
- Update proactively; do not wait for the user to ask. If a session did meaningful work and PROJECT.md was not touched, that is a bug.

## Rapid handoff (session ending NOW)

When the user signals the session is about to end abruptly ("je gaat bijna weg", context nearly full):

1. Skip pleasantries. Write or update PROJECT.md immediately with everything above.
2. Add a `## Handoff` section on top: what was happening this exact session, the last thing completed, the very next action, and any open questions for the user.
3. Include exact file paths and any commands needed to resume.
4. Tell the user in one line where the file is.

Speed matters more than polish here — a rough complete dump beats an elegant partial one.

## Why not just rely on chat history

Chat history is long, unstructured, contains dead ends, and is not shared across sessions or models. PROJECT.md is curated: only surviving decisions, only current state. Writing it forces the distinction between "what we tried" and "what is true now" — that distinction is the whole value.
