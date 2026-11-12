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
