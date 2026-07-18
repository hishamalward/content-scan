# Example scan digest (sanitized real output, v2 format)

> Scan window: since last scan tag, 2 repos.
>
> **Lessons added to pool (8). Each cites its artifacts; three shown:**
> 1. Push-to-deploy silently died after a GitHub username rename: the deploy platform's linkage still pointed at the old org while the remote moved; 3 days stale before merge day exposed it. One CLI re-link fixed source and triggered a deploy (081e8cf, 6f72f4a)
> 2. A reconciliation fix shipped with a reviewer-caught bug: the anchor only advanced on rounds that booked at least one event, so a zero-booking round permanently under-counted (delta-from-moving-snapshot vs running-deficit). Fix: store {counts, at}, not a bare count map (b6a290f, 64edb32)
> 3. Two-stage rescue cascade (cheap fuzzy match, then LLM only on the ambiguous remainder): 82 flagged from 449 rejects, 3 false positives on founder review, and all 3 came from the fuzzy-only bucket; the LLM-confirmed bucket was 100% clean (34f68d0)
>
> **Opportunities (structured; one shown in full):**
>
> ### Build a deterministic dashboard generator
> - Friction: dashboard.html claims to be a generated view but regeneration is an LLM re-authoring pass that drifts every time.
> - Evidence: commit f613245 (prose-only sync churned 148/49 HTML lines vs 116 across all md sources, including unprompted CSS refactoring); README.md:18 ("never edit directly").
> - Pattern: hand-maintained "generated" artifact.
> - Recommendation: CREATE script build_dashboard.py: input the three md sources, output HTML via a fixed template; zero churn on prose-only changes.
> - Effort: evening · Recurs: every content sync.
>
> Other verdicts this run: permission allowlist audit → USE /fewer-permission-prompts (already installed); blank kill-gate detector → CREATE (grep script; a gate went stale within 24h of being written); stale-view detector → resolved without a build (zero observed drift; folded into the generator entry).
>
> **Consolidation:** 1 done-item checkbox fixed; 2 entries resolved without building; 8 items untouched 100+ days flagged for a keep/kill call. Header cadence claim corrected to "consolidated on each /content-scan run."
