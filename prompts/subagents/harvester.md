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
