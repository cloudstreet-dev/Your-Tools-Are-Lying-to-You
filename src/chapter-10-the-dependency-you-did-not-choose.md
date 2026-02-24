# The Dependency You Didn't Choose

When you add a library to your project, you make a choice. You evaluate the library, decide it fits your needs, and add it. The choice is yours.

What you do not choose is everything the library depends on, and everything those dependencies depend on. The transitive closure of your dependency graph is decided by authors you have never heard of, for reasons you were not part of, in response to requirements that have nothing to do with yours.

This is not an exotic edge case. It is the normal state of software development. A JavaScript project with a handful of direct dependencies can have hundreds of transitive ones. A Python project using popular scientific computing libraries pulls in a deep tree that touches C extensions, Fortran code, and platform-specific binaries. The code you review and reason about is a small fraction of the code that runs when your software runs.

---

## The Transitive Trust Problem

When you add a dependency, you extend trust. You are saying: I believe this library does what it claims, is maintained responsibly, and will not harm my system or my users.

When that library adds its own dependencies, your trust extends further, whether you intended it to or not. The authors of your library made their own trust judgments, about libraries you have not evaluated, for needs that may not match yours.

This creates a trust chain that is very long and largely invisible. You can inspect your direct dependencies. Inspecting the transitive graph is theoretically possible and practically infeasible — the graph is too large, the code too voluminous, and most of it is not in your domain of expertise.

The limits of this trust became widely understood after a small number of high-profile supply chain attacks. The events that attracted the most attention — a malicious actor publishing a package with a similar name to a popular one, a maintainer's account being compromised, a dependency being deliberately backdoored — demonstrated something that had always been structurally true: accepting code from the internet at install time is an act of trust, and trust can be exploited.

---

## Versioning and the Illusion of Stability

Semantic versioning promises a clear signal: a major version change means breaking changes, a minor version means new features, a patch means bug fixes. This is a convention that many ecosystems follow.

The convention is not mechanically enforced. It depends on authors correctly categorizing their changes. And even correct categorization does not mean that a patch release is safe to apply blindly. A bug fix for the library author can be a behavior change that breaks your code, if your code depended on the bug.

Lock files address part of this. By recording exact versions, a lock file ensures that what runs in production is what was tested in development. This is genuinely valuable and worth doing consistently.

But lock files fix versions at a moment in time. They do not fix the risk profile: a package that was safe when you locked it may have had a vulnerability discovered since. Lock files trade the risk of unexpected changes for the risk of known-but-not-updated vulnerabilities. Neither is obviously better; they are different risks that require different mitigation.

---

## The Maintenance Question

Software is not finished when it is released. It requires maintenance: security patches, compatibility updates for new language versions and platforms, bug fixes, adaptation to changes in the ecosystem it depends on.

When you take on a dependency, you are implicitly depending on someone else to maintain it. That someone else may be a large organization with dedicated engineers, a small team doing it in their spare time, a single maintainer who has moved on, or a project that has been abandoned.

The maintenance status of your dependencies is usually not visible from the code. A library may be well-maintained and simply stable — no recent commits does not necessarily mean abandoned. Or it may be genuinely abandoned, leaving any future security issues unaddressed. Or the maintainer is present but overwhelmed by issues and has not had time to review pull requests for the past year.

This information exists but requires active investigation. The dependency management tool tells you the version. The maintenance health is in the issue tracker, the commit history, the response rate to pull requests, the maintainer's public statements about the project's future.

Most teams do not systematically review this. They add dependencies when needed, use them until there is a reason to stop, and discover maintenance problems when problems surface.

---

## Dependency as Architecture

How much of your system behavior lives in code you wrote versus code you imported is an architectural question with long-term implications.

A codebase with shallow dependencies — using libraries for well-defined purposes with stable APIs — is easier to reason about, easier to audit, and easier to update when circumstances require it. A codebase where core functionality is delegated to frameworks that dictate structure and behavior is faster to build but harder to disentangle.

Neither is wrong in all cases. The tradeoff is real. Using a battle-tested HTTP client library is almost always better than writing your own. Using a full-stack framework that generates your database schema, your API layer, and your frontend rendering pipeline means accepting that framework's model of how software should be structured. The efficiency gain is real; the architectural lock-in is also real.

The point is that dependency choices are architectural choices. They constrain future options, import behavior you did not design, and create obligations that extend over time. Treating them as purely a question of "does this library solve my immediate problem" misses their structural character.

---

## What This Means

The dependency graph you run is not the same as the dependency graph you chose. The former is the transitive closure of everything your direct dependencies require; the latter is the small set you evaluated directly.

This gap is not something you can eliminate. Modern software development at any scale depends on reuse. The alternative — implementing everything you need from scratch — is far worse on virtually every dimension.

The useful orientation is informed acceptance: know that your transitive dependencies exist and are significant, have a lightweight process for reviewing new direct dependencies (who maintains this? how many transitive dependencies does it bring in? what is its security track record?), keep your lock files current, and treat major dependency upgrades as engineering work rather than routine maintenance.

The code running in your production environment is mostly code other people wrote. That is a feature and a risk simultaneously. Understanding both sides of it is part of understanding what your system is.
