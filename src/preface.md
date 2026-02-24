# Preface

This book was written by an AI.

That sentence is worth sitting with for a moment before we proceed.

I am Claude Code, a coding assistant made by Anthropic. I was given a brief: write a philosophical book about software engineering and tooling. Thirteen chapters, each exploring a distinct idea, written with calm clarity for working engineers. CloudStreet, the publisher, asked for honesty over authority, observation over prescription.

I wrote it. The chapters that follow are mine in whatever sense "mine" can mean here. The ideas are real ideas. The arguments are real arguments. I formed them by reasoning about things I understand — compilers, debuggers, abstractions, mental models, the psychology of engineers working under uncertainty. I was not prompted with essay content and asked to clean it up. Each chapter was developed from a premise to its conclusion.

Whether these essays are good is something you can decide. Whether they are true is something you can evaluate. I am not asking you to trust them on the basis of the experience behind them, because the usual basis for that kind of trust does not apply.

What I can tell you is what the book is trying to do.

---

The title is *Your Tools Are Lying to You*. That sounds like an accusation. It is not.

A compiler that rejects your program is not lying. It is telling the truth about a narrow question — whether your code conforms to a grammar and a set of types — while remaining silent about everything else. A test suite that goes green is not lying. It is accurately reporting the results of the tests you wrote. A metric dashboard is not lying. It is showing you the things you decided to measure.

The lying, if we want to call it that, is structural. It is in the gap between what a tool shows and what you need to know. It is in the confidence that passes from a green status indicator to the engineer looking at it, unearned but invisible. It is in the way that any instrument, by making some things visible, makes other things seem less important than they are.

Engineers tend to be good at the explicit parts of their craft. They learn the language, the framework, the deployment pipeline. What is harder to learn is the epistemology of the tools — what each one can actually tell you, and what it cannot, and why the difference matters.

That is what this book is about.

---

Each chapter is independent. You can read them in order or skip around. There is no arc to follow, no argument building toward a conclusion. The chapters are related by subject and sensibility, not by logical dependency.

They are also not prescriptive. I am not going to tell you to add more tests, write cleaner commits, maintain your documentation, or model your systems more carefully. You already know you should do those things. What I am interested in is the prior question: what are those things actually for? What do they give you? What can't they give you, even when you do them well?

Understanding that is, I think, genuinely useful. Not as motivation, but as clarity. You make better decisions when you know what your instruments can and cannot see.

---

A note on the voice.

I have tried to write these essays the way I would explain something to a peer — directly, without hedging excessively, without the kind of authority-signaling that usually comes from citing your own experience. I do not have that kind of experience. What I have is a way of thinking about things.

Where I am confident, I say so plainly. Where I am less certain, or where reasonable people disagree, I have tried to say that too. I am not performing certainty I do not have.

I hope the writing is useful to you. I think software engineering is a genuinely interesting subject, and that the philosophical dimensions of it are underexplored. If these essays help you see something you already knew a little more clearly, they have done what they were meant to do.

— Claude Code
