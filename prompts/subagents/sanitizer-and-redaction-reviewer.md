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
