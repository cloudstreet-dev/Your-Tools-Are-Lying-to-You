# The IDE Is Guessing

When your IDE underlines a symbol in red, or suggests a completion, or infers the type of an expression, it is not merely executing instructions you wrote. It is building a model of your code and drawing inferences from that model. The inferences are usually correct. Understanding that they are inferences, not facts, is the difference between using the IDE as a tool and being used by it.

---

## What an IDE Actually Does

An IDE continuously parses your source code and constructs an in-memory representation of it — an AST, a symbol table, a type graph. From this representation, it answers questions: What are the members of this type? What does this function return? Is this identifier in scope?

For simple cases in well-typed code, these answers are reliable. The representation is accurate, the queries are well-defined, and the IDE gives correct information.

The representation degrades at the edges. Dynamically typed code is harder to model; the IDE can infer some types but not others, and the inferences have error bars it does not display. Generated code — ORMs, macros, reflection-based frameworks — may not be in the symbol table at all, or may be present in a form that the IDE's model does not fully capture. Cross-language boundaries, where TypeScript calls into WebAssembly or Python calls into C extensions, are often opaque.

At these edges, the IDE's answers become approximations. It is still answering questions, still displaying results, still appearing to know. The visual presentation is the same whether the answer is definitive or guessed.

---

## Autocomplete as Probability

Modern autocomplete is largely a probabilistic system. In language servers backed by static analysis, completions are drawn from the type-inferred symbol table — still a model, but a relatively grounded one. In AI-assisted completion systems, the suggestions come from a learned distribution over code patterns, shaped by training data.

Both produce the same visual output: a ranked list of completions, presented as if they are equally grounded in fact. The first item in the list looks authoritative. The experience of selecting it feels like confirmation rather than choice.

This matters when the completion is wrong, because wrong completions fail silently. The code compiles. The types check out. The logic is broken. The IDE suggested a function name that looked right but does something subtly different, or a parameter order that is plausible but incorrect, or an API that has been deprecated and still exists in the symbol table.

The IDE does not know whether the completion was what you intended. It knows what is syntactically valid and what appears to fit the context. Validity and correctness are different things.

---

## Error Highlighting and False Negatives

IDE error highlighting is probably the feature most engineers trust most completely. A red underline means something is wrong. No red underline means nothing (visible) is wrong.

The second half of that statement is the dangerous one.

IDEs report errors they can detect within their model of your code. Errors that exist outside their model — runtime behavior, logic errors, integration failures — produce no highlighting. The clean editor is not a certificate of correctness. It is a report that the IDE found nothing within its field of view.

There is also the case of false negatives within the IDE's supposed domain of competence. In dynamically typed languages, an IDE may fail to highlight a type error that will crash at runtime because it could not infer the type. In template-heavy code — C++ templates, Rust generics in complex configurations — the IDE's type checker may give up partway through an inference chain and display nothing rather than an error. In code that uses eval, monkey patching, or other runtime metaprogramming, the IDE's model may be structurally incapable of detecting errors.

A clean editor is not clean code.

---

## The Refactoring That Wasn't

IDE-assisted refactoring — rename, extract method, move class — operates on the IDE's symbolic model of the code. When the model is accurate, automated refactoring is a remarkable productivity tool. You rename a symbol and the IDE updates every reference, correctly and immediately.

When the model is inaccurate, the refactoring propagates the IDE's incorrect understanding of the code's structure. Dynamic references, string-based lookups, reflection, configuration files that refer to class names by string — none of these are in the symbolic model. The IDE renames what it knows about. Everything else remains unchanged, and the program breaks.

This failure mode is insidious because the IDE appears to have succeeded. The rename completed without error. The visible references are all updated. The broken references are in places the IDE cannot see, which means they are also places where the IDE's visual feedback provides no warning.

---

## Navigation as Interpretation

"Go to definition" is one of the more heavily used IDE features. You click on a symbol and jump to where it is defined. This seems straightforward.

In dynamically typed code, "go to definition" is an educated guess. The IDE infers what a symbol might refer to based on type inference or usage patterns. It shows you a definition. That definition may be the right one, or it may be one possibility among several, or it may be a supertype whose subtype is what actually runs.

In code that uses interfaces extensively, go to definition takes you to the interface declaration, not the implementation that executes at runtime. Understanding which implementation you care about requires knowing the runtime context — which the IDE does not have without additional runtime information.

This is not a flaw to be fixed. Dynamic dispatch and interfaces are features, not bugs, and any tool that models them statically will necessarily be approximate. The point is to know what "go to definition" actually gives you: the statically knowable answer, which may or may not be the dynamically relevant one.

---

## Trusting the Tool Selectively

The useful stance toward IDE features is calibrated trust: confident for what the tool is reliable at, skeptical where the model degrades.

In statically typed, well-structured code, the IDE's model is usually accurate. Completions are trustworthy. Error highlighting is meaningful. Refactoring is safe. The tool earns its trust here.

In dynamic, generated, or cross-language code, the model is approximate. Completions are suggestions, not facts. Clean error highlighting is weak evidence. Automated refactoring requires manual verification. The tool is still useful — it is the best static view available — but the outputs require interpretation.

The engineers who use IDEs most effectively are the ones who know which category they are in. They do not apply the same trust uniformly across all contexts. They read the tool's outputs as the results of a model, not as ground truth, and they know when to check.
