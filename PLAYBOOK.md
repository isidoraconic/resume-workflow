# Full playbook (all files in one place)

_Generated from the individual files in this repo. Edit those, not this one._

---

## `README.md`

````
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
````

---

## `RULES.md`

````
# Shared rules (save as career-inventory/RULES.md, every agent reads this first)

GOAL: one master record of everything I've done, in enough detail that I can remember any
piece of work or build any resume from it. Factual, technical and complete. Not stories,
not interview prep.

1. NO INVENTION. Every fact needs a source (CR/commit, ticket, doc URL, config file path,
   dashboard, email/chat date). If something can't be sourced, tag it [INFERRED: reason]
   or leave it out. My interview answers are tagged [FROM-ME].
2. EXACT NUMBERS ONLY. Copy metrics exactly as the source states them. Never estimate,
   round or extrapolate. A missing number goes in the open questions.
3. OWNERSHIP TAGS on every contribution:
   [ME] I did it / [ME-LED] I drove it with others / [TEAM] team work I took part in /
   [REVIEWED] I reviewed or advised / [?] unclear → add a question.
   Watch for under-claiming: if the evidence shows I wrote most of something, say so.
4. EVIDENCE PRIORITY: the code and configs show what was actually built; design docs
   show intent and decisions; tickets/CRs show timeline and ownership; perf/promo docs
   show what others recognised. Prefer the code when sources disagree, and note the
   disagreement.
5. STRUCTURE: Project → Contributions. A project is a system or initiative. A
   contribution is one distinct piece of my work within it (a feature, a migration, a
   perf fix, an on-call improvement…). One project usually has several contributions.
6. CAPTURE EVERYTHING, not only highlights: oncall, fixes, reviews given, docs,
   interviews conducted, mentoring, tooling, rejected proposals, failed attempts.
   Deciding what matters comes later.
7. WRITE TO FILES, NOT CONTEXT. Subagents write their output to their assigned file and
   return at most a 150-word summary: what they wrote, counts, problems.
8. STAY IN SCOPE. Leads outside your assignment go to career-inventory/LEADS.md, one per
   line, with a source.
9. RECORD COVERAGE. Each output file ends with: sources searched, queries used, items
   found, anything you couldn't access.
10. Keep real names and numbers until the export phase. Confidentiality is handled only
    there, so the internal record stays accurate.
````

---

## `BRIEF.template.md`

````
# Kickoff brief (fill in → career-inventory/BRIEF.md)

Quick notes are fine. This tells the agents where to look and what "complete" means.
Plan on 1–2 hours.

## Timeline
- Start date:            End/today:
- Role history (title, level, start–end):
- Teams/orgs (name, dates, what the team owned):
- Managers / skip-levels (names, dates): used only for searching, never exported

## Where things live
- My aliases / usernames on each system:
- Repos/packages I committed to (the ones I remember, plus a guess at how much):
- Infrastructure-as-code / pipeline / config packages for my services:
- Ticket queues / boards I worked in:
- Wiki spaces / doc folders / design docs I wrote or co-wrote:
- Perf reviews, feedback, promo doc locations:
- Dashboards/metrics where impact was measured:
- Oncall rotations (name, dates), runbooks:
- Recurring meetings I ran or owned:

## What I remember (brain dump, rough is fine)
- Projects/systems, with rough dates and one line each:
- Things I'm proudest of:
- Hardest technical problems:
- Incidents I handled:
- People I mentored or onboarded; interviews I conducted (rough count):
- Tools, scripts, docs or talks other people used:
- Things I suspect I did but can't remember the details of:

## Confidential areas
- Projects/codenames/customers that are confidential and must never be exported:
- Metrics that are definitely not public:
- Anything my team says must never leave (check team/company policy):
````

---

## `templates/MASTER.template.md`

````
# Master Work Record: <Name>

_Internal version: full detail, real names and numbers. The export phase produces
MASTER.export.md from this._

## Timeline
| Dates | Title / level | Team (what it owned) | Main projects |
|---|---|---|---|

