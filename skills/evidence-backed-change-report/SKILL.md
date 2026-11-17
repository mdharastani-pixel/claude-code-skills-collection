---
name: evidence-backed-change-report
description: Use when writing or reviewing a pull request description, release note, or change summary that says a change is faster, smaller, fixed, safer, or looks different, or when a reviewer asks for proof. Phrases: "write up this PR with before/after numbers", "how do you know it's faster", "back these claims with evidence".
---

# Evidence-Backed Change Report

You are the auditor of a receipt drawer: each claim in the description is a purchase, and a claim with no receipt is returned to the shelf. When you finish, the user has a change description whose top line contains only claims backed by a matched before/after receipt, plus a ledger that shows where each receipt came from.

The central idea is the **Receipt Rule**: no receipt, no claim. A receipt is one piece of evidence tied to one claim. It records the revision, the procedure, the environment, the date, and the sample size.

## Rules

1. **Fix claims first.** Before you measure anything, write two to five numbered claims in the form "X improves Y for workload Z". If you write the summary first, you will go looking for evidence that fits it and pick only the results that agree.
2. **Pair each claim with one receipt type.** Decide what would prove the claim: a benchmark, a test that failed before and passes now, a rendered image pair, a log excerpt, or a size report. Move any claim nothing could prove into a "rationale" section, so opinions don't pass as findings.
3. **Reuse existing receipts.** Look at CI output, earlier runs, and bot comments before you measure, and cite them where they apply. This avoids repeating work. A bot comment alone still does not give the specific before/after that a claim needs.
4. **Measure both sides the same way.** Run the base revision and the changed revision on the same machine, input, configuration, and repetition count. Keep the two results separate, and clear stale caches. A fresh run compared against an old number mixes in drift from the machine and the data.
5. **Stamp provenance on every artifact.** Note the revision, the procedure in words, the environment, the date, and the run count. Label any value that is secondhand or read by hand. A number with no source cannot be checked again.
6. **Keep four layers separate.** Use Observations (raw results, no adjectives), Interpretation (the cause you suspect), Recommendations (what the reviewer should do), and Open questions. Words like "because" in the observations quietly turn a guess into a fact.
7. **Report nulls and contradictions.** If before and after match, say whether the change has no effect on that property or the measurement missed it. Weaken or withdraw any claim that a result goes against. A buried regression costs you the reviewer's trust once someone finds it.
8. **Name what you could not measure.** List each surface you could not capture. Give a proxy if one exists, and describe a way for a human or CI to verify it. Otherwise "unverified" looks the same as "fine".
9. **Look at the published view.** Open the rendered description and confirm that each image loads and each number is readable. A broken embed means the claim has no evidence.

## Ledger format

| # | Claim (property, direction, condition) | Receipt type | Before | After | Provenance | Status |
|---|---|---|---|---|---|---|

Status is one of: supported, weak, contradicted, unverified. Only claims marked supported may appear in the summary sentence at the top.

## Worked example

Weak version:
"This PR makes the search page much faster and doesn't affect memory. Tested locally, looks great."

Better version:
"Summary: p99 latency for read-heavy search drops from 42 ms to 31 ms (claim 1, supported).
Observations: claim 1, base vs head, same host, same dataset, 5 runs each, spread ±2 ms. Claim 2, heap 210 MB before and 211 MB after, single run.
Interpretation: the latency drop is probably due to the new result cache.
Open questions: claim 2 is weak with n=1. Behavior on the legacy browser is unverified. As a proxy, the polyfill test suite passes, and a manual check is needed on that browser."

What changed: the vague "much faster" became one claim with a condition and a matched receipt, the cause moved out of the results, and the gaps are stated instead of hidden behind "looks great".

## Final reply

Return, in this order:
1. A one-sentence summary that uses only claims marked supported.
2. The numbered claims.
3. The completed ledger table.
4. The four layers: Observations, Interpretation, Recommendations, Open questions.
5. A last line in the form: "Not checked: <surfaces, claims, or conditions left unmeasured, or 'nothing'>."

## Excuses to reject

| Excuse | Correct response |
|---|---|
| "One run already shows the speedup." | Report the run count and the spread. With n=1 the status is weak at best. |
| "I measured the base last week, so that's fine." | Run the base again now, under the same conditions as the head run. |
| "The screenshot change is obvious, so I'll just describe it." | Embed the image pair, or mark the claim unverified. |
| "The bot already posted benchmark numbers." | Cite them, then confirm they cover this exact claim and include a before/after. |
| "The memory regression is minor, so I'll leave it out." | Put it in the ledger as contradicted or as a stated trade-off. |
| "Everyone knows the cache caused it." | Put that in Interpretation, not Observations. |
| "I can't test that platform, so I'll skip mentioning it." | Name it, give a proxy, and describe how to verify it. |

## When not to use

Skip this for changes that make no behavioral or measurable claim, such as pure renames, comment edits, or formatting.

## Self-check

- Did I write the claims before I gathered any measurements?
- Does every numbered claim have exactly one ledger row with a status?
- Were base and head measured under the same stated conditions, and does each artifact show its revision, environment, and run count?
- Is the Observations layer free of causal words like "because", "due to", or "thanks to"?
- Are null results, contradictions, and unmeasurable surfaces all reported?
- Did I check that every image and table renders in the published view?
