# The Linter's Politics

A linter presents its rules as technical requirements. Violation is flagged in the same visual language as a compiler error: red underline, warning icon, a count in the problems panel. The presentation implies objectivity — this is wrong, in the same way that a type error is wrong.

Most linter rules are not like that at all. They are conventions. They encode preferences about style, readability, and consistency that reflect choices made by some group of people at some point in time. Those choices are legitimate and often worth following. But they are not the same category of thing as a type error, and treating them as if they were obscures something important.

---

## What Linters Actually Check

Linters check two distinct categories of things, and they present both in the same way.

The first category is genuinely error-prone patterns: code that is valid but statistically likely to be wrong. An unused variable, a comparison with NaN, a condition that is always true because of a logic error, a function that has a missing return in some code path. These rules have a clear epistemic basis — engineers have repeatedly written bugs of these forms, and catching them statically is unambiguously useful.

The second category is stylistic conventions: how code is formatted, how things are named, whether you use semicolons, how long a line can be, whether you prefer `===` over `==` in JavaScript. These rules have a social basis — some team or language community decided on a convention, and the linter enforces it.

The first category is closer to a compiler check. The second category is closer to a code review comment. Both are presented identically.

---

## Conventions as Encoded Culture

When a linter rule says "function names must be camelCase" or "maximum line length is 120 characters," it is encoding a cultural choice as a technical requirement.

This is not a neutral act. The choice was made by people with particular backgrounds, working in particular contexts, with particular tools and workflows in mind. The Python community's preference for snake_case reflects different conventions than the Java community's preference for camelCase. Neither is more correct. Both are now enforced by linters in their respective ecosystems as if they were facts about code.

The line length rule is a good example of the underlying reasoning often being lost. The common limit of 80 characters comes from the physical width of early terminals. 120 characters is a common update for wider modern displays. Neither number reflects something fundamental about code readability — they reflect hardware constraints that existed at the time the conventions were established. The convention is now enforced without the context that generated it.

This is not an argument for ignoring line length rules. Consistency has real value, and a codebase that follows a consistent style is genuinely easier to read. The argument is for knowing what the rule is — a social contract, not a truth — so you can reason about it clearly.

---

## The Cost of Enforcement

When conventions are enforced as requirements, they create friction. The friction is sometimes intentional — you want consistency enough to impose a cost on deviation. But friction has effects beyond what is intended.

Engineers who disagree with a rule spend cognitive energy fighting the linter instead of thinking about their code. They find workarounds: the `// eslint-disable` comment, the pragma comment, the carefully structured exception. These workarounds accumulate and make the codebase harder to read in different ways than the rule was trying to prevent.

More subtly, automatic enforcement tends to suppress the reasoning that should accompany rule application. When a rule is enforced by a tool, engineers stop asking whether the rule applies here — they just satisfy it. This is the price of scaling conventions: rules that were good heuristics become rules that are applied without judgment, including in cases where they do not apply well.

Good linter use requires knowing which rules are there for error prevention (follow them carefully) and which are there for consistency (follow them, but don't lose sight of the underlying goal when edge cases arise).

---

## The Neutral Position That Isn't

Some linting tools are presented as enforcing "best practices." This framing deserves scrutiny.

Best practices are practices that have worked well in some contexts. They are not universal laws. The practice of avoiding global variables is a good heuristic in most application code and a bad fit for some systems programming contexts. The practice of limiting function length is useful for complex business logic and potentially counterproductive for generated code or lookup tables. The practice of preferring composition over inheritance is sound advice in many OO designs and not particularly relevant in functional code.

Linters that enforce "best practices" are enforcing the judgment of whoever configured them about which practices apply in which contexts. That judgment may be very good — the tool authors may have deep experience — but it is still judgment, embedded in configuration, applied automatically without knowing your specific context.

The alternative is not to abandon linters. It is to configure them deliberately: to understand each rule you enable, know what it is for, and be willing to disable rules that do not fit your context. The worst linter configuration is the one applied from defaults without review, because it embeds someone else's context silently into your workflow.

---

## Consistency Has Genuine Value

It would be easy to read this chapter as an argument against linters. It is not.

Consistency in a codebase has real, measurable benefits. Code review is easier when reviewers do not need to negotiate style in every PR. Onboarding is easier when there is one way to do common things. Searching for patterns is easier when patterns are uniform. The cognitive load of moving around a large codebase is lower when the stylistic surface is predictable.

Linters are an efficient way to achieve consistency. The alternative — hoping that style conventions are applied through shared culture alone — does not scale beyond small teams.

The point is that the benefits are social, not technical. Consistency matters because of what it does for the people working in the codebase, not because the consistent style is objectively superior. Understanding this changes how you think about which battles to fight. Pushing back hard on a linter rule because you prefer a different style is probably not worth it — the consistency benefit outweighs your preference. Pushing back because a rule produces genuinely worse code in your context is a different argument, and worth making.

---

## What This Means

Linters mix two distinct things: error detection and convention enforcement. The former is technical; the latter is social. Treating them the same is a category error that tends to produce uncritical rule-following and accumulated exceptions where exceptions do not help.

The useful practice is to know which of your linter rules are which, configure rules deliberately, and apply them with the judgment they deserve. A linter is a tool for encoding the team's collective preferences efficiently. Those preferences should be visible and considered, not hidden in configuration and treated as unquestionable facts about code.
