# Evidence-Backed Change Report

Turns a change description into a few testable, numbered claims, each backed by a like-for-like before/after measurement with its source recorded, and keeps what was observed separate from what it is taken to mean.

## Install

Copy SKILL.md from this folder into ~/.claude/skills/evidence-backed-change-report/ on your machine. Nothing else is needed: one Markdown file, no scripts.

## Ideas and credits

This skill is original text. It merges ideas from:

- [Orchestra-Research/AI-Research-SKILLs](https://github.com/Orchestra-Research/AI-Research-SKILLs): Phrase the contributions as numbered, testable claims in the form 'X is better for Y in environment Z', each mapped to the evidence that backs it.
- [yschimke/compose-ai-tools](https://github.com/yschimke/compose-ai-tools): Capture before/after evidence at the base and the changed revision, reuse existing CI output first, treat identical pairs as findings, and state openly which surfaces could not be captured.
- [AgriciDaniel/claude-ads](https://github.com/AgriciDaniel/claude-ads): Keep the provenance of every input and separate observations, diagnoses, recommendations, and uncertainties into distinct layers.

Licenses of the sources: Orchestra-Research/AI-Research-SKILLs (MIT), yschimke/compose-ai-tools (Apache-2.0), AgriciDaniel/claude-ads (MIT).

## Grade

Overall 2.2 on the German school scale (1 = best, 6 = worst), graded by a separate model run: usefulness 2, clarity 2, novelty 3, safety 1.5, testability 2.5.
