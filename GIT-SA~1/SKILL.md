---
name: git-safety-net
description: 'Use version control as an undo machine for every project - initialize git early, commit at every working state, and recover calmly from "ik heb iets kapotgemaakt" moments without losing work. Use this skill at the start of ANY multi-file or multi-session project (init + first commit belong in setup), after every completed feature or fix, and IMMEDIATELY when the user says "terug naar gisteren", "vorige versie", "alles is kapot", "kan ik dit ongedaan maken", or fears losing work. Also the prerequisite for ship-it: git-connected deploys need a repo.'
---

# Git Safety Net

Without version control, every experiment risks the whole project and "even iets proberen" becomes scary. With it, any working state is one command away — which changes how boldly you can build. This skill is git for a solo builder: an undo machine, not a team ceremony.

## Setup (first minutes of any project)

- `git init` in the project root before meaningful work exists. Retrofitting history is impossible.
- Immediately add `.gitignore` BEFORE the first commit: `node_modules/`, `.env`, build output (`dist/`), OS junk (`.DS_Store`). A secret committed once lives in history forever — see ship-it for rotation.
- First commit = the working skeleton. From here, the safety net exists.

## The core habit: commit every working state

Commit whenever the project WORKS and something is finished — a feature, a fix, a styling pass. Not by the clock, by state. The test: "als ik nu alles verpest, is dit het punt waar ik naar terug wil."

- Message = what + why in one line, present tense: `voeg contactformulier validatie toe`. Six months later the message is the only documentation of intent.
- Never commit a broken state on the main line "voor de zekerheid" — a safety net of broken states catches nothing. (Half-done work that must be saved: use a branch or `git stash`.)
- For Claude sessions specifically: commit at the end of every working session, so the next session (see project-continuity) starts from a known-good point.

## Experiments: branch instead of hope

Trying a risky redesign or refactor? `git switch -c experiment-nieuwe-layout` first. Works → merge back. Fails → `git switch main` and the experiment never happened. Branches for a solo builder are just named parallel saves — use them for anything scary, skip elaborate branching models.

## Recovery playbook (calm, in escalating order)

The golden rule during panic: as long as you do not run destructive commands, git almost never loses committed work. Diagnose first: `git status` + `git log --oneline -10`.

| Situation | Fix |
|---|---|
| Uncommitted changes are wrong, want last commit back | `git restore <file>` (or `git restore .` for everything — gone is gone for uncommitted work, so say so before running it) |
| Last commit is wrong, keep the work | `git reset --soft HEAD~1` — commit undone, changes stay |
| Want to see/return to an older state | `git log --oneline`, then `git checkout <hash>` to LOOK; `git revert <hash>` to undo one commit safely (works even after pushing) |
| "Alles kwijt, ik zie mijn werk nergens" | `git reflog` — the journal of everything HEAD did; almost always the rescue |
| Committed a file that should not be there | Remove + add to `.gitignore` + commit; if it is a secret, rotate it (ship-it) |

Prefer `revert` (adds an undo-commit) over `reset --hard` (rewrites history) whenever the work has been pushed or shared. Never suggest `--force` push to a solo builder without explaining exactly what it destroys.

## Remote = offsite backup

A local repo dies with the laptop. Push to GitHub/GitLab (private repo is fine, free) as soon as the project matters: `git remote add origin <url> && git push -u origin main`. Push at least at session end. This also unlocks git-connected deploys (ship-it) and sharing.

## What NOT to import

No rebase workflows, no squash policies, no commit-lint, no PR process against yourself. Those solve team problems. The whole practice is: ignore-file → commit working states → branch for experiments → push. Four habits, full safety.
