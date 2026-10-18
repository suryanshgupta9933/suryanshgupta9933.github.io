---
layout: default
title: Privacy
description: What Brotto stores, what transits the server, what reaches disk, and what an idle-page suggestion reads — on self-host and on the hosted relay.
---

# Brotto Privacy Policy

**Effective date:** 2026-10-11

Brotto has a single purpose:

> **Let you ask an AI to perform tasks in your own logged-in browser.**

Everything below describes what that purpose requires and nothing more.

This policy explains what Brotto does with data.

Brotto has two deployments.

On a self-hosted install **you run the orchestrator.** It is open-source software you install on your
own machine or your own server, and the extension talks to whatever address you type into its settings.
There is no Brotto-operated service there, we run no servers on your behalf, and "the server" below
means the machine you chose to run it on.

There is also a capped, invite-only hosted relay at `agent.brotto.dev`, operated by Brotto on Heroku.
If you point the extension at it, page observations transit a server we run and a run's record is
written to a disk we operate. Nothing there expires on a timer: the record stays until you delete it,
so the task is there when you come back to it — see [Retention and deletion](#retention-and-deletion).

That is worth being precise about: whoever operates the machine the orchestrator runs on can read the
pages the agent reads. On a self-hosted install there is no operator between the agent and your
documents, because there is no operator at all. It is a property of the deployment, not a promise
from us. On the relay that operator is us, which is the reason the relay is capped, invite-only, and
not the recommended install.

If you would rather not trust anyone with that — including yourself in six months — do not have an
agent work on pages you would not paste into a chat window, and self-host rather than use the relay.

## Summary

Brotto is built so that we collect as little as possible. We take product analytics — counts of
whether people can run a task, not what the task was — and nothing else. There is no advertising, no
tracking across sites, and we do not sell or share data with anyone for marketing. Two things are
kept on the hosted relay and are described in full under [What the relay keeps](#what-the-relay-keeps):
a failure log (a machine-readable reason code and your account id, when a run breaks), and one
record per sign-in (your account id, the network you came from, and the browser — enough to tell a
new laptop from somebody else holding the account). Neither holds page content, prompts, task text
or URLs. On
a self-hosted install we do not operate the server, so we do not receive your data. On the hosted
relay at `agent.brotto.dev` we do operate it, and choosing that relay means your page observations
reach us for as long as the task runs; the rest of this policy applies to it unchanged. The data that
moves during a task is the data the task inherently requires: what the page looks like to a computer,
and the model provider you chose.

**The extension makes no outbound requests of its own.** Its interface fonts are bundled with it, so
opening the side panel contacts nothing. The only network traffic the extension starts is to the server
address you configured, and from there to the model provider you configured.

**Your model API key is never written to disk by Brotto.** It is held in memory and used to call your
model provider.

## What the extension stores on your device

| Data | Where | Lifetime |
|---|---|---|
| Model configuration (provider, model name, context window) | `chrome.storage.local` | Until you clear it |
| **Your model API key** | `chrome.storage.session` | **Memory only.** Cleared when the browser closes. Never written to disk by the extension. |
| **Your server secret** (`AGENT_SECRET`)**, or, if you signed in to Brotto Cloud, your cloud access token** | `chrome.storage.local` | Until you clear it. On a self-hosted server it authorizes reading every transcript on that server, so treat it like a password. On the relay it is an account token and carries no server-wide access. |
| An install id — a random identifier generated once, with no relationship to you, your machine, or your network | `chrome.storage.local` | Until you clear it |
| Your policy (blocked domains, sensitive-action list) | `chrome.storage.local` | Until you clear it |
| Session ID for the conversation | `chrome.storage.session` | Until the browser closes |
| The address of the server you are connected to | `chrome.storage.local` | Kept until you change it |
| The last page URL the agent saw | `chrome.storage.session` | Cleared when the browser closes |
| A running transcript of the current task — your messages, the cards Brotto is showing you | `chrome.storage.session` | Cleared when the browser closes |
| **A mirror of your finished runs** — page URLs and titles, what you typed, the agent's replies, kept so history works offline | **IndexedDB** | **Until you delete the session.** This is a copy on your own disk, and it is the broadest one we keep. |

Because the key lives in `chrome.storage.session`, it is not written to disk by Chrome and is gone when
the browser exits. You will be asked for it again next session.

The server address and the last page URL are the two rows worth a second look: both name a page you
were on, and the server address names the machine that ran your agent.

## What leaves your device during a task

When you start a task, the extension sends to the orchestrator:

1. **Your model API key and model configuration.** The orchestrator needs the key to call your model
   provider. It holds it in memory for the duration of the task.
2. **The page you are looking at**, as the machine sees it: the page URL, the page title, the
   accessibility tree of interactive elements (role, accessible name, value, and a stable reference for
   each), visible page text when the task calls for it, and — only if the server has screenshot capture
   enabled — a JPEG of the visible viewport, for pages where nothing the browser can read is about
   the task you gave.

**Page text is redacted before it is sent.** Before page text reaches the model, the orchestrator
removes credentials, API keys, bearer tokens and payment card numbers, replacing
each with `[redacted]`. This happens in code, on your machine, on every task, with no setting to turn it
off — and on the suggestions path too, which reads a page with no task running and is the easiest place
for this to be forgotten. It is pattern matching, not a guarantee: it will miss an unfamiliar identifier format, and it will
occasionally redact an innocuous number that happens to pass a checksum. The agent is told the redaction
already happened and is instructed not to try to reconstruct a redacted value.

**One limit worth stating plainly.** This is a best-effort pattern match over a fixed list, so an
unfamiliar identifier format will pass through, and an innocuous number that happens to look like a
card may be redacted when it is not. It runs on every path by which page text reaches the model,
including the agent's own page-reading tool on a later step — but treat it as a guard against
accidents, not as a boundary you can rely on.

**The accessibility tree is not redacted, and this paragraph does not cover it.**
The list above runs on the page-text channel only. The tree — the roles, labels, values and references
listed in the previous section, and the channel the model mostly reads — is passed through as it is. A
token that appears in a field's label or value rather than in body text will reach your provider
unredacted.

**A screenshot is not redacted at all.** There is a third channel, and it is the one with no coverage
whatsoever. When nothing the browser can read is about the task you gave — a chart, a drawing canvas,
Google Docs, Figma, a spreadsheet whose grid the browser has no way to describe and whose toolbar it
describes perfectly — the agent has nothing to work from, and if screenshot capture is enabled it asks
the extension for a JPEG of the visible viewport of the tab you attached. Note that this is broader than
an empty page: a page with a full toolbar and a couple of hundred characters of chrome around it is
photographed too, because what matters is whether what the browser could read was about your task, not
whether there was anything at all. Redaction is pattern matching over strings. A JPEG is pixels, so there
is nothing for it to match: a payment card number, a one-time code or an account balance rendered into a
canvas reaches the model provider whole, where the same characters in page text would have been replaced
with `[redacted]`. This is not partial coverage or best-effort coverage. It is no coverage, and the
honest description is that the one channel the redaction cannot touch is the one carrying whatever was
drawn on the screen.

**It also sees more of the page than the other two channels do.** The accessibility tree is narrowed to
interactive elements, and the page text is capped and redacted. A screenshot is the whole viewport,
unfiltered and unredacted. And because Brotto is bring-your-own-key, that image goes to *your* provider —
a single unredacted JPEG of a logged-in session is worth more to a provider's retention than an excerpt
of text from the same page is.

**Capture is off unless you turn it on.** It is a server setting: a self-hosted orchestrator takes a
screenshot only when `BROTTO_VISION_CAPTURE` is explicitly set to `on`, `1`, `true` or `yes`. Any
other value — including a typo, `false`, or the variable being absent — means no screenshot is ever
captured, on any step, for any page. If you never set it, nothing here describes anything your install
does. Independently of the switch, a page whose domain is on your own blocklist is never photographed:
that is the same list you already wrote, not a second one you have to maintain.

A screenshot is one image of the visible viewport of the one tab you attached, taken while a task is
running — not a recording, not a screenshot of your whole screen, not a history of what you have looked
at. Brotto does not write it to disk: not to the audit trail, not to a log, not to the side panel. What
the model then writes about what it saw appears in its summary, exactly as page-derived text already
does. On the hosted relay, whether capture is enabled is the operator's decision, not yours.

The orchestrator then sends **the page observations to the model provider you selected**. Brotto ships
with Anthropic, OpenAI, MiniMax, Gemini, OpenRouter, DeepSeek and Groq, and can be pointed at a
compatible endpoint of your own. This is the core of what a browser agent does: the model has to see the
page in order to act on it. Which provider receives it is entirely your choice, and that choice
determines which company's privacy policy governs that data. If you point Brotto at your own endpoint,
that data goes to your own machine and no model company sees it at all.

**None of this reaches us — on a self-hosted install.** The orchestrator is software on your machine,
so both the key and the page observations go from your browser to your machine and on to your model
provider, and no copy passes through Brotto. If you are using the hosted relay instead, that last
sentence is not true of us: the key and the observations cross a machine we operate on their way to
the provider, and we describe what that machine keeps below. The observations do not stop at the model
call on either deployment, though: the server saves the URL, the page title, and a short digest of
each page to a file on its own disk, and that file is still there after the task ends. The next
section says exactly what is in it.

## What the orchestrator writes to disk

| File | Contents |
|---|---|
| `logs/sessions/<session_id>.json` | The audit record of your conversation: your messages, the page URL and title at each step, the prompts, the actions taken, approvals, timing, and errors. It also holds the text you **typed** into a field, and the model's own written reasoning about what it saw. For the page itself it keeps counts and a summary of what changed — not the whole tree. |
| `logs/sessions/<session_id>.scratchpad.txt` | The agent's working memory: a short digest of each captured page and its URL. |
| `logs/user_models/<install-id>.json` | Your model configuration: provider, model name, context window, and the address of your provider's API if you set a custom one. **Not your key.** If that address is on your own network, it is written to disk in the clear. |
| `logs/user_policies/<hash>.json` | Your blocked-domains list; the sites you have approved Brotto to work on; and when you last saved it. |

**The page itself is never written to disk — but the record of it is not empty.** Each step's page is
recorded as a 200-character digest, so a run over an authenticated session leaves a record of *what* was
visited and not copies of *what was on it*. Two things about that step survive on disk in full: **the text
you typed** (only fields that look like credential fields are masked), and **the model's own prose about
the page**, which is its paraphrase rather than a copy. A run over your mail or your documents therefore
leaves readable traces of both.
A run resumed later recalls those digests rather than whole pages — that is the trade for keeping your
pages off the filesystem, and it is not configurable.

**If you used an earlier build, read this one.** Those builds kept a page-bodies sidecar beside each
session file, and it does hold whole pages — tens of kilobytes per session. Nothing writes it any more,
but the files a previous build wrote are still on your disk. Deleting a session removes one, and **Delete
all** removes every one including any left behind on their own; to clear them all, delete
`logs/sessions/*.pages.json` by hand. If you started on a recent build, you have none.

Values typed into a field the orchestrator identifies as a secret — anything with `type="password"`, or
a field whose name reads like a credential, a token, or a code — are **redacted before the record is
written**, so a password you type is not stored in the audit file.

That redaction applies to what the agent *types*, and the page text that reaches the model provider is
redacted separately. What is kept on disk is narrower than either: a 200-character digest of each page.
A page that displays a token, an account number, or an email address may still put a fragment of it in
that digest. If that matters for a site you use, the safest thing is to not have the agent work on that
site.

The files are named after the install that created them, so that separate users on one server do not
share settings. That name is the random install id the extension generated on your machine — not your
name, not your IP address, and not your network. The model-configuration file is named with the install
id in plain text; the policy file is named with a scrambled version of it. It is not used for
advertising — on a self-hosted install the machine holding them is yours, and nothing is
sent anywhere with it. On the hosted relay that machine is ours, and the records on it stay until you
delete them; the install id is a random identifier the
browser generated, so it does not name you.

**The approved-sites list is a record of where you have let Brotto work.** When you approve a site in
an approval card, its domain is added to your policy file and stays there until you clear it, so you
are not asked about that site again. That means the server holds a list of the domains you have given
an agent access to. Nothing else about those sites is kept — no URLs, no page content, no dates of
use — and the list is yours to remove: delete the policy file, or the approved list inside it, and
every site goes back to asking. Blocking a domain is separate from approving it, and blocking one
always wins.

One caveat worth knowing rather than guessing at: the server also accepts an identifier a client can
supply in place of that install id, and it will use that instead. The Brotto extension supplies its own
install id, so that is what is used. A client that sends something else — or nothing at all — falls back
to the connection's address. It is mentioned here because it is a real property of the software, not
because you should expect to meet it.

## Suggestions on an idle page (optional)

If you leave the side panel open on a page with no task running, Brotto can read that page's **visible
text**, URL, and title and send them to suggest something you might want to do. That request goes to
the orchestrator and on to your model provider, so the same page text leaves your machine here as it would
during a task. No action is taken on the page, and no file is written for it — the suggestion is
held in the panel's memory, which is discarded when the browser closes.

This reads a page you are looking at without a task in flight. **It is off unless you turn it on**, and
we are calling it out here rather than relying on you noticing a change. If you would rather it did not
exist, do not enable it.

Two things narrow what it will read. Pages whose address looks like a login, checkout, payment or account
settings screen are skipped before the read, and a page carrying a password, card or one-time-code field
is skipped even when its address looks ordinary. The panel shows a **"Reading page"** badge for exactly
as long as a read is in progress, so the read is visible while it happens.

Suggestions made from a page you read are labelled **"Read from the text of this page."** underneath, and
suggestions Brotto made from a page's address and title alone are not. The label is part of the
suggestion, so it comes back with it after you reopen the panel.

## Third parties

The only third party that receives your page data is **the model provider you selected**. Brotto does
not share data with advertising networks, data brokers, or social platforms. Product analytics stay
with us and are counts of whether people can run a task, not what the task was.

**If you use Brotto Cloud, one more third party is involved.** The relay authenticates accounts through
**Supabase**, which holds your email address and your quota row. Supabase never receives page content,
your prompts or your model key — it only answers "is this signed in, and how many tasks has this
account used this week". Everything else stays on the dyno, under our control, until you delete it.

**Asking for an invitation puts your address in two more places.** A waitlist row — the address, and
the optional name you typed beside it — is held in our
Supabase table, and the single confirmation email we send is delivered by **Resend**. Resend sees the
recipient, the subject and the body of that one email — all of which we wrote — and nothing about any
task, because no task exists yet. It never sees a page, a prompt or a model key. Each of those emails
carries a `List-Unsubscribe` header, which Gmail and Outlook render as an Unsubscribe button above the
message, and an unsubscribe link in the footer; either way the address comes off the list. We keep the
row until you leave.

The model providers we support — Anthropic, OpenAI, MiniMax, Gemini, OpenRouter, DeepSeek and Groq —
each have their own privacy policy and terms governing what they receive and how long they keep it.
Those terms are between you and them, and we do not control them. Your orchestrator is also a party to
this data, in the sense that it holds the page observations in memory while it waits for the model to
answer.

**On the hosted relay, that orchestrator is ours rather than yours**, which makes us a party to your
page data rather than only to the relay's traffic. Nothing else changes: the provider still receives
what it would have received on a self-hosted install, the only thing Brotto measures is whether people
can run a task — not what the task was — and no other company is given a copy.

## What the relay keeps

On the hosted relay at `agent.brotto.dev` only, and only for cloud accounts, we keep two records.

**A failure log.** When a run ends in an error we write one row: your account id, a machine-readable
reason code, a timestamp, and the app version that produced it. It exists so that when someone
reports "it just stopped", we can tell which of a hundred possible failures they hit instead of
guessing.

**One record per sign-in.** When you sign in we write one row: your account id, the network you came
from (a `/24` on IPv4 or a `/48` on IPv6 — a neighbourhood, not your address), and the browser and
operating system. It exists to answer one question: is this the same person on a new laptop, or
somebody else now holds the account? That is an incident question, not an analytics one, and the
table is not joined to anything else. It is the trade we made to know when a member signs in from a
device we have not seen — if you would rather we not have it, self-hosting is the version where
there is no operator on the other end at all.

What neither contains is the point. No page content, no accessibility tree, no prompt text, no task
titles, no URLs, no model responses. The failure row is built from a fixed set of fields and the code
raises rather than record if it is handed anything it does not recognise, so a new field cannot be
added to it by accident. Neither is used to measure usage, rank accounts, or decide who to invite. We
would delete the failure log the day the product stops breaking; the sign-in records go when the beta
does.

Nothing here applies to a self-hosted install. That disk is yours, and there is no failure log and no
sign-in record.

**Deleting your account does not delete your sign-in history**, on purpose: the record's whole value
is answering "was this account used by somebody else", and a cascade would let an intruder erase the
answer by deleting the account they stole. Ask us and we delete it — one statement, and it is yours
to make.

## Retention and deletion

Nothing expires on a timer unless you ask it to. **Deletion is entirely yours, and it is immediate** —
on a self-hosted install:

- **Session records** — the audit file and the scratchpad, described above — are written to disk and
  stay there until you remove them. Nothing expires on a schedule unless you ask for it: the server has
  a `BROTTO_RETENTION_DAYS` setting that will age sessions out, and it is **off by default** — on the
  hosted relay as well.
  - **In the panel:** each conversation in **Session history** has a delete button, and there is a
    **Delete all** above the list. Both ask you to confirm first — the question names the conversation
    by its own first message, or names how many are about to go. There is no undo.
  - **If a file cannot be removed** — open on another program, or on a read-only mount — **Delete all**
    says so rather than reporting a clean sweep. The message tells you how many files are still there;
    remove them by hand from `logs/sessions/`.
  - **On the server:** `curl -X DELETE -H "Authorization: Bearer $AGENT_SECRET" \
    http://localhost:8000/v1/sessions/<id>` removes one; `DELETE /v1/sessions` removes every one.
    The files live in `logs/sessions/`, so removing them by hand works exactly the same way.
- **Local extension data** is removed by clearing the extension's storage, or by uninstalling it.
- **Deleting sessions does not delete your settings.** `DELETE /v1/sessions` and the panel's **Delete
  all** cover the session records only. Your blocked-domains list and your **approved-sites list**
  (`logs/user_policies/`) and your model configuration (`logs/user_models/`) are separate files, keyed by
  your install id, and survive. If you want the approved-sites list gone — which is the one that records
  which domains you have let an agent work on — delete that file by hand, or clear the approved list
  inside the panel's policy screen.
- **Your API key** is not retained by Brotto anywhere. It is held in the orchestrator's memory for the
  duration of a task and not written to disk. On the hosted relay that memory belongs to a machine we
  operate, for the duration of the task.

**The two deployments differ in who has to be trusted, not in what is written or how long it is
kept.** On either one a session record stays until you delete it, so the task is there when you come
back to it. `BROTTO_RETENTION_DAYS` will age sessions out if you set it, on either deployment, and it
is off unless you do. The panel's **Delete** and **Delete all** are immediate and are the path you
control.

## Security

- The extension communicates with the orchestrator over WebSocket, and with your model provider over
  that provider's HTTPS API.
- The extension requests `chrome.debugger` to read the accessibility tree and dispatch input, and
  `<all_urls>` host access so it can work on the site you name. Both are exercised only during a task
  you started.
- The extension requests `notifications`, so a task that is waiting on you — an approval, a sign-in, a
  question — can say so, and so a finished or failed task can tell you when you are not looking at the
  panel. The notification is rendered by the operating system on your own machine and nothing about it
  is sent to the orchestrator or to us. Be aware that its wording is Brotto's own description of the
  event — the reason for an approval, or the run's summary on completion — and **a summary can quote
  what was on the page**, so a notification is page-derived and should be treated as one. Both kinds of
  alert are on by default and can be switched off independently in settings.
- The extension's other permissions are `storage` for the settings listed above, `sidePanel` for the
  panel you talk to it in, and `scripting`, which is used only to read the visible text of a page for
  idle suggestions, and only after you have turned that on. None of the three contacts a server.
- Brotto always asks for approval before sensitive actions (sending email, payments, deletes,
  publishing, changing passwords, and similar), and always asks before acting on a site for the first
  time. There is no setting that turns either off.
- The blocked-domains list is yours alone. There is no server-side floor, so nothing Brotto's operators
  configure can add a site you did not block yourself.

**The endpoints are authenticated, and the bind address is the other half of that.** The server requires
an `AGENT_SECRET` you set yourself, and the extension sends it as a WebSocket subprotocol rather than in
the URL — a `?token=` would write your secret in plain text into the access log of your server and of
any proxy in front of it. With the secret unset, every caller is treated as trusted and the server says
so in its startup log, so if you expose the port to a network, set the secret first. The default
`docker compose` binds to `127.0.0.1` for exactly this reason.

One endpoint is deliberately left open on a self-hosted install, and it is not a session one: `POST
/run` launches a headless browser with no authentication. Do not put it on a public interface. It is
refused outright on the hosted relay, which runs in production mode. `/health` is also
unauthenticated because the container's own healthcheck needs it; it reports that the service is up,
which model is resolved, the version, and which authentication mode is in force. It names a mode and
never a secret.

No system is perfect. A browser agent operating with your session has the same access you do, and a
compromise of the extension or the server would have the same effect. Do not use it on accounts where
that risk is unacceptable.

## Chrome Web Store Limited Use

> The use of information received from Google APIs will adhere to the Chrome Web Store User Data
> Policy, including the Limited Use requirements.

We collect user data only to perform the task you asked for — driving the tab you selected on your
behalf — and for nothing else. We do not sell it, and we do not use it for advertising. Product
analytics are counts of whether people can run a task, not what the task was.

## Children

Brotto is not directed at children under 13.

## Changes to this policy

Material changes will be noted in the repository's commit history and dated at the top of this file.

## Contact

Questions about this policy: open an issue in the repository.
