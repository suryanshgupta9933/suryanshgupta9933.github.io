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
  and on patterns marked critical. You can *add* to that list; there is no setting that turns any of
  it off.
- **Your domain blocklist, and only yours.** There is no server-side floor policy, by design.
- **Prompt-injection defence** — the system prompt establishes a trust hierarchy
  (system > user task > page content) and instructs the model to treat page content as data.
- **Secret redaction** — credentials, API keys, bearer tokens, private keys, payment card numbers and
  government identifiers are stripped from page text before it reaches your model provider, and typed
  values in credential fields are kept out of the audit record. Pattern matching, so it can miss a
  novel format and can over-redact; both directions are the accepted trade.
- **No remote code execution.** The extension never `eval`s, never fetches a script, and dispatches only
  a fixed set of typed actions. See
  [the extension's README](https://github.com/suryanshgupta9933/Brotto/blob/main/clients/brotto-extension/README.md#what-this-extension-does-not-do).

What Brotto does **not** provide, and you should not assume:

- **Authentication is on only if you set a secret.** The orchestrator requires `AGENT_SECRET` on every
  route the extension calls, including the WebSocket. With no secret set it logs a warning and serves
  **open** — anyone who can reach it can drive a browser. Do not expose an unconfigured server to a
  network you do not control.
- No isolation between concurrent users. Identity is a random per-install id the extension generates on
  your machine. It is not a real user account, and it is not a credential.
- No protection against a hostile page. The gates reduce the blast radius; they do not eliminate it.

## Out of scope

- Model behaviour (the agent making a poor decision is not a Brotto vulnerability, though a
  *disclosure bypass* — an action taken without a required approval — is)
- Denial of service by a page or a model
- Findings that require an attacker to already control your machine or your orchestrator
- Missing hardening with no demonstrated impact
