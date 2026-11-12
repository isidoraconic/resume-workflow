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
