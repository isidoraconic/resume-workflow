# Resume Workflow: Career Inventory

A multi-agent workflow that turns years of work (code, design docs, code reviews,
tickets, perf reviews) into one **master record** of everything I've done. It's detailed
enough to jog my memory or build any resume, and it exports a copy with internal details
removed.

Runs on the work machine with approved tools. Only `career-inventory/export/` leaves it.

## Quick start
1. Copy `BRIEF.template.md` → `career-inventory/BRIEF.md` and fill it in (about 1–2 hrs).
2. Copy `RULES.md` → `career-inventory/RULES.md`.
3. Paste `prompts/00-orchestrator.md` into your agent. It runs only P0, then stops and
   shows you a slicing plan.
4. Keep approving at each ⏸. If a session runs out, start a new one and paste the
   orchestrator again; it resumes from `career-inventory/STATE.md`.

## Why many agents instead of one
One agent going through 4 years of material ends up skimming. Here the orchestrator
never reads raw material; each subagent gets a small slice (≤1 quarter × 1 source, about
100 items), writes to a file and reports back briefly. P0 records how many items exist,
and every later phase has to account for all of them.

## Pipeline
| Phase | Agent (`prompts/subagents/`) | Output |
|---|---|---|
| P0 | Source mapper | `00-sources.md`, counts per quarter, slicing plan ⏸ |
| P1 | `harvester` (one per quarter × source) | `raw/<Q>/<source>.md` index |
| P2 | `code-reader` (per repo/CR cluster), `doc-reader` (≤5 docs each) | `reads/code/*`, `reads/docs/*` |
| P3 | `digester` (per quarter) | `quarters/<Q>.md` contributions |
| P4 | `auditor` (per quarter, loops) | `audits/<Q>.md` |
| P5 | leads sweep + `cross-checker` | `crosscheck.md` ⏸ |
| P6 | `synthesizer` (per project) | `projects/<name>.md` ⏸ |
| P7 | `investigator` (per project) | implied work, under-claiming, `questions/<name>.md` |
| P8 | `prompts/interviewer.md` (with you) | answers tagged `[FROM-ME]` |
| P9 | `prompts/final-completeness-interview.md` | `MASTER.md` ⏸ |
| P10 | `sanitizer-and-redaction-reviewer` | `export/MASTER.export.md`, `REDACTIONS.md` ⏸ |

## Output format
See `templates/MASTER.template.md`: timeline, skills index, then **Project →
Contributions**. Each contribution has dates, role, how it was built, tech, scale,
impact, supporting work, collaborators by role, keywords and open questions. After that
come other work (oncall, reviews, interviews, mentoring, tools), recognition, and open
items.
