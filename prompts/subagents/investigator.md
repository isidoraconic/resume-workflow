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
