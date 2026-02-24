# The Model in Your Head

Every engineer who works on a system carries a mental model of that system. The model is not the system. It is a simplified, partially accurate representation that enables reasoning and prediction. Without it, you could not work on the system at all — you would have no basis for predicting the consequences of a change or diagnosing the cause of a failure.

The model is also always wrong in some ways, and the ways it is wrong matter enormously.

---

## How Mental Models Form

You build a mental model of a system the first time you encounter it: reading the code, watching it run, talking to people who built it. The model starts rough and becomes more detailed as you interact with the system more.

But the model is not a passive reflection of what is there. It is an active construction — shaped by what you expect to find based on prior experience, by what the documentation says (which may not match the code), by what the previous engineer told you (which reflects their model, not the system directly), and by the parts you happened to examine versus the parts you did not.

This means mental models have structure that comes from you, not from the system. The analogies you used to understand the system — "it works like a queue," "it's basically a cache," "it's similar to the auth system we had at my last job" — are scaffolding that helped you build the model. They also introduce inaccuracies wherever the system does not actually behave like the analogy.

---

## Divergence Over Time

A mental model formed at time T and a system modified after time T will diverge. The system changes; the model does not update automatically.

Some of this divergence is visible: you see the pull request, you read the change, your model updates. Some is invisible: a change was made to a part of the system you do not work on regularly, and your model never incorporated it. A behavior you assumed was true for years was actually changed eighteen months ago. The assumption is so baked into your model that you never thought to verify it.

This invisible divergence is the source of a particular class of bug: the engineer is completely confident that the code does X, because the code used to do X and they have not been told otherwise, but the code now does Y and has for over a year.

Experience is supposed to make engineers more effective, and mostly it does. But experience also creates confident wrong assumptions that are hard to dislodge precisely because they are confident. An engineer encountering a system for the first time has no model and reads carefully. An experienced engineer often reads less carefully because the model fills in what they expect to see, making discrepancies between expectation and reality less visible.

---

## The Model as a Lens and a Filter

When you look at code through a mental model, the model determines what you see.

In a codebase you know well, your eye skims over familiar patterns and focuses on anomalies. This is efficient — you are using the model to filter out noise. But it is also a source of errors. If the "familiar pattern" has been modified in a significant way, your eye may not catch it. Your model predicts what will be there, and prediction shapes perception.

This is particularly relevant in code review. Reviewing code in a system you know well, you often read the diff through the lens of what you expect the change to look like given the intent. If the change does something different from what you expected — correctly or incorrectly — the discrepancy may not register.

Reviewers who catch the most bugs in code review tend to read code as if they are encountering it for the first time, suppressing the prediction from the model and reading what is actually there. This is harder in familiar code than in unfamiliar code, because familiarity generates stronger predictions.

---

## Testing the Model

One of the more valuable habits an engineer can develop is testing their mental models explicitly rather than relying on them implicitly.

"I believe the cache has a TTL of five minutes — let me check the configuration to confirm." "I think this function always returns before calling the database — let me trace through it to verify." "My understanding is that this queue is FIFO — let me check whether there are priority levels I'm not aware of."

These are deliberate acts of verification. They are slower than acting on the model directly. They are also how you find the cases where the model has drifted from reality — and those are precisely the cases where acting on the model would produce errors.

The instinct to verify rather than assume increases with engineering experience, or it should. Early-career engineers sometimes over-verify — checking things they can reasonably trust — but more often the problem is under-verification, especially on systems one knows well.

A useful heuristic is: the more confident you are about something, the more worth checking it is. High confidence with low recent verification is exactly the profile of an assumption that has silently diverged.

---

## Shared Models and Their Failures

A team working on a system has a collection of individual mental models that overlap imperfectly. Each engineer's model is shaped by their history with the system — which parts they built, which bugs they debugged, which incidents they responded to.

Coordination problems between engineers often trace back to divergent models rather than bad intentions or poor communication. Engineer A changes the behavior of a shared service because their model says downstream consumers do not depend on the old behavior. Engineer B's service breaks because their model assumed the old behavior. Neither engineer was wrong given their model; the models were incompatible.

Design documents, architecture diagrams, and technical discussions are attempts to align these models. They create a shared reference that people can verify their individual models against. This alignment has a real effect: teams with more shared understanding of their system make fewer coordination errors.

The limitation is that shared documentation ages the same way individual models do. The architecture diagram from two years ago reflects the shared understanding from two years ago. The models that engineers actually use are built from that document plus everything that has happened since — and what has happened since may have drifted the system significantly from the diagram.

---

## The Map and the Territory

There is a traditional framing for the relationship between models and reality: the map is not the territory. A map is a useful representation of a territory. It is not the territory itself. The features that are on the map exist in the territory; the territory also contains things that are not on the map.

The mental model is your map of the system. The system is the territory. Your map was accurate enough to navigate when you made it. The territory has changed since then, in ways large and small, and your map has not kept up.

This does not make maps useless. It makes them tools that require maintenance, scrutiny, and occasional willingness to put them down and look at the territory directly.

The most dangerous moment is not when you know your map is incomplete — you are alert then, reading carefully, open to surprise. The most dangerous moment is when you do not know your map is wrong, and you navigate confidently into territory that is not where the map says it is.

---

## What This Means

The mental model is indispensable. You cannot reason about a system you have no model of. The model enables every useful thought you have about the code — how to structure a change, where a bug might be hiding, what the consequences of a modification will be.

The model is also a source of errors that are invisible precisely because they are errors in your model rather than errors in the code. The code is right in front of you. The gap between your model and the code is not.

The discipline that addresses this is not constant skepticism — you cannot function if you question every assumption always. It is targeted verification: the willingness, especially in unfamiliar territory or after long absence, to check the things you are most confident about. To read what is there rather than what you expect. To treat the system as the authority and your model as a hypothesis.

The system is always more complex than the model. That is not a failure — it is the nature of models. The goal is a model accurate enough to be useful and a habit of checking it often enough to stay approximately right.
