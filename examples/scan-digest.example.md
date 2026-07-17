# Example scan digest (sanitized real output)

> Scan window: last 14 days, 2 repos.
>
> **Lessons added to pool (10):**
> 1. Refused a 50% cost cut on the user-facing path: Batch API is ~24h turnaround and latency IS the product (D-055)
> 2. The cost optimization CAUSED a data gap: cache-hit users stranded at a partial enrichment tier; fix cost $0 (d6c0e7c)
> 3. Batch run failed at the END, after 100% of LLM spend: idle DB socket dropped by the platform proxy (e8e75ed)
> 4. Cross-cutting invariant enforced by hand-copied WHERE clause leaked on the first attempt: 3 places implemented, 7 missed (4d3beac)
> 5. Default 5s transaction timeout: a ~200-item write died at 5.3s; latent bug only large accounts would find (c53f53f)
> 6. "Generated view" with no generator: an LLM re-authoring pass churned 148 lines on a prose-only change (f613245)
> 7. Ranked ideas on a rubric, then overrode the top score in writing, reasons logged (IDEAS.md:47)
> 8. Source-quality ranking as a written rule; two ideas killed on citation alone (STRATEGY.md:38)
> 9. Shipped a knowingly-inert iOS entitlement at 14:30, stripped it at 15:27 (1679da5 -> bb2202e)
> 10. A hardcoded credibility promise forced a better data model than a free hand would have (D-056)
>
> **Opportunities appended to IMPROVEMENTS.md (7):**
> 1. Real dashboard generator to replace the LLM re-authoring pass (evening)
> 2. Stale-view detector for generated artifacts (hour)
> 3. Blank-gate detector for empty spec sections (hour)
> 4. Attach the consolidation run to a trigger that actually fires (hour)
> 5. /fewer-permission-prompts pass on accreted settings (hour)
> 6. Cross-repo link checker for doc references (hour)
> 7. Permission allowlist audit (hour)
>
> **Flagged stale:** IMPROVEMENTS.md header claims weekly cadence; last touched 102 days ago. Cadence claim updated to "consolidated on each scan."
