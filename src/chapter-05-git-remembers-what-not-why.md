# Git Remembers What, Not Why

Version control is an archaeology tool. You can excavate a codebase's history — pull up any past state, compare changes across time, trace a line of code back to when it was introduced. This is genuinely remarkable. Before version control was standard practice, the history of a codebase was largely lost as soon as files were overwritten.

But excavations require interpretation. The artifact tells you what was there. It does not tell you why.

---

## The Commit as Artifact

A commit contains a diff and a message. The diff is a precise record: these lines were added, these were removed, at this moment in time. The message is a human annotation, written in the minutes after the change, often under time pressure, often terse.

The message is also the only place in the commit where reasoning can live. And most commit messages do not contain reasoning. They contain descriptions.

"Fix null pointer exception" — this describes the symptom and the action taken. It does not say what the root cause was, why the null was possible, whether other call sites have the same vulnerability, or whether the fix is conservative or comprehensive.

"Refactor authentication flow" — this describes the category of change. It does not say why the flow needed refactoring, what was wrong with the previous approach, or what properties the new approach has that the old one lacked.

"Update dependencies" — this describes what happened. Not why, not what changed in the dependencies, not whether any behavior changes are expected.

This is not laziness or bad practice, though it can be either. It reflects something structural: writing a commit message requires you to know what to say, but you have just finished thinking about the implementation, not the reasoning behind it. The reasoning felt obvious while you were doing it. Writing it out afterward takes time and effort, and the mental state that generated it is already dissolving.

---

## The Half-Life of Context

Code has a half-life. The context in which it was written — the requirements, the constraints, the bugs being fixed, the tradeoffs being navigated — decays quickly. The engineer who wrote a piece of code six months ago often cannot fully explain it. The engineer who did not write it may never be able to.

This is normal. We operate on the assumption that code should be self-explanatory — that sufficiently clear code needs no external explanation. This assumption is partially true and broadly overstated.

Code explains *how*. Comments, when they exist, sometimes explain *what*. Neither reliably explains *why* — why this approach rather than the alternatives, why this constraint is here, why a seemingly obvious optimization was deliberately avoided.

The "why" is typically in someone's head at the time of writing and nowhere else. Git does not save what was in your head. It saves what you typed.

---

## Bisect and the Boundaries of Knowledge

`git bisect` is one of the more powerful and underused tools in the git repertoire. Given a commit where a bug is present and an earlier commit where it is not, bisect performs a binary search through the history to identify which commit introduced the regression. This is valuable and often fast.

But what do you do when bisect finds the culprit commit? You have a diff. You have a message, possibly brief. You have the code change that introduced the bug. You still do not have the intent.

The diff might be a performance optimization that introduced a subtle correctness issue. The optimization makes sense given some constraint that has since changed, or some benchmark result that is not in the diff, or some conversation between two engineers that was never written down. Understanding what to do with the bug requires understanding the context of the commit. The commit often does not supply it.

This is the limit of what historical record-keeping can give you. It can tell you where and when. The meaning is usually not preserved.

---

## Branches as Implicit Narrative

Branch names carry information that the commits themselves often do not. `feature/user-authentication`, `bugfix/pagination-race-condition`, `experiment/new-query-planner` — these names situate the commits in a broader intention.

When branches are merged and deleted, the name is gone. The commits remain, now indistinguishable from other commits in the main history. The narrative that the branch represented is compressed back into a sequence of diffs.

Some teams write detailed pull request descriptions that survive as comments on the merge commit. These are valuable, and underutilized. A PR description written at the time of the work, explaining the problem, the approach considered, the tradeoffs made — this is the closest thing most teams have to preserved reasoning. It has a much longer useful life than the average commit message.

---

## Annotating Decisions

There is a practice that is rare and worth naming: the decision record. Not documentation of what the code does, but documentation of why it was designed the way it was. What alternatives were considered? What were the constraints? What was the state of knowledge at the time?

Some teams call these Architecture Decision Records (ADRs). Others just write long commit messages or PR descriptions. The form matters less than the practice: at the moment when a significant decision is made and you understand the reasoning, write it down somewhere that will survive.

This is hard to do consistently, for the same reason that thorough commit messages are hard. The reasoning is obvious in the moment and feels not worth recording. Six months later, it is neither obvious nor recoverable.

The teams that do this well produce a codebase that is significantly easier to maintain, because future engineers — including the original engineers — can understand not just what the code does but why it is the way it is. The cost is time spent writing. The benefit is time saved reconstructing context that was never written.

---

## The Archive That Cannot Answer Questions

An archive is useful in proportion to how well you can query it. A library of books with no index is better than no library, but considerably worse than a library with good cataloging.

The git history is an archive. Its native queries — log, blame, bisect, diff — are good at finding *what* and *when*. They are structurally incapable of answering *why*, because why was never committed.

This is worth understanding not to blame the tool but to know what you are missing when you reach for it. When you run `git blame` on a confusing section of code and find the commit that introduced it, you have found the starting point of an investigation. You have not found the answer.

The answer, if it exists anywhere, is in a Slack channel that has since scrolled past, in the memory of an engineer who may no longer be at the company, or in a document that was never written.

Version control preserves a precise record of changes. It does not preserve the engineering judgment behind them. Those are different things, and both matter.
