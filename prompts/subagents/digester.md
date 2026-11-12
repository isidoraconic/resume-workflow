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
