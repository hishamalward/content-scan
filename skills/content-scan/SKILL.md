---
name: content-scan
description: Mine your own repos for lessons learned and workflow-friction opportunities. Lessons feed a content pool (for posts, talks, blogs); opportunities feed an improvements backlog. Run on demand, typically every 1-2 weeks or after finishing a phase of work.
---

# content-scan: harvest lessons and opportunities from your own work

You are harvesting two things from the user's repositories: (1) post-worthy lessons for their content pool, and (2) efficiency opportunities (candidate skills, MCP servers, hooks, automations) for their improvements backlog.

## CONFIG (user: edit this block once)

- REPOS: the local repository paths to scan.
  - Example: /Users/you/projects/app-one, /Users/you/side-projects
- CONTENT_POOL: path to your content-pool.md (create from templates/content-pool.md in this repo if you do not have one).
  - Example: /Users/you/writing/content-pool.md
- IMPROVEMENTS: convention for opportunity capture. Default: append to an IMPROVEMENTS.md at each scanned repo's root if present; otherwise list opportunities in the reply only.

## Procedure

1. Determine the scan window: since the newest `content-scan YYYY-MM-DD` source tag in CONTENT_POOL; default to the last 14 days if none.
2. Gather signal from each repo in REPOS (for large repos, delegate to a read-only exploration subagent if available):
   - `git log` for the window: reverted approaches, bugfix clusters, "gotcha" commit messages, decision records, eval/benchmark results.
   - New or changed docs: status/plan files, learning notes, IMPROVEMENTS.md, agent-instruction files (CLAUDE.md and similar), postmortems.
   - Friction markers: repeated manual steps, TODO/HACK comments added in the window.
3. Extract LESSONS. The quality bar: concrete, quantified, non-obvious. Each lesson needs the thing that happened, the number or specific detail that makes it real, and why a builder audience would care. Generic takes ("testing is important") are not lessons; discard them.
4. Extract OPPORTUNITIES, with pattern recognition, in three passes:
   a. Collect friction candidates: repeated manual steps, TODO/HACK comments, copy-paste rituals, "generated" artifacts maintained by hand, cadence promises that lapsed.
   b. Recognize patterns: for each candidate, look across ALL scanned repos and beyond the current window for recurrences of the same friction class. A friction that occurred once is a note for the digest, not an opportunity; tooling is justified by recurrence.
   c. Check what already exists before recommending anything new: list the user's installed skills (~/.claude/skills/), project commands (.claude/commands/), and installed plugins. If existing tooling covers the friction, the recommendation is USE (name it), not CREATE.
5. Write results:
   - Lessons: append as new rows to the CONTENT_POOL table (status: seed; source: content-scan YYYY-MM-DD plus the commit/doc reference). Dedupe against existing rows and drafted content first.
   - Opportunities: per the IMPROVEMENTS convention, one structured block each (brevity was tried and produced entries too thin to act on):

     ```
     ### <short imperative name>
     - Friction: what keeps happening, one sentence
     - Evidence: 2+ concrete occurrences (commits, files, dates); same citation rule as lessons
     - Pattern: the friction class (manual sync, repeated lookup, missing gate, copy-paste ritual, hand-maintained "generated" artifact)
     - Recommendation: USE <existing skill/tool> | CREATE skill <proposed name: trigger, inputs, outputs, 3-line behavior sketch> | hook | MCP server | script
     - Effort: hour / evening / weekend · Recurs: how often the friction actually bites
     ```
6. Consolidate each touched IMPROVEMENTS.md while you are there (calendar cadences do not survive contact with life; consolidation runs whenever the scan runs): dedupe and merge near-duplicates, mark since-implemented items done with a pointer to the evidence, flag items untouched 60+ days for a keep/kill decision, and re-rank open items (quick wins first, then by friction frequency).
7. Reply with a compact digest: N lessons added (one line each), N opportunities (one line each), plus any flagged stale items.

## Rules

- Never invent or embellish. Every claim traces to a commit, doc, or artifact you actually read in this scan. Half-remembered claims get marked "pending verification" in the pool, never stated as fact.
- Respect confidentiality boundaries: personal-repo lessons are unrestricted; anything from an employer's code or data stays concept-level or is excluded. When in doubt, exclude and say so in the digest.
- Do not draft full posts during a scan; drafting is a separate pass over the pool.
