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
