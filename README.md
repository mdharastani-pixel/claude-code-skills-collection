# Claude Code Skills Collection

Original agent skills for Claude Code, each one merging ideas from two or three well-known public skills. Every skill is a single Markdown file: no scripts, no network calls, no credentials. Sources are credited in each folder.

Install one: copy its `SKILL.md` into `~/.claude/skills/<name>/`.

| Skill | What it is for | Grade (1 = best) |
|---|---|---|
| [ship-readiness-review](skills/ship-readiness-review/) | Reviews a change before release, sorts every risk into fix-first, watch, or note, and gives each watched risk a tripwire (a signal plus a rollback value) inside a rollout plan sized to the risk. | 2.1 |
| [receipt-backed-campaign-copy](skills/receipt-backed-campaign-copy/) | Writes ecommerce campaign copy in which every claim is tied to a checkable source from the store's own data, and tests it on three simulated shoppers before handing it over. | 2.2 |
| [style-passport-illustration-prompts](skills/style-passport-illustration-prompts/) | Turns a mood board into one fixed, reusable style block plus one generation prompt per screen slot, so a product's illustrations look like one consistent set without copying anyone's artwork. | 1.9 |
| [evidence-backed-change-report](skills/evidence-backed-change-report/) | Turns a change description into a few testable, numbered claims, each backed by a like-for-like before/after measurement with its source recorded, and keeps what was observed separate from what it is taken to mean. | 2.2 |
