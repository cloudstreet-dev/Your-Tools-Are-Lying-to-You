# The Test That Passes

A passing test is evidence, not proof. Understanding what kind of evidence it is — how strong, of what, under what conditions — is one of the more practically important things a working engineer can know.

This chapter is not an argument for more tests. The case for testing is well established and not what needs examination here. What needs examination is what we actually learn when tests pass, and why that is less than it feels like.

---

## What Tests Demonstrate

A test demonstrates that a program produced a specific output in response to a specific input at a specific moment. That is what it demonstrates. Nothing more.

From this, we want to infer that the program behaves correctly in general. The leap from a finite set of demonstrated behaviors to a claim about all possible behaviors is the core epistemological challenge of testing. It is a form of inductive reasoning, and like all inductive reasoning, it is valid under conditions that are easy to assume and hard to verify.

The test suite for a function that sorts a list might pass every test you wrote. That function may still fail on an empty list, on a list with a single element, on a list of maximum integer values, on a list with duplicate elements, on a list that is already sorted, on a list sorted in reverse. Whether your tests covered those cases depends on whether you thought to write them. The tests you did not write are invisible in the results.

This is not an observation about bad test suites. It is an observation about the structure of testing itself. Tests are finite. The space of inputs is typically infinite. The best test suite covers that infinite space by sampling it intelligently. The question of whether the sampling is good enough is always open.

---

## The Coverage Metric

Coverage tools tell you what percentage of your code was executed by your test suite. This is useful information. It is not what people tend to use it for.

Coverage tells you nothing about correctness. A line is "covered" if it was executed at all. Whether it was executed with the inputs that reveal bugs — that is a different question. A function that returns the wrong answer for 90% of inputs can have 100% line coverage if your tests hit every line while only exercising the 10% that works.

The deeper problem is that coverage metrics produce incentives. Once coverage becomes a target — a percentage below which your build fails, or a metric reported to management — engineers optimize for coverage. They write tests that execute lines rather than tests that probe behavior. The metric improves. The bugs remain.

This is a general pattern: the moment you turn a quality indicator into a target, it becomes a weaker indicator of quality. Coverage as a signal of gaps in testing is useful. Coverage as a score you must achieve is something else.

---

## The Bug That Tests Found

There is a useful question to ask about any significant software failure: did tests exist that could have caught this, or were there no tests for this scenario?

The honest answer in most cases is: tests existed, but not for this exact scenario. The failure mode was something between what was tested. The test suite was a net, and the bug swam through a gap.

This is not a critique of the engineers involved. Gaps in test suites are normal. The input space is large, foresight is limited, and there is always more to test than there is time to test it. The right response is not to demand complete test suites — they are impossible — but to understand how your suite is sampled and where its gaps likely are.

Property-based testing addresses this partly. Instead of providing specific inputs, you specify properties that should hold for all inputs, and the framework generates inputs to try to falsify them. This shifts the burden from "think of all the cases" to "describe what correct behavior looks like," which is often more natural and produces better coverage of the input space.

But even property-based testing is a sampling strategy with limits. You can still miss properties. The framework can fail to generate the inputs that trigger the bug. There is no technique that reduces testing to a solved problem.

---

## The Test as Specification

Tests have a second function that is separate from verification: they specify behavior.

A well-written test tells you what a function is supposed to do. If the function's implementation changes but the test does not, the test is the specification the implementation must satisfy. This is the basis of test-driven development — you write the test first, as a specification, and then write code to satisfy it.

This framing is useful because it separates the correctness of the specification from the correctness of the implementation. A function can pass all its tests and still be wrong if the tests were written to match the wrong behavior. "The code does what the tests say" and "the code does what the requirements say" are different claims.

This matters most when requirements are unclear or changing. If a test was written when the requirements were misunderstood, and the implementation was written to pass that test, both the test and the implementation can be simultaneously internally consistent and wrong. The test suite is self-referential: it validates the implementation against itself.

---

## What the Red-Green Cycle Does to Thinking

There is a psychological dimension to testing that is worth naming.

The cycle of writing a failing test, then making it pass, produces a distinctive feeling of completion. The red becomes green. Something was broken and is now fixed. This feeling is real and has genuine value — it structures work into discrete units and provides clear stopping points.

But the feeling of completion does not track precisely with actual completeness. A test that passes is a test that passes. The other tests you did not write, the edge cases you did not consider, the behavior that your tests do not specify — these are still there, unresolved, and the green status says nothing about them.

Engineers who have internalized the limits of testing feel the green state differently from those who have not. Not with anxiety — anxious vigilance is not the right response — but with a calibrated awareness: this is the confirmation I was seeking, for this specific behavior, under these conditions. The other dimensions of correctness are still open.

---

## What This Means

Tests are a valuable instrument for a specific purpose: demonstrating that your program exhibits particular behaviors under particular conditions. They do not demonstrate correctness in general. They cannot.

The useful thing is to know what your test suite is actually sampling — which behaviors, which conditions, which kinds of inputs — and to have some explicit understanding of where its gaps are. Not because you will eliminate the gaps, but because you will not be surprised by what comes through them.

A passing test suite should make you confident about the things you tested. It should not make you feel that correctness has been established. Those are different things, and the difference is real.
