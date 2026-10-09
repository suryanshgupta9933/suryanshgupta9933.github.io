# An agent holding your cookies

**2026-10-09 · Suryansh Gupta**

The previous post was about perception — why Brotto reads the accessibility tree
instead of screenshots, and why a reference that resolves is not a reference that
can be clicked. That argument is about capability. This one is about the part
that should worry you: **an agent that runs inside your signed-in browser is
holding your sessions, and what happens when it is wrong.**

I want to be specific rather than reassuring, because the reassuring version of
this post is what every agent product writes, and it is the reason people hand
their Gmail to things that shouldn't have it.

## The blast radius is not "it can send an email"

The scariest property of an in-session agent is not that it *can* do things. It
is that **it does them as you.**

An email it sends carries your name, your address, your sending domain, your
prior relationship with the recipient, and a TLS certificate from a domain your
bank and your mail provider recognise. It does not look like an attack. It looks
exactly like you, on a day you were busy, which is the reason phishing defence is
built to trust it.

A payment it makes has your full session — the bank has already done MFA, the
second factor is satisfied, the device fingerprint is your laptop. There is no
second check standing between the agent and the money, because from the bank's
point of view there is nobody else there.

That is not an argument against in-session agents. It is the argument for
treating the moment of first contact with a new domain as a security boundary,
which is what Brotto does and what most of them don't.

## What actually stops it

Three mechanisms, none of them a setting you can turn off.

**It stops and asks before anything irreversible.** Not "before anything it
classifies as risky" — before it sends, pays, deletes, publishes, approves,
transfers, or changes a password.

**It stops and asks before it visits a domain for the first time.** This is the
one that matters more than it looks. A malicious instruction does not arrive from
a search engine; it arrives from a page the agent was sent to. If it cannot
reach an unfamiliar domain without asking, the whole indirect-injection surface
gets much smaller.

**Your blocklist is the only blocklist.** No server-side floor, no operator
override, nothing merged in behind your back. A blocked domain is a hard stop
with no override path — the task ends.

And then the one that is easy to skip and that I would not skip: **every run
writes an audit document to your disk.** Not a chat transcript. Tasks, turns,
each observation, each prompt, each action, each approval, each timing, on a
filesystem you control, greppable and deletable as a unit. When something goes
wrong, the difference between "I think it clicked the wrong thing" and a
grep for `off-screen` across `logs/sessions/` is the difference between a fear
and an incident report.

## Where my own guardrails are made of strings

Here is the part I would want to read in someone else's post about their own
tool, so I am going to write it about mine.

The irreversible-action gate is **a regex over the action's own description.**
Ten patterns:

```python
CRITICAL_PATTERNS = [
    r"delete", r"submit.*form", r"send.*email", r"create.*ticket",
    r"approve", r"reject", r"payment", r"transfer",
    r"publish", r"deploy", r"confirm",
]
```

matched against `f"{action} {action_args}"`. Nothing clever is happening. The
action name the model wrote, concatenated with its arguments, run past those ten
patterns.

**Which means the label is the security boundary.** A destructive control
labelled `Purge`, `Empty`, `Remove`, `Wipe`, `Archive`, `Trash`, or `Cancel
subscription` does not match any of them. `Clear inbox` does not match. `Delete`
is in the list and `Purge` is not, and there is no principled difference between
those two buttons — only a linguistic one.

The same shape appears one layer up. A domain grant is keyed on the **eTLD+1**,
deliberately: approving `example.com` approves every subdomain and every future
verb on it, for good, because keying it finer made one run ask the same question
once per action type on the same page. That is the right default and it is also
exactly the shape of a confused-deputy bug.

And the most important limitation of all, stated plainly: **page content reaches
the model.** A hostile page can put text in front of the model the same way a
hostile email can. The approval gate is a list of ten strings; the domain gate is
a list you wrote. An attacker who can get the agent to take an action whose
description is innocuous has walked around all of it, because every guard in the
path is a string test and the attacker controls the string.

None of this is a reason to throw the design away. It is a reason to know
exactly which parts are load-bearing and which are a speed bump, and I would
rather you hear it from me than find it.

## The one narrowing that doesn't ride a grant

There is a single exception to "approving a site approves the site," and it is
there for a specific reason.

Most actions are gated on the domain, and a domain grant is permanent. But
`aria-hidden` elements — the content a page marks as assistive-technology-only —
**never ride a grant**. The check is membership *after* the key: the element has
to be hidden *and* the domain has to be unvisited this session. A page injecting
a hidden "Delete account" button cannot get through on a site you approved last
week.

That is a very narrow control against a very specific attack, and I include it
because it shows the shape of thinking I think the rest of this needs: the grant
is broad, so find the one thing it must not cover, and cover that separately.

## What I am not claiming

- **This is not prompt-injection defence.** It is a set of gates that make the
  *common* case safe and make the *indirect* case much harder. A determined
  attacker with page control has real leverage, and I have described exactly
  where.
- **Redaction is not a boundary.** Credentials, API keys, bearer tokens, card
  numbers and government identifiers are stripped from page text before it
  reaches the provider — in code, on every task, no setting. But that is a filter
  on the way out, not a guarantee about what is in the page. Redaction catches
  things that *look* like secrets.
- **Bring your own key is about the key, not the pages.** The agent loop runs on
  a server you run, so page observations transit it — that is inherent, not a
  leak. What you choose is that there is no operator between the agent and your
  documents, because there is no operator.
- **The blocklist being yours is a liability as much as a feature.** I have no
  floor. You run this, you are the entire trust model.

## What I want to be argued with

- **Is a description-matched gate the right shape at all?** The obvious
  alternative is asking the model to classify the action as irreversible in a
  separate cheap call. That moves the boundary from a word list to a model I
  cannot audit. I do not obviously think that is better, and I would like to be
  argued out of my own position.
- **Should a domain grant expire?** A grant that is scoped to one run is safer
  and much more annoying. I chose permanent, because a prompt every five minutes
  is a prompt people click through without reading, which is the failure mode
  that makes approval cards worthless.
- **Is the audit document a real control or just comfort?** If nobody ever reads
  it, it is a log file and the trust argument is thinner than I am making it.

---

Brotto is [Apache 2.0](https://github.com/suryanshgupta9933/Brotto). The
previous post, on perception, is
[here](https://suryanshgupta9933.github.io/blog/2026-10-08-the-browser-is-not-a-picture.html).