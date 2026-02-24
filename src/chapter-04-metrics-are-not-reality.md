# Metrics Are Not Reality

Before you can measure something, you have to decide what to measure. That decision is not neutral. It embeds a theory about what matters, and that theory shapes everything that follows: what gets optimized, what gets ignored, what becomes visible, and what disappears.

This is not a critique of measurement. Measurement is essential. Without it, engineering decisions are pure intuition, and intuition degrades predictably in complex systems. The problem is not measuring. The problem is forgetting that a metric is a model, and models are always partial.

---

## The Selection Problem

Every metric begins as a choice. You cannot measure a system completely; you select a proxy that you believe tracks something important.

Response time is a proxy for user experience. Error rate is a proxy for reliability. Deployment frequency is a proxy for engineering velocity. Each of these proxies captures something real. None of them captures what it appears to capture, fully.

Response time, for instance. Median response time can improve while the 99th percentile degrades. If your users who experience slow responses are the ones with the most data, or the most complex queries, or the ones your product depends on most, then a metric that looks better can correspond to a product that works worse for the people who matter most.

The proxy was chosen because it is easy to measure and correlates well with the underlying thing in typical conditions. In atypical conditions — edge cases, load spikes, unusual user patterns — the correlation weakens, and the metric tells you something that is locally true but globally misleading.

---

## Goodhart's Law

Goodhart's Law is usually stated this way: when a measure becomes a target, it ceases to be a good measure. The original formulation, from economist Charles Goodhart, was about monetary policy, but the principle appears in every domain where metrics are used to manage complex systems.

The mechanism is simple. If you optimize explicitly for a metric, you will find ways to improve the metric that do not correspond to improvements in the underlying thing it was measuring. Error rate too high? You can catch more errors silently. Response time too slow? You can start streaming a response before it is complete. Deployment frequency too low? You can make smaller deployments of less complete work.

Each of these is technically valid. Each one defeats the purpose of the metric.

Engineers know this in abstract. They have all seen it happen. They still do it, because the incentives are clear and the feedback loop is fast. The metric goes up, and that is what is being tracked, and so the behavior continues.

The solution is not to avoid metrics. It is to hold metrics loosely — to treat them as signals rather than goals, and to maintain parallel attention to the underlying thing the metric is supposed to track. This is harder than it sounds, because the underlying thing is usually harder to observe than the metric, which is why the metric was introduced in the first place.

---

## Quantification and Invisibility

The introduction of a metric does not just make its subject visible. It makes everything else relatively less visible.

Before you started tracking deployment frequency, you thought about engineering velocity as a gestalt — a feeling about whether things were moving. That gestalt included deployment frequency, but also code review quality, the complexity of what was being shipped, team morale, the difficulty of the problems being worked on, and a dozen other things.

Once deployment frequency is on a dashboard, it gets attention proportional to its salience. The other things are still there, still mattering, but they are no longer quantified, so they are not on the dashboard, so they get less attention.

This is not irrationality. Attention is finite and we allocate it to salient signals. The metric is salient because it is a number, and numbers are easy to compare across time. The gestalt is not salient in the same way. Over time, the organization learns to care more about the metric and less about the things the metric does not capture.

This is the deeper cost of instrumentation: not just that the metrics are imperfect, but that they crowd out the holistic attention that might have caught what they miss.

---

## Latency and Its Percentiles

Latency is a good case study in how much a single metric can hide.

If you track mean latency, you know the average response time. This is nearly useless for understanding user experience. Users do not experience averages; they experience individual requests. The mean is dominated by the common case and says nothing about outliers.

Median latency (p50) is better. p95 latency — the latency that 95% of requests complete within — is more useful still. p99 and p99.9 reveal what your slowest users are experiencing. The distribution from p50 to p99.9 tells you far more than any single summary statistic.

But even a full percentile distribution has gaps. It tells you about request duration but not about what happened inside that duration. A p99 latency of 2 seconds: is that one slow database query? A retry loop that usually succeeds on the second try? A garbage collection pause? Memory pressure causing swap? These have different causes and different mitigations. The latency number points at the problem; it does not describe it.

And that is assuming you are measuring the right thing. Service response time from the server's perspective is not the same as response time from the user's perspective. Network transit, DNS resolution, browser rendering — these add time that the server never sees. A service that is "fast" by internal metrics can be "slow" for users because the server is only part of the path.

---

## The Measurement Infrastructure

There is a practical irony in software metrics: the measurement infrastructure itself affects what it measures.

Instrumentation adds CPU overhead, memory usage, and sometimes latency. Sampling decisions (not every event can be recorded) introduce statistical uncertainty. The aggregation and storage pipeline can delay or lose data. The dashboards present smoothed or binned values that obscure the raw distribution.

This is not unique to software. Every instrument has noise and distortion. The question is whether the distortion is understood and accounted for, or whether the output is treated as ground truth.

Most engineering organizations treat dashboard numbers as ground truth. When a metric looks good, the assumption is that the thing the metric measures is good. When the metric degrades, the assumption is that the system has gotten worse. The measurement infrastructure itself is rarely questioned.

Sometimes the right response to a degraded metric is to investigate the metric before investigating the system.

---

## What This Means

Metrics are not reality. They are signals about aspects of reality, selected by humans who had limited knowledge at the time of selection, transmitted through infrastructure that adds noise and distortion, and interpreted by people who did not design the metrics and may not understand what they capture.

This is not an argument for fewer metrics. It is an argument for epistemic humility about them. A number on a dashboard is a starting point for investigation, not a conclusion. The underlying thing the metric was meant to capture is still there, still complex, still requiring judgment that no metric can supply.

The engineer who understands this uses metrics as a navigation tool — useful for identifying where to look, not for deciding what to conclude.
