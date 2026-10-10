---
layout: default
title: Security
description: How to report a vulnerability, what Brotto's threat model is, and what it explicitly does not protect you from.
---

# Security Policy

Brotto runs an agent against your own logged-in browser, so the interesting part
of its threat model is *you*, and the whole design is the set of gates standing
between an agent holding your sessions and your documents. What Brotto does not
protect you from is written down here as well, because a policy that only lists
strengths is not a threat model.

## Reporting a vulnerability

Email the maintainer, or open a **private** security advisory on the repository
("Security" → "Report a vulnerability"). Please do not open a public issue for an unfixed vulnerability.

Include: what you did, what you expected, what happened, the affected version, and your Chrome version
if the issue involves the extension. A proof of concept helps a great deal.

You can expect an acknowledgement within 72 hours and a substantive reply within seven days. If a fix
is warranted we will agree a disclosure date with you, and credit you in the release notes unless you
would rather we did not.

## Threat model

Brotto is unusual in a way that changes what "safe" means, so it is worth being explicit.

**Brotto is not a sandbox.** The agent operates with the full authority of the session you run it in.
A malicious page, a prompt injection in page content, or a bug in Brotto can all cause actions to be
taken as you. Treat a Brotto run the way you would treat handing your logged-in browser to a contractor.

What Brotto does provide:

- **Gates that always ask.** An approval card before a sensitive action (send email, payment, delete,
  publish, change password, revoke access, and similar), before the first action on a given domain,
  and on patterns marked critical. Two lists, not one: the sensitive-action list is yours to extend
  in the panel's settings, and the pattern list is fixed in code. Neither can be turned off, and
  nothing can be installed that approves on your behalf.
- **Your domain blocklist, and only yours.** There is no server-side floor policy, by design.
- **Prompt-injection *resistance*, not defence.** The system prompt establishes a trust hierarchy
  (system > user task > page content) and instructs the model to treat page content as data. That is
  an instruction to a model, not an enforced boundary — it changes behaviour on most runs and does not
  stop a determined attacker. The gates below are the load-bearing control, and they are string tests.
- **Secret redaction** — credentials, API keys, bearer tokens, private keys, payment card numbers and
  government identifiers are stripped from page text before it reaches your model provider, and typed
  values in credential fields are kept out of the audit record. Pattern matching, so it can miss a
  novel format and can over-redact; both directions are the accepted trade. **This runs on the
  page-text channel only — the accessibility tree is not redacted**, and that is the channel the model
  mostly reads.
- **No remote code execution.** The extension never `eval`s, never fetches a script, and dispatches only
  a fixed set of typed actions. See
  [the extension's README](https://github.com/suryanshgupta9933/Brotto/blob/main/clients/brotto-extension/README.md#what-this-extension-does-not-do).

What Brotto does **not** provide, and you should not assume:

- **Authentication is on only if you set a secret.** The orchestrator requires `AGENT_SECRET` on every
  route the extension calls, including the WebSocket. With no secret set it logs a warning and serves
  **open** — anyone who can reach it can drive a browser. Do not expose an unconfigured server to a
  network you do not control. (The hosted beta at `agent.brotto.dev` has it set; if you are running
  your own, this is the line to check.)
- No isolation between concurrent users. Identity is a random per-install id the extension generates on
  your machine. It is not a real user account, and it is not a credential.
- No protection against a hostile page. The gates reduce the blast radius; they do not eliminate it.
  We say this plainly because every guard in the action path is a string test, and the model chooses
  the string. [A post on exactly this](/blog/2026-10-09-what-an-agent-holding-your-cookies-can-do.html)
  names the eleven patterns and where each one fails.

## Out of scope

- Model behaviour (the agent making a poor decision is not a Brotto vulnerability, though a
  *disclosure bypass* — an action taken without a required approval — is)
- Denial of service by a page or a model
- Findings that require an attacker to already control your machine or your orchestrator
- Missing hardening with no demonstrated impact
