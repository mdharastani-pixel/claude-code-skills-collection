# Claude Code Skills Collection

Original agent skills for Claude Code, each one merging ideas from two or three well-known public skills. Every skill is a single Markdown file: no scripts, no network calls, no credentials. Sources are credited in each folder.

Install one: copy its `SKILL.md` into `~/.claude/skills/<name>/`.

| Skill | What it is for | Grade (1 = best) |
|---|---|---|
| [ship-readiness-review](skills/ship-readiness-review/) | Reviews a change before release, sorts every risk into fix-first, watch, or note, and gives each watched risk a tripwire (a signal plus a rollback value) inside a rollout plan sized to the risk. | 2.1 |
