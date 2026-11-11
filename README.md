# Career Inventory Playbook

A multi-agent workflow for turning years of work history into a complete, evidence-backed
master resume. It collects everything, audits it, interviews you to fill the gaps, and only
then exports a copy with confidential details removed.

Built to run on a work machine with approved tools. Only `export/` should ever leave it.

## Quick start
1. Copy `BRIEF.template.md` → `career-inventory/BRIEF.md` and fill it in (about 1–2 hrs).
2. Copy `RULES.md` → `career-inventory/RULES.md`.
3. Paste `prompts/00-orchestrator.md` into your agent. It sends out the subagents in
   `prompts/subagents/` and tracks progress in `career-inventory/STATE.md`.
4. Interview phase: `prompts/interviewer.md` (one project per session), then
   `prompts/final-completeness-interview.md`.

The whole playbook in one file: [`PLAYBOOK.md`](PLAYBOOK.md).

## Pipeline
| Phase | Agent | Output |
|---|---|---|
| P0 | Source mapper | `00-sources.md` |
| P1 | Harvesters (quarter × source) | `raw/<Q>/<source>.md` |
| P2 | Digesters (per quarter) | `quarters/<Q>.md` |
| P3 | Auditors (per quarter, loops) | `audits/<Q>.md` |
| P4 | Leads sweep | `LEADS.md` cleared |
| P5 | Cross-checker vs perf/promo docs | `crosscheck.md` |
| P6 | Synthesizers (per project) | `projects/<name>.md` |
| P7–8 | Interviewer (with you) | answers tagged `[FROM-ME]`, `master-summary.md` |
| P9 | Sanitizer, then redaction reviewer | `export/`, `REDACTIONS.md` |
