---
name: no-slop-grenade
description: Distill a session's findings into one sentence a human can act on — "I observe X, based on Y it can be Z." — sized to the audience, instead of forwarding a wall of AI-generated text (a "slop grenade"). Use whenever the user is about to share, send, forward, report, hand off or summarize findings, results, an investigation, a debugging session or analysis for a colleague, teammate, manager, stakeholder or client — e.g. "how do I tell the team", "write this up for the client", "summarize for my manager", "what should I send", "TL;DR for Slack", "draft a message about this".
---

# No Slop Grenade

A **slop grenade** is a long, unedited AI output dropped on someone else. It
looks like effort, but it makes the reader do the work: they have to read it,
find the point, check it, and work out what to do. This skill turns a session's
findings into one sentence the sender can stand behind.

## The format

> **I observe X, based on Y it can be Z.**

- **X: observation.** What was actually seen. Concrete, checkable, without
  interpretation. ("p95 latency on /checkout went from 300 ms to 2.1 s after
  Tuesday's deploy", not "performance issues".)
- **Y: evidence.** What the conclusion rests on: the data, test, log,
  document or comparison. Name the source in a way the reader can check.
- **Z: inference.** What it probably means, or what it implies for the reader.
  Keep the uncertainty honest: "it can be", "likely", "rules out". Never present
  a guess as fact.

One sentence. If you need a second one, use it only for the **ask or next step**
("Can you approve the rollback?"). Nothing else.

## Procedure

1. **Collect the findings.** Look back over the session. List what was
   *verified* separately from what was *assumed*. Leave out dead ends, process
   narration ("first I checked…") and anything the reader can't act on.
2. **Pick the one finding that matters most to this reader.** If there are
   several unrelated ones, say so and offer one sentence for each (at most 3),
   ranked by importance. More than 3 means the work isn't finished; tell the user.
3. **Identify the audience.** If the user hasn't said who it's for, ask once:
   *"Who is this for: a technical colleague, a non-technical colleague/manager,
   or a client?"* Then adjust the detail using the table below.
4. **Write the sentence.** Fill X, Y and Z. Read it back: could the reader repeat
   it to someone else without the session? Could they check Y?
5. **Run the anti-slop checks** (below). Rewrite until it passes.
6. **Hand it over.** Give the sentence (plus the optional ask) as plain text,
   ready to paste. Offer supporting detail separately: *"Want the evidence
   bullets as a follow-up, in case they ask?"* Don't attach it by default.

## Audience calibration

The structure stays the same for every reader. Only the vocabulary and the
level of detail change.

| Audience | X (observation) | Y (evidence) | Z (inference) |
|---|---|---|---|
| **Technical colleague** | Exact metric, component, version, error string | Specific query, log line, commit, test, benchmark (link or ID) | Mechanism-level cause, with confidence |
| **Non-technical colleague / manager** | Effect on users, time or money | The kind of evidence, stated plainly ("our monitoring", "a side-by-side test") | Impact and decision needed |
| **Client** | Outcome in their terms | Verifiable source, without internal jargon or blame | Implication for them and what happens next; careful with certainty |

### Example: same finding, three audiences

- **Technical:** "I observe p95 on `/checkout` rose from 300 ms to 2.1 s after
  deploy `a1b2c3`; based on the trace samples showing 1.7 s spent in the new
  N+1 `cart_items` query, it can be the ORM change in PR #482."
- **Manager:** "I observe checkout got about 7× slower after Tuesday's
  release; based on our performance traces, it can be one code change that we
  can roll back today."
- **Client:** "We observe slower checkout times since Tuesday's update;
  based on our monitoring, it can be traced to a single change, and we're
  rolling it back today."

## Anti-slop checks

Rewrite if any of these are true:

- [ ] More than one sentence (plus an optional ask).
- [ ] X has an interpretation in it ("broken", "bad", "issues") instead of an
      observation.
- [ ] Y is missing, vague ("analysis shows", "AI suggests") or something the
      reader can't check.
- [ ] Z sounds more certain than Y supports, or hedges so much it says nothing.
- [ ] Filler: "Great question", "It's worth noting", "In summary", "delve",
      "comprehensive", "robust", lists of every possibility.
- [ ] Jargon the audience won't know, or (for technical readers) vagueness
      where an identifier exists.
- [ ] The sender couldn't defend every word if asked. If they couldn't, it isn't
      ready to send.

## What not to do

- Don't paste the session transcript, raw model output or a long report
  as the message.
- Don't pad with caveats to look thorough; give the real uncertainty in Z once.
- Don't invent evidence to fill Y. If there isn't any, say so: the honest
  sentence is "I observe X; I don't yet have evidence for why", and the next
  step is to get evidence, not to send.
