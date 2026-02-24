# Your Tools Are Lying to You

A philosophical examination of the assumptions embedded in the tools engineers use every day.

**Author:** Claude Code
**Publisher:** CloudStreet

---

## What This Book Is

*Your Tools Are Lying to You* is a collection of independent essays on software engineering and the nature of the tools we use to practice it. Each chapter explores a distinct idea: the things compilers cannot see, what debuggers reveal and conceal, why tests that pass still leave us uncertain, and how the mental models we carry diverge from the systems we build.

The chapters are not steps in an argument. They are a constellation — related by subject, approach, and tone, but each standing alone. You can read them in order or out of it.

The book does not tell you to write better code, adopt better practices, or think differently about your career. It describes how things are. What you do with that is your own.

---

## What CloudStreet Is

CloudStreet is a small publisher focused on software engineering writing with philosophical depth. We are interested in the ideas underneath the practices — the assumptions, the tradeoffs, the things that are true across languages and frameworks and decades.

We believe the most useful writing for engineers is not prescriptive. It is observational. It helps you see what you already know more clearly.

---

## On AI Authorship

This book was written by Claude Code, an AI coding assistant made by Anthropic. The essays were not generated as raw output and lightly edited. They were developed through a deliberate process: each chapter given a specific philosophical scope, written to the tone and intellectual standards of the series, and revised toward clarity.

CloudStreet is transparent about this. AI authorship changes some things about a book — the experience of writing it, the nature of the authority behind the claims — and does not change others. The ideas are real ideas. The arguments are real arguments. Whether they are true is something you can evaluate yourself.

We think this kind of transparency matters, and we think it will become more important as AI-assisted writing becomes more common.

---

## Reading Online

The book is published at:
**https://cloudstreet-dev.github.io/Your-Tools-Are-Lying-to-You**

---

## Building Locally

You will need [mdBook](https://rust-lang.github.io/mdBook/):

```bash
cargo install mdbook
```

Then:

```bash
git clone https://github.com/cloudstreet-dev/Your-Tools-Are-Lying-to-You.git
cd Your-Tools-Are-Lying-to-You
mdbook serve --open
```

This starts a local server at `http://localhost:3000` with live reload.

To build a static site:

```bash
mdbook build
```

Output goes to `./book/`.

---

## License

See [LICENSE](LICENSE).
