# Documentation Decays

Documentation is a record of understanding at a point in time. The moment it is written, it begins to diverge from the system it describes. Code changes. Requirements change. The people who knew the original intent leave. The documentation does not automatically update.

This is not a problem with insufficient discipline. Teams with strong documentation cultures still produce documentation that decays. The decay is structural: code and documentation are two representations of a system, updated by different processes, with no mechanism that keeps them synchronized.

---

## The Two Things Documentation Is

Documentation serves two distinct purposes that are often conflated.

The first is orientation: helping someone understand a system they are unfamiliar with. This is the README, the architecture overview, the "how does this work?" document. Its goal is to build a sufficient mental model fast enough to be useful. For this purpose, approximate accuracy is often acceptable — you do not need a complete picture, you need enough to start.

The second is specification: an authoritative description of how something works that can be relied on for implementation or integration. The API reference that tells you what a function returns, what exceptions it throws, what guarantees it provides. For this purpose, approximate accuracy is not acceptable. Inaccurate specifications cause bugs in the things built against them.

The decay problem is different for each type. Orientation documentation that is six months out of date may still be mostly useful — the architecture is probably similar, the concepts are still there, the stale parts may be identifiable. Specification documentation that is six months out of date can be worse than no documentation, because it is relied on and wrong.

---

## Why Documentation Lags

The fundamental issue is that documentation and code have different update incentives.

Code is updated when it does not work. Bugs fail visibly. Tests fail. Users complain. The feedback loop is tight and the motivation is clear.

Documentation is updated when someone notices it is wrong. There is no automated system that detects when documentation has become inconsistent with code. A comment describing what a function does will remain there, unchanged, after the function's behavior has been modified — unless the engineer who modified the function thought to update it. Thinking to update it requires holding two things in mind simultaneously: the implementation change and its description. One is the task; the other is overhead.

This is the root cause, and no amount of process changes it completely. Humans reliably prioritize tasks with visible feedback loops over tasks with invisible feedback loops. Documentation's feedback loop is invisible — no one knows it is wrong until they rely on it and find out.

---

## Code as Ground Truth

One partial solution to documentation decay is to make the code itself as self-explanatory as possible. Clear names, small functions, explicit types, logical structure — these reduce the need for external explanation and ensure that the authoritative record (the code) is as accessible as possible.

This helps, but it has limits. Code can explain what it does. It cannot explain why it was designed a particular way, what alternatives were considered and rejected, what invariants must hold, or what the downstream consequences of changes are. These things require prose.

There is also a version of "self-documenting code" that is a rationalization for the absence of documentation. Code that is perfectly readable in isolation may be incomprehensible in context — if you do not know what problem it is solving, or what constraints it is operating under, or how it fits into the broader system. The code is the mechanism. The documentation is the context.

---

## The Documentation That Survives

Some kinds of documentation age better than others, and understanding the difference is useful.

Documentation that explains *why* a decision was made ages well. The reasons behind an architectural choice — the constraints that existed at the time, the alternatives that were rejected, the tradeoffs that were accepted — do not become false when the implementation changes. Even if the implementation has since been updated, understanding the original reasoning is often useful for understanding the current state.

Documentation that describes *what* the system does ages poorly. Behavioral descriptions tied to specific implementations become inaccurate as the implementation changes. The closer a document is to a literal description of the code, the faster it decays, because the code itself is the most accurate version of that description.

This is also why API reference documentation generated from code — docstrings, type annotations, inline comments — tends to stay more accurate than externally maintained documentation. The documentation is co-located with the thing it describes. Updating the code and updating the documentation become the same operation.

---

## The Cost of Stale Documentation

Stale documentation has two kinds of cost that are easy to underestimate.

The first is the cost to the reader who finds it. They spend time reading something that is not true. Worse, they may act on it — implement against a stale specification, make a decision based on an outdated architecture description, waste a day debugging something that the documentation says should work. The time lost is often invisible because the reader does not know the documentation is stale; they assume they are misunderstanding something and keep reading.

The second is the cost to the codebase's reputation for documentation. Once an engineer has been burned by stale documentation a few times, they learn to distrust documentation generally. They stop reading it before diving into the code. The documentation that is accurate becomes useless because nobody reads it. Stale documentation does not just fail to help; it degrades the value of all documentation by association.

---

## What This Means

Documentation is not a solved problem. It decays, and the decay is structural.

The practical response is to choose what to document strategically rather than comprehensively. Document the things that are hardest to infer from the code: the reasoning behind decisions, the invariants that are not enforced mechanically, the integration points where multiple systems meet. Document for the reader who is lost rather than the reader who is merely reading.

Keep documentation as close to the code as possible. Prefer generated reference documentation over manually maintained descriptions of behavior. Delete documentation that is known to be stale; wrong information is worse than missing information.

And hold documentation with appropriate skepticism — including documentation you wrote yourself. The gap between what code does and what we believe it does is often larger than we expect. Documentation records the belief. The code is the authority.
