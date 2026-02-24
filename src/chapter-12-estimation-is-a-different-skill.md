# Estimation Is a Different Skill

Engineering estimation is consistently wrong in systematic, predictable ways. Projects take longer than estimated. Features are more complex than expected. Bugs surface that were not anticipated. This is so common and so consistent that there are named phenomena for it: Hofstadter's Law, the planning fallacy, the ninety-ninety rule.

The interesting question is not why estimates fail — there are good accounts of that — but what estimation actually is and what would constitute getting better at it.

---

## What an Estimate Is Not

An estimate is not a prediction. A prediction is a statement about what will happen. An estimate is a probabilistic range around a central expectation, given current understanding, subject to revision as understanding changes.

These are treated as the same thing in most engineering contexts, which produces predictable dysfunction. When an estimate is treated as a commitment, it puts pressure on the estimator to compress uncertainty. Uncertainty feels like weakness in a context where a number is expected. The result is a point estimate with implicit false precision — "two weeks" rather than "between one and four weeks, with two being the median under current assumptions."

The compressed estimate then becomes a commitment that the project is held to. When reality produces a distribution rather than a point, the project is "late." The estimate was wrong, but it was wrong in the same direction it is always wrong: reality contains variance that point estimates suppress.

---

## The Systematic Bias Toward Underestimation

Underestimation is not random error. It is systematic, which means it has systematic causes.

One cause is the planning fallacy: people estimate based on the best-case scenario rather than the realistic distribution of outcomes. When you estimate a task, you imagine executing it correctly, without interruptions, without discovering unexpected complexity. This imagined scenario is possible. It is not the median case.

Another cause is reference class neglect: ignoring the history of how similar projects went in favor of the specifics of this project. "This project is different" is often true in the details and almost never true in the structure. Similar projects took longer than estimated. This project will probably also take longer than estimated.

A third cause is the unknown unknowns: the things you do not know you do not know. Every non-trivial engineering project contains surprises. A bug in a third-party library. An undocumented interaction between systems. A requirement that was not clearly stated until it became a blocker. These surprises are not individually predictable, but their existence is predictable. Every project has them. They are not in most estimates.

---

## The Reference Class as Calibration Tool

One approach to improving estimates is to explicitly use reference classes: "how long have similar tasks taken in the past?"

This requires having tracked how long similar tasks took. Most teams do not do this systematically. The data that would most improve future estimates — the actual duration of past work, compared to estimates — is rarely collected and analyzed.

When teams do collect it, they often find that their estimates are consistently off in the same direction by a consistent factor. A team that estimates two weeks for features that take four weeks has a systematic 2x underestimation bias. This bias can be corrected by multiplying estimates by the historical factor. This sounds too simple to work. It often works.

The more important use of reference classes is to resist the natural tendency to treat each project as unique. "This project is different" is almost never different in the ways that matter for estimation. The sources of variance — integration complexity, unclear requirements, unexpected bugs, competing priorities — are largely the same across projects. Historical data captures the variance class even when it does not capture the specifics.

---

## The Tasks Not in the Estimate

Estimates typically cover the direct work: writing the code, writing tests, doing code review. They typically do not cover the surrounding work.

Every feature involves time spent understanding the existing codebase. Time spent in meetings discussing the feature. Time spent on interruptions — questions from colleagues, other bugs that need to be handled, incidents. Time spent integrating with dependencies that behave unexpectedly. Time spent revising requirements that were unclear at the start.

None of this is deadweight. It is the actual cost of building software in a real organization. But it is often not in the estimate, so it appears as overrun when it materializes.

A more accurate estimate would include a realistic accounting of overhead. Most engineers know from experience that they do not spend 100% of their time on the task they are nominally working on. The overhead is real and consistent. Estimates that treat an eight-hour day as eight hours of productive task work are systematically off from the start.

---

## When Estimates Cannot Be Given

There are tasks for which no meaningful estimate can be given at the time estimation is requested.

A task that requires first understanding an unfamiliar system cannot be estimated until the system has been understood. A bug whose cause has not been identified cannot be estimated until the cause is known. A feature with unclear requirements cannot be estimated until the requirements are clarified.

In these cases, the appropriate response is not to provide a number but to name the prerequisite: "I need to spend a day reading the codebase before I can estimate this" or "I need to understand what 'flexible' means in this requirement before I can say how long it will take."

This is often received badly. The request was for an estimate, and the response was a condition. But providing a number when the preconditions for estimation are not met is not honest estimation — it is guessing with the social framing of estimation. The number produced in those circumstances is not an estimate; it is a placeholder.

The organizations that handle this well distinguish between estimates given with adequate information and commitments made under uncertainty. They treat the first as the basis for planning and the second as a risk to be managed, not a failure to be penalized.

---

## What This Means

Estimation is a skill, and like all skills, it can be developed. The development does not come primarily from trying harder to estimate accurately. It comes from tracking actuals against estimates, understanding the systematic biases in your own estimates, using reference classes, and building the organizational culture that allows uncertainty to be expressed honestly.

The estimate is not a contract. It is a best current answer to the question "how long, given what we know now?" As what you know changes, the estimate should change. An estimate that does not change as understanding changes is not an estimate; it is a deadline that was labeled as an estimate.

Software projects take the time they take. The goal of estimation is to know as early as possible what that time is likely to be — not to commit to a number that then determines how long the project is allowed to take.