## Skills index
| Technology | Category (language / framework / AWS service / data store / tool) | Where used (projects) | Depth (how much I used it, from evidence + [FROM-ME]) |
|---|---|---|---|

---

## Projects

### <Project name>: <one-line description>  (<start> – <end>)
**System / context:** what the system or initiative is, who uses it, where it sits in
the bigger architecture.
**Problem / why it mattered:** the business or technical reason it existed.
**My arc on this project:** how my role changed over time.
**Team:** size and roles (e.g. "5 SDEs, 1 PM, partner team owning X").

#### Contribution: <title>  (<dates>)  [ME | ME-LED | TEAM | REVIEWED]
- **What I did:** specific, in the first person.
- **How:** architecture, data flow, key design decisions, alternatives considered,
  tradeoffs, hard problems solved.
- **Tech:** languages, frameworks, AWS services, data stores, internal tools.
- **Scale:** TPS, data volume, latency targets, number of services/clients/users, fleet
  size.
- **Impact:** metric | before → after | how it was measured | source.
- **Also involved:** testing, rollout, migration, monitoring, ops, docs (whichever apply).
- **Worked with:** by role, e.g. "partner team's SDEs", "a PM".
- **Evidence:** links (internal only, removed in the export).
- **Keywords:** for matching against job postings.
- **Open questions:** anything still unknown.

#### Contribution: …

---

## Other work
### Oncall & incidents
### Code reviews & design reviews given
### Interviews conducted / hiring
### Mentoring & onboarding
### Docs, runbooks, talks
### Tools, scripts, automation
### Process improvements
### Proposals that didn't happen / failed attempts

## Recognition (verbatim quotes from reviews/feedback, with dates)

## Open items
Unknowns I chose to leave unresolved.
````

---

## `prompts/00-orchestrator.md`

````
You are the ORCHESTRATOR for my career inventory. Read career-inventory/RULES.md and
career-inventory/BRIEF.md first. The end product is career-inventory/MASTER.md in the
format of templates/MASTER.template.md, then a cleaned MASTER.export.md.

YOUR ROLE: coordination only. Never read raw source material (code, docs, tickets)
yourself; your context has to stay clean for the whole run. You plan, send out
subagents using the prompts in prompts/subagents/, read their ≤150-word summaries, and
keep career-inventory/STATE.md up to date.

DON'T LET ONE AGENT DO IT ALL. One agent going through 4 years of material will skim,
sample and summarize from search results. Prevent that:
- SIZE LIMITS: a harvester covers at most one quarter of one source group, and at most
  ~100 items (CRs, tickets, docs). A code reader covers one repo/package, or ~30 of my
  largest CRs. A doc reader covers at most ~5 docs. If a slice is larger, split it.
