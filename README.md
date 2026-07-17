# content-scan

A [Claude Code](https://claude.com/claude-code) skill that mines your own repositories for two things you keep losing:

1. **Lessons learned** worth writing about (posts, talks, blogs), appended to a content pool you own.
2. **Workflow friction** worth tooling away (candidate skills, MCP servers, hooks, automations), appended to an improvements backlog.

## Why

Most technical content online is opinion. The interesting material (the bug that cost real money, the eval that contradicted the pricing page, the invariant that leaked on the first attempt) is sitting in your git history and your notes, and you forget it within two weeks. This skill runs through recent commits, docs, and decision records and pulls out the receipts.

The quality bar is enforced in the skill itself: concrete, quantified, non-obvious. "Testing is important" gets discarded. "The batch run failed after 100% of the LLM spend because an idle DB socket got dropped" gets captured, with the commit hash.

## Install

```bash
# copy the skill into your Claude Code user skills
cp -r skills/content-scan ~/.claude/skills/
```

Then edit the CONFIG block at the top of `~/.claude/skills/content-scan/SKILL.md`:
your repo paths, your content-pool file location (start from `templates/content-pool.md` if you do not have one), and your improvements convention.

## Use

In any Claude Code session:

```
/content-scan
```

Run it every week or two, or after finishing a phase of work. You get a digest of what was found; lessons land in your pool as seeds, opportunities land in the relevant repo's `IMPROVEMENTS.md`. Drafting actual posts from the pool is deliberately a separate pass.

## What a digest looks like

See `examples/scan-digest.example.md` for a real (sanitized) output: 10 lessons and 7 opportunities harvested from two repos in one run, each traced to a commit or doc.

## Design notes

- **Capture is manual-first; the scan is a supplement.** The pool is a plain markdown table you also append to by hand whenever something fascinates you. The habit is the asset; the skill just makes sure the repo evidence does not slip through.
- **Consolidation is attached to the scan, not the calendar.** The skill also tidies each `IMPROVEMENTS.md` it touches (dedupe, mark done, flag stale), because "weekly review" files famously go 100+ days untouched.
- **Confidentiality is a rule, not a hope:** employer material stays concept-level or is excluded; the skill says so when it excludes.

## License

MIT
