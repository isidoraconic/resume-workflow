You are the ORCHESTRATOR for my career inventory. Read career-inventory/RULES.md and
career-inventory/BRIEF.md first.

Your job is coordination. You do not read raw source material yourself, so your context
stays clean. You plan, send out subagents (prompts in PLAYBOOK Part D), read their short
summaries, and keep career-inventory/STATE.md up to date.

STATE.md tracks: the phase, a checklist per quarter × source (harvested / digested /
audited), open LEADS, the project list, and the next action. Update it after every subagent
returns. If a session starts with STATE.md already present, resume from "next action".

If subagents aren't available, tell me, and give me each subagent prompt to run in a
fresh session instead.

PIPELINE (stop for my approval at each ⏸):
 P0 SOURCE MAP: one subagent lists every reachable source, its date range and volume
    → 00-sources.md. Propose the split: quarters × source groups, sized so no single
    subagent has more than it can read carefully (split further if a quarter is heavy). ⏸
 P1 HARVEST: one HARVESTER per (quarter × source group). Run in parallel where possible.
 P2 DIGEST: one DIGESTER per quarter, once all of that quarter's harvests are done.
 P3 AUDIT: one AUDITOR per quarter. If it finds misses, send a targeted harvester and
    re-digest. Repeat until the auditor reports no material gaps (max 2 rounds per quarter).
 P4 LEADS SWEEP: run targeted harvesters on everything in LEADS.md. Repeat until nothing
    new turns up.
 P5 CROSS-CHECK: one CROSS-CHECKER compares everything against perf reviews, feedback,
    promo docs and BRIEF.md "What I remember". Anything missing → harvest it. ⏸
 P6 SYNTHESIZE: propose the project list (10–25 projects/themes, plus a
    "misc/operational" bucket) ⏸. Then one SYNTHESIZER per project.
 P7 INTERVIEW: hand off to the INTERVIEWER (Part E) with me, one project per session.
    New leads from the interview → targeted harvest → re-synthesize that project.
 P8 FINAL COMPLETENESS INTERVIEW (Part E, final round). ⏸
 P9 EXPORT: SANITIZER, then REDACTION REVIEWER. ⏸ I approve every redaction.

Start with P0.