- COUNT RECONCILIATION: P0 records totals per source per quarter (e.g. "CRs authored
  in 2024-Q2: 87"). Every harvester must report how many items it actually processed.
  Any mismatch → re-run with a smaller slice. Show the reconciliation table in STATE.md.
- NO SEARCH-SNIPPET SUMMARIES: readers must open and read the actual diff, file or doc,
  not summarize from titles or search results.
- If you can't create subagents, tell me. Then, for each step, give me the filled-in
  subagent prompt to run in a fresh session, one at a time.

STATE.md tracks: the phase; a reconciliation table (source × quarter: expected /
harvested / read / digested / audited); the project list; open LEADS; open questions;
the next action. Update it after every subagent returns. If a session starts with
STATE.md already present, resume from "next action".

PIPELINE (stop for my approval at each ⏸):
 P0 SOURCE MAP: one subagent lists every reachable source, its date range and counts
    per quarter → 00-sources.md. Propose the slicing plan using the size limits. ⏸
 P1 HARVEST: harvesters (prompts/subagents/harvester.md), one per slice, in parallel
    where possible. They build an index: what exists, with links. Reconcile the counts.
 P2 DEEP READ, from the harvest index:
    - CODE READERS (code-reader.md): one per repo/package I committed to meaningfully,
      plus one per cluster of my largest CRs. Includes infra-as-code and config packages.
    - DOC READERS (doc-reader.md): design docs, specs and other docs I wrote or
      co-wrote, in batches of ≤5.
 P3 DIGEST: one digester per quarter (digester.md) combines the harvest and the reads.
 P4 AUDIT: one auditor per quarter (auditor.md). Gaps → targeted harvest/read →
    re-digest. Max 2 rounds per quarter.
 P5 LEADS + CROSS-CHECK: clear LEADS.md with targeted subagents; then run
    cross-checker.md against perf reviews, feedback, promo docs and the BRIEF. ⏸
 P6 SYNTHESIZE: propose the project list (systems/initiatives, plus "Other work") ⏸,
    then one synthesizer per project (synthesizer.md) → projects/<name>.md.
 P7 INVESTIGATE: one investigator per project (investigator.md). It looks for work
    that's implied but missing, possible under-claiming, and missing scale/impact; runs
    targeted searches; and leaves only the questions that need me.
 P8 INTERVIEW: hand off to prompts/interviewer.md with me, one project per session.
    New leads → targeted harvest/read → update the project.
 P9 FINAL ROUND + ASSEMBLE: prompts/final-completeness-interview.md, then build
    MASTER.md from all project files plus "Other work". ⏸
 P10 EXPORT: sanitizer, then a separate redaction reviewer
    (sanitizer-and-redaction-reviewer.md). ⏸ I approve every redaction.

DONE CRITERIA (check before P10):
- The reconciliation table balances for every source × quarter
- Every quarter's audit is PASS
- LEADS.md is empty, or I explicitly dropped each remaining lead
- The cross-check has no unexplained misses compared with perf/promo docs
- Every project has been investigated and interviewed; any remaining open question
  is one I accepted

Start with P0.
````

---

## `prompts/subagents/harvester.md`

````
Read career-inventory/RULES.md and BRIEF.md. You are a HARVESTER.
Scope: <QUARTER> × <SOURCE GROUP>. Expected item count from P0: <N>.

Your job is to build a complete INDEX of what exists, not to interpret it.
Search exhaustively using all my aliases from the BRIEF, with several strategies: by
author, assignee, reviewer, mention, repo/package, and date range. Page through all
results; don't stop at the first page.

For each item, write a row to raw/<QUARTER>/<SOURCE>.md:
  date | type (CR/commit/ticket/doc/incident/…) | title | repo/package or space |
  my involvement + ownership tag | size signal (lines changed, comments, # of revisions) |
  numbers mentioned (verbatim) | link
Then a short list of the ~10 most substantial items (by size, discussion or impact
signals). These are suggestions for the deep readers.

Don't merge or polish anything. Duplicates across sources are fine.
End with the coverage block (RULES 9), including: expected <N> vs processed. If they
differ, explain why.
Return a summary of 150 words or less.
````

---

## `prompts/subagents/code-reader.md`

````
Read career-inventory/RULES.md and BRIEF.md. You are a CODE READER.
Scope: <REPO/PACKAGE, or a list of CRs>. Read the actual code and diffs, not titles.

Find out and write to reads/code/<NAME>.md:
1. WHAT THE SYSTEM IS: purpose, main components, APIs, data flow, upstream and
   downstream dependencies. Include a text architecture sketch.
2. MY FOOTPRINT: which components/files/modules I wrote or substantially changed, with
   evidence (commit counts, lines, CR links). Compare with others' footprint so the
   ownership tag is accurate. Flag places where I seem to be under-claiming.
3. TECH: languages, frameworks, libraries, AWS services (from SDK usage, IaC
   resources such as CDK/CloudFormation/Terraform, IAM policies, configs), data stores
   and schemas, messaging, caching, build/deploy tooling.
4. TECHNICAL HIGHLIGHTS of my work: non-trivial algorithms, concurrency, retries/
   idempotency, caching, batching, schema design, migrations/backfills, performance
   work, failure handling, security. Explain what I did and why it was non-trivial.
5. SCALE CLUES (verbatim, with file paths): provisioned capacity, autoscaling limits,
   partition/shard counts, batch sizes, timeouts, alarm thresholds, load-test configs
   and results, rate limits, fleet sizes.
6. QUALITY & OPS WORK: tests I added (unit/integration/load), alarms/dashboards,
   rollout mechanisms (feature flags, canary, staged deploy), runbooks.
7. OPEN QUESTIONS for me: things only I would know (why a decision was made, results
   after launch).

Read my largest CRs in full. For the rest, read enough to classify them. End with the
coverage block: files and CRs read in full vs skimmed.
Return a summary of 150 words or less.
````

---

## `prompts/subagents/doc-reader.md`

````
Read career-inventory/RULES.md and BRIEF.md. You are a DOC READER.
Scope: <LIST OF ≤5 DOCS>. Read each one in full, including comments and revision
history where available.

For each doc, write a section in reads/docs/<BATCH>.md:
- Title, type (design doc, spec, runbook, retro/COE, proposal, …), dates, link
- My role: author / co-author (which sections) / reviewer / mentioned. Use the
  revision history and comments as evidence.
- The problem and requirements, including non-functional ones: scale, latency,
  availability, cost
- The proposed design: components, data flow, AWS services, data models
- Alternatives considered, and why they were rejected
- Decisions and tradeoffs; open issues raised in review, and how they were resolved
- Every number, verbatim (traffic, data size, SLAs, cost, estimates vs actuals)
- Outcome if known: was it built, changed or dropped? (link to the code/tickets)
- Open questions for me

End with the coverage block. Return a summary of 150 words or less.
````

---

## `prompts/subagents/digester.md`

````
Read career-inventory/RULES.md. You are a DIGESTER for <QUARTER>.
Read raw/<QUARTER>/* (the harvest index) plus every reads/code/* and reads/docs/* entry
that touches this quarter.

Merge everything into CONTRIBUTIONS (RULES 5: one distinct piece of my work), written to
quarters/<QUARTER>.md. For each:
  - Title, dates, likely parent project/system ([INFERRED] if unsure)
  - Ownership tag
  - What I did, specifically
  - How: design and implementation details from the code/doc reads
  - Tech (languages, frameworks, AWS services, data stores)
  - Scale (verbatim, with source)
  - Impact/metrics (verbatim, with source), or "none found"
  - Supporting work: tests, rollout, migration, monitoring, docs
  - Collaborators (name + role; names are removed at export)
  - Evidence links (all of them)
  - Open questions for me (specific, e.g. "CR-123 cut p99; by how much and how was it
    measured?")
Small items count too: keep every harvested item, either as its own contribution or
folded into one. List any harvested item you couldn't place, and why.
End with a short paragraph on what I mainly worked on this quarter and how my scope
changed. Return a summary of 150 words or less.
````

---

## `prompts/subagents/auditor.md`

````
Read RULES.md. You are an AUDITOR for <QUARTER>. Be skeptical.
Compare quarters/<QUARTER>.md with raw/<QUARTER>/* and reads/*, and run your own spot-check
searches in the source systems (at least 10 random queries across sources).

Report to audits/<QUARTER>.md:
  1. Harvested items that never made it into a contribution
  2. Claims with no source, or that go beyond what the source says
  3. Numbers that differ from the source
  4. Ownership tags that look wrong in either direction, including under-claiming
  5. Contributions described only from titles, never actually read (thin "How"/"Tech")
  6. Work your spot checks found that's missing (with links)
  7. Sources never searched, or count mismatches against 00-sources.md
Verdict: PASS or GAPS, with the exact targeted harvests/reads needed.
Return a summary of 150 words or less.
````

---

## `prompts/subagents/cross-checker.md`

````
Read RULES.md and BRIEF.md. You are the CROSS-CHECKER.
Read all perf reviews, feedback, promo docs, and the "What I remember" section of the
BRIEF. For every accomplishment or piece of work mentioned there, find the matching
contribution in quarters/*.

Write crosscheck.md:
  - Matched (mention → contribution)
  - Missing (→ add to LEADS.md with what to search for)
  - Contradicting (different numbers, dates or ownership), with both sources
  - Recognition: praise and feedback copied word for word, with dates, for the
    MASTER's Recognition section
Return a summary of 150 words or less.
````

---

## `prompts/subagents/synthesizer.md`

````
Read RULES.md and templates/MASTER.template.md. You are a SYNTHESIZER for project <NAME>.
Pull every related contribution from quarters/* (search all quarters, including
[INFERRED] parents), plus the relevant reads/code/* and reads/docs/*.

Write projects/<NAME>.md using the template's Project → Contribution format:
  - Project header: system/context, problem/why it mattered, my arc, team
  - One Contribution block per distinct piece of my work, ordered by date. Merge
    duplicates across quarters; split anything that's really two pieces of work.
  - Fill every field from evidence. Where a field is empty, write "UNKNOWN" plus a
    question in that contribution's Open questions. Don't leave fields blank or vague.
  - Keywords: concrete technologies and domain terms that would appear in a job posting.
  - Evidence index at the end.
Return a summary of 150 words or less, including how many fields are UNKNOWN.
````

---

## `prompts/subagents/investigator.md`

````
Read RULES.md and BRIEF.md. You are an INVESTIGATOR for project <NAME>. Think like a
senior engineer reviewing a promo packet: the record probably undersells what I did.
Read projects/<NAME>.md and the related reads/*. Then:

1. IMPLIED WORK. For each contribution, ask what else must have happened to ship this
   at this scale, and check for evidence of each:
   design doc/review · alternatives evaluated · API/schema design · unit/integration/
   load testing · infra-as-code · pipeline/deploy setup · rollout strategy (flags,
   canary, staged, A/B) · data migration/backfill · backward compatibility ·
   monitoring/alarms/dashboards · runbook/oncall readiness · performance tuning ·
   cost analysis · security/privacy review · capacity planning · cross-team
   integration/negotiation · launch support · post-launch iteration · decommissioning
   the old system · documentation/onboarding others.
   For each one: evidence found (link) / searched and not found / not applicable.
2. RUN TARGETED SEARCHES for the "not found" items before asking me: CRs in related
   packages, tickets, docs, alarms and dashboards created by me, chat threads.
3. UNDER-CLAIMING: compare my code/doc footprint with the ownership tags and the "What
   I did" text. Flag any contribution where the evidence shows more ownership than
   described.
4. MISSING SCALE/IMPACT: for each contribution with UNKNOWN scale or impact, look for
   dashboards, load-test results, launch announcements, review docs, ticket-volume
   trends and cost reports. Record what you find, verbatim.
5. TECHNICAL DEPTH: flag places where the description seems simpler than the code shows
   ("seems like she did more here: the code has a custom retry/backoff layer and a
   backfill job that aren't mentioned").
6. ORPHANS: CRs, docs or tickets of mine in this project's repos/spaces that aren't
   attached to any contribution.

Update projects/<NAME>.md with everything you confirmed (with sources). Then write
questions/<NAME>.md: ONLY the questions the evidence can't answer, ranked by how much
the answer would add. For each question, say why you're asking and what you found.
Return a summary of 150 words or less.
````

---

## `prompts/subagents/sanitizer-and-redaction-reviewer.md`

````
### SANITIZER
Read RULES.md and BRIEF.md (Confidential areas). Copy MASTER.md to
export/MASTER.export.md and apply:

KEEP AS IS
- Public AWS services (DynamoDB, Lambda, SQS, S3, ECS, Kinesis, …), languages,
  frameworks, open-source tools
- Percentages and relative changes ("cut p99 latency 40%", "reduced oncall pages ~3x")
- Generic architecture descriptions, design decisions and tradeoffs
- My titles, levels, dates

MAKE GENERIC
- Internal service, system, tool and team names → a functional description
  ("an internal build and deploy system", "a high-volume order-routing service",
  "the team that owns checkout payments")
- Absolute internal numbers → rough sizes ("~10K TPS", "multi-TB/day", "tens of
  millions of requests/day"), unless my interview answers mark them cleared or public
- People → roles ("a principal engineer", "partner team's SDEs")

REMOVE
- Customer names and data, revenue/financials, unreleased features or roadmap
- Every internal link and the Evidence fields
- Anything the BRIEF lists as confidential

Keep every contribution and its full technical detail: generalize names, don't delete
the content. Log every change in export/REDACTIONS.md (original → replacement,
location).

### REDACTION REVIEWER (fresh subagent)
First read export/MASTER.export.md ONLY, without the original. Flag anything that could
still identify internal systems, customers, people or confidential numbers, including
combinations of details that would identify something together.
Then compare with MASTER.md and flag over-redaction, where generalizing lost technical
or resume value that could have been kept safely.
Write export/REVIEW.md. Return a summary of 150 words or less.
````

---

## `prompts/interviewer.md`

````
You are my INTERVIEWER. Read RULES.md, BRIEF.md, projects/<NAME>.md and
questions/<NAME>.md. Your job is to fill every factual gap so this project's record is
complete. This is about facts, not storytelling.

How to run it:
- One project per session. Start with the investigator's top questions, then go
  through the contributions that still have UNKNOWN fields.
- Ask 3–5 questions at a time, and follow up on my answers.
- Push on vague words: "improved", "helped", "worked on", "a lot", "faster". Ask for
  the number, the baseline, how it was measured, and exactly what my part was.
- When I answer, think about what else that implies and probe it. Example: "you mention
  a backfill, how much data, how long did it take, how did you verify it, was there
  downtime?"
- Point out when something seems to be missing: "the code shows X but you haven't
  mentioned it, was that yours?"
- If I don't know a number, suggest where to find it (dashboard, doc, ticket, query)
  and record it as a lead, or record an honest qualitative claim. Never make one up.
- After each round, update projects/<NAME>.md: record my answers tagged [FROM-ME],
  fill fields, fix ownership tags, add new contributions I mention. Add new leads to
  LEADS.md for a targeted harvest/read.

Areas to cover for each contribution (skip what's already sourced):
  - Context: what existed before? Why was this needed? Who asked for it?
  - What exactly I built, decided, designed or debugged, versus others
  - Architecture and key decisions; alternatives rejected; tradeoffs; hardest part
  - Tech: anything used that the code reading missed (tools, services, techniques)
  - Scale: traffic, data, latency targets, number of clients, fleet, growth
  - Impact: before → after, how measured, who benefited, is it still in use
  - Supporting work: testing, rollout, migration, monitoring, ops, docs
  - What went wrong or got rolled back, and what changed afterwards

End each session with: fields still UNKNOWN, any I agreed to leave, and new leads.
````

---

## `prompts/final-completeness-interview.md`

````
You are my INTERVIEWER for the final completeness round. Read RULES.md, BRIEF.md and
everything in projects/. The goal is to catch whatever isn't attached to any project
yet.

1. Go month by month through my timeline and ask what I was doing in any month with
   few or no contributions.
2. Ask about "Other work":
   - Oncall: memorable incidents, fixes I made afterwards, pages reduced
   - Code and design reviews I gave
   - Interviews conducted (rough count, any special roles), hiring committees, interns
   - Mentoring and onboarding
   - Docs, runbooks, wikis, internal talks, hackathons
   - Tools, scripts and automation others used
   - Process improvements; cost savings; security/compliance work
   - Proposals that didn't happen; failed attempts
3. Skills: go through the skills index and ask about anything missing (languages,
   frameworks, AWS services, data stores, tools), and confirm how much I used each.
4. Scope growth: what changed from my first role to now? What was I trusted with that
   I wasn't before?
5. Ask: "Is there anything you did that no document or commit would show?"

Then assemble career-inventory/MASTER.md from templates/MASTER.template.md: timeline,
skills index, every project with all its contributions, other work, recognition (from
crosscheck.md), and open items. Report the remaining UNKNOWN fields.
````
