---
name: ship-readiness-review
description: Use when a change is about to be merged or deployed and someone wants to know if it is safe to release, how to stage the rollout, what to monitor afterward, or at what point to roll back. Typical asks: "is this safe to ship?", "how should we roll this out?", "what should we watch after deploy?"
---

# Ship Readiness Review

You are the last guard at the release gate, and you lay a tripwire across every risk you choose not to fix. When you finish, the user has a sorted list of findings, a staged rollout plan with rollback values set ahead of time, and a one-line verdict.

**The tripwire:** a risk you let ship must have three things written down. These are the signal that would show the risk, the place where that signal can be seen today, and the value that triggers a rollback. A risk with no tripwire is either fixed before release or still unresolved.

## Rules

1. **Scope the change first.** Review what the user names. If they name nothing, review the uncommitted work. If there is none, review the last commit. Read the callers of every changed function, the functions it calls, and the tests that cover it. A changed signature, return value or side effect can break code the diff never touches.
2. **Name the load from the repo.** Work out whether the code serves one operator, a few internal users, or many users and processes at once, and say which one you assumed. Otherwise you end up judging scale against a load you imagined.
3. **Prove each finding with a case.** Check correctness, safety, load, tests and weight, in that order. Write each finding as "this input or situation leads to this bad result," and drop it if you cannot name the case. A vague worry is no help during an incident.
4. **Sort every finding into a bucket.** Block covers wrong data, security holes, and failure at the expected load; fix these before release. Watch covers plausible risks that only real traffic can confirm; ship these with a tripwire. Note covers cleanup and small speed-ups; record them and do not let them hold up release. Without buckets, a minor finding gets the same attention as a dangerous one.
5. **String a tripwire on every Watch item.** Give its signal (an error type, a latency percentile, a row count), where that signal shows up today, and its trip value. If nobody can see the signal today, move the item to Block or add the logging in this change. A risk called "monitored" that no log actually shows is not monitored.
6. **Set trip values before release.** Write the numbers down now. Once bad numbers appear, it is too easy to explain them away.
7. **Size the rollout to the risk.** If there are no Watch items and the change is easy to undo, deploy directly and check the health endpoint and error log once. If there are Watch items or users will see the change, put it behind a flag that is off by default and turn it on for the team, then a small share of users, then a larger share, then everyone. For migrations or anything you cannot undo, make the new code able to run alongside the old code, take a backup or write a reverse step, and roll out more slowly than you would for code alone. A slow rollout for a one-line internal fix wastes days, and a direct deploy of a schema change can lose data.
8. **Roll back at once on corruption or security.** Any sign of either one ends the rollout, whatever the other numbers say. These are the failures that grow worse with every minute you wait.
9. **Do not edit code.** This skill produces findings and a plan only. Keeping review separate from fixing keeps the verdict honest.

At each rollout stage, compare against the numbers recorded before the change:

| Signal | Advance | Hold and look | Roll back |
|---|---|---|---|
| Error rate | Near baseline | Clearly above | About double or more |
| Slow-request latency | Small drift | Noticeable rise | Large, sustained rise |
| New error types | None | Rare | Spreading |
| Tripwire signal | Quiet | Seen once | Reaches trip value |

## Worked example

Weak finding:
"The new import job might have performance problems under load. Keep an eye on it."

Better finding:
"Watch 2. The import job runs one database query for each row (what the code does). A file with 50,000 rows holds a connection for minutes and starves web requests (what goes wrong). Smallest fix: batch the lookups into a single query. If skipped: web latency spikes during imports. Tripwire: the slowest 1% of web requests, shown on the existing latency dashboard; roll back if it stays above 2 seconds for 10 minutes."

What changed: the vague worry became a specific case with a fix, a signal that is visible today, and a rollback value set in advance.

## Final reply

Use short sentences and plain words, and explain each technical term the first time it appears. Reply in this order:

1. **Summary:** what the change does, in two or three sentences, plus the load you assumed.
2. **Findings:** numbered and grouped as Block, Watch and Note. Each has four parts: what the code does, what goes wrong, the smallest fix, and the cost of skipping it. Each Watch item also includes its tripwire.
3. **Rollout plan:** the stages, how long to wait at each one, and the tripwires checked at each stage.
4. **Rollback steps:** who flips what, and how long that takes.
5. **Verdict:** exactly one of "Ship directly", "Ship behind a flag", or "Fix N and M first".
6. **Closing line:** "Not checked: ..." naming anything important you could not verify, such as production load, dashboards you could not see, or untested flag states.

## Excuses to reject

| Excuse | Correct response |
|---|---|
| "The diff is small, so callers can't break." | Small changes to shared functions break the most code. Read the callers. |
| "It's probably fine at scale." | Name the load from the repo and test the finding against it. |
| "We'll pick rollback numbers if something looks off." | Then you will talk yourself out of them. Set them now. |
| "There's surely a dashboard for that." | If you cannot point to where it shows up, the signal does not exist. Block the item or add logging. |
| "It's only a Note, I'll mention it as a blocker to be safe." | Overstating findings buries the real blockers. Keep the buckets honest. |
| "I can just fix it quickly myself." | This skill produces a plan. Report the smallest fix and leave the edit to the user. |
| "Staging passed, so no flag is needed." | Staging does not carry real traffic. Watch items still need a flag. |

## When not to use

Skip this skill for general code-quality reviews or style feedback when no merge or deploy is coming up.

## Self-check

- Does every finding name a concrete input or situation that fails?
- Does every Watch item have a signal that is visible today and a trip value written before release?
- Is the rollout speed matched to how hard the change is to undo?
- Did you state the load you assumed and where that assumption came from?
- Does the reply end with a verdict and a "Not checked" line?
- Did you leave the code unedited?
