# The Honesty of Compilers

There is a kind of trust engineers extend to compilers that they rarely examine. When the build passes, something like relief settles in. When it fails, the error is treated as authoritative: the compiler has found a problem, and the problem is real.

This trust is mostly warranted. Compilers are careful instruments. They apply consistent rules to well-defined inputs, and their judgments are reproducible. A type error is a type error whether you run the compiler at midnight or noon, on your machine or a colleague's.

But the trust goes further than the instrument deserves, and understanding exactly how far is worth doing.

---

## What Compilers Actually Check

A compiler checks whether your program conforms to a specification. In a statically typed language, it checks that values flow through operations in ways the type system permits. It checks that identifiers are declared before use, that function calls provide the right number and kind of arguments, that syntax is well-formed.

These are not small things. Catching type mismatches at compile time prevents entire categories of runtime failure. The value of a compiler that can tell you, before your program runs, that you are treating an optional value as if it were definitely present — that is substantial.

But the specification the compiler checks against is not "correct behavior." It is a formal grammar and a type system, which are approximations of correct behavior — useful approximations, carefully designed ones, but approximations nonetheless.

The compiler does not know what your program is supposed to do. It cannot tell you whether your business logic is right. It cannot detect that you are sorting a list in ascending order when the caller expects descending. It cannot find the condition you forgot to check, or the edge case your algorithm handles incorrectly, or the security vulnerability introduced by a perfectly type-correct operation.

It checks what it checks, and nothing else.

---

## The Confidence Problem

The subtler issue is not what compilers miss — most engineers understand intellectually that a passing build is not a proof of correctness. The subtler issue is what a passing build does to how you feel.

When you fix the last type error and the build goes green, something shifts. The anxious scanning stops. You become less alert. The green status has done something psychological that it has not earned the right to do: it has made you feel like the risky part is over.

This is understandable. The human attention system is not well-suited to maintaining vigilance against abstract possibilities. We respond to signals. A green build is a signal, and we respond to it. The fact that the signal is narrowly defined does not prevent it from having a broad calming effect.

This matters in practice. Engineers who have just fixed a compile error are less likely to carefully read the surrounding logic. They have received confirmation that something was wrong, they have fixed it, the tool says it is fixed. The natural next step is to move on.

But compile errors and logical errors are not the same category of problem. You can have code that is entirely type-correct and entirely wrong.

---

## Type Systems as Proofs

There is a strand of programming language theory that takes the relationship between types and correctness seriously. In sufficiently expressive type systems, you can encode properties of your program that go well beyond basic type safety — invariants, preconditions, entire correctness proofs expressed as types.

Dependent types, for instance, allow you to write a type that represents "a list of exactly n elements" or "a natural number greater than zero." If you can express what your program should do in the type language, the compiler's guarantee extends that far.

This is real and interesting. But it has costs. The more you encode in types, the more complex the types become, and the harder the code is to read, write, and reason about. There is a tradeoff between what the compiler can verify and what the human programmer can understand — and the tradeoff is not free.

Most production codebases sit far from the dependent-types end of this spectrum. They use types to prevent certain categories of errors, not to prove correctness. Which means the compiler's guarantee, while real, is bounded.

---

## The Useful Lie

There is something to be said for the confidence a green build produces, even when that confidence is not fully warranted.

Programming is a cognitively demanding activity. If every passing build were treated with the full uncertainty it deserves — "this might be correct, or it might be wrong in ways I cannot immediately see" — the anxiety would be paralyzing. We need to be able to close things down, declare partial victories, move forward.

The compiler saying "this is fine" is useful even if "this is fine" means something more limited than we feel it means. It partitions the work. It lets you stop holding certain things in mind.

The problem is not the confidence itself. The problem is when the confidence is not calibrated — when "the compiler accepted it" bleeds into "I have verified it" without that transition being examined.

The engineer who understands the compiler's limits can take the green build at full value for what it actually provides, and no more. They can stop worrying about type errors without stopping to think about correctness.

---

## A Note on Type Inference

Type inference adds another dimension to this. In languages with strong inference — Haskell, Rust, recent versions of TypeScript in strict mode — the compiler is doing significant reasoning on your behalf. You do not write every type annotation; the compiler infers what the types must be.

This is mostly a good thing. It reduces ceremony and catches errors you would not have thought to annotate against.

But it introduces a gap between what you think the types are and what the compiler has inferred. Usually these are the same. When they diverge, the error messages can be disorienting — the compiler is arguing about a type you never named.

The inference is a form of interpretation. The compiler is reading your code and deciding what you meant. When it decides correctly, the experience is seamless. When it decides incorrectly, the error appears to be about something other than what you thought you were doing.

This is not a reason to avoid inference. It is a reason to understand that the compiler is interpreting, not merely executing your instructions.

---

## What This Means

None of this is an argument against compilers. Compilers are among the most valuable tools in the engineer's repertoire, precisely because their guarantees are real and their feedback is fast.

The point is narrower: the guarantee is specific, and the trust we extend should match the guarantee.

A passing build tells you that your program is well-formed with respect to a formal system. That is worth something. It is not worth everything. The things it does not tell you are still there, still requiring your attention.

The engineer who knows this is in a better position than the one who does not. Not because they worry more, but because they worry about the right things.
