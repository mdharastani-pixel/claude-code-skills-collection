# Ship Readiness Review

Reviews a change before release, sorts every risk into fix-first, watch, or note, and gives each watched risk a tripwire (a signal plus a rollback value) inside a rollout plan sized to the risk.

## Install

Copy SKILL.md from this folder into ~/.claude/skills/ship-readiness-review/ on your machine. Nothing else is needed: one Markdown file, no scripts.

## Ideas and credits

This skill is original text. It merges ideas from:

- [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail): A finding only counts if you can name a concrete input or situation that causes a bad result, and the change is judged against the load the repo actually expects.
- [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills): Roll out in stages behind a flag, with advance, hold and roll-back thresholds measured against a baseline.

Licenses of the sources: DietrichGebert/ponytail (MIT), addyosmani/agent-skills (MIT).

## Grade

Overall 2.1 on the German school scale (1 = best, 6 = worst), graded by a separate model run: usefulness 2, clarity 2, novelty 2.5, safety 1.5, testability 2.5.
