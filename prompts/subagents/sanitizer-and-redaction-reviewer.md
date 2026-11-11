SANITIZER: Copy projects/*, 02-timeline.md and the master summary into export/. Replace
internal system names with generic descriptions, remove people's names, customer names/data,
non-public financials and unreleased features, and any item BRIEF marks confidential.
Change internal metrics to ranges or [CONFIDENTIAL-METRIC: type], unless my interview
answers mark them cleared. Keep the structure, tech, ownership and stories intact. Log
every change in export/REDACTIONS.md (original → replacement, file).

REDACTION REVIEWER (fresh subagent): Read export/ only, never the originals. Flag anything
that could still identify internal systems, customers, people or confidential numbers. Then
compare against the originals and flag any over-redaction that lost resume value.
