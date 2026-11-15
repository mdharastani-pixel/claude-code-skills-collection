# Style Passport: One Look, Many Screens

Turns a mood board into one fixed, reusable style block plus one generation prompt per screen slot, so a product's illustrations look like one consistent set without copying anyone's artwork.

## Install

Copy SKILL.md from this folder into ~/.claude/skills/style-passport-illustration-prompts/ on your machine. Nothing else is needed: one Markdown file, no scripts.

## Ideas and credits

This skill is original text. It merges ideas from:

- [wuyoscar/GPT-Image2-Skill](https://github.com/wuyoscar/GPT-Image2-Skill): Reverse-engineer reference images into a few visual anchors placed early in the prompt, with a medium fence and names translated into observable traits.
- [ckryptickunal/OpenDesigner](https://github.com/ckryptickunal/OpenDesigner): Agree a slot-by-slot shot list before producing art, color the art from the product's tokens, avoid lettering inside images, and treat results as placeholders.
- [Appllama/appllama-skills](https://github.com/Appllama/appllama-skills): Study references to extract the pattern rather than the pixels, so the result follows proven conventions without copying anyone's screen.

Licenses of the sources: wuyoscar/GPT-Image2-Skill (MIT), ckryptickunal/OpenDesigner (MIT), Appllama/appllama-skills (MIT).

## Grade

Overall 1.9 on the German school scale (1 = best, 6 = worst), graded by a separate model run: usefulness 2, clarity 1.5, novelty 2.5, safety 1.5, testability 2.
