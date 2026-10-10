---
layout: default
title: Twenty tabs, one sentence
date: 2026-10-11
description: Every cloud browser agent starts at a sign-in wall, which is why they ask for your passwords. Brotto runs in the tab you are already signed into, so there is nothing to hand over — here is one real task, start to finish.
---

There is a particular kind of afternoon. You have twenty tabs open and a thing
you need done: find the invoice from March, check whether the refund landed,
pull the number you were emailed about last week, cancel the subscription you
forgot about. None of it is hard. All of it is *yours* — your accounts, your
sessions, your passwords — and you are doing it by hand, one tab at a time,
because that is the only way to reach the inside of a site you are signed in to.

Brotto exists because that afternoon is a sentence.

> *Find my last three unread emails from Priya and summarise them.*

## Why the obvious alternative asks for your password

The obvious way to build this is a browser in a data centre. You give it a URL
and it opens the page. And then it hits the wall: a cloud browser has no cookie
jar, so every site starts at the sign-in screen, and a site that has never seen
this machine has no reputation and serves a bot challenge. Both problems have
the same fix in the industry, and the fix is to ask you for your credentials and
store them.

I think that is the wrong shape, and not only because handing a third party
your Google password is a bad idea in the way that handing a stranger your house
keys is a bad idea. It is bad because the thing you wanted — *reach the inside
of a site you are signed in to* — is something you already had. The session was
sitting in your browser the entire time. The credential vault exists to work
around a limitation of where the browser runs, and then it gets sold as a
feature.

So Brotto runs somewhere else: **in the tab you are already signed in to.** A
Chrome extension, driving the browser you already have open, against the
accounts you already have. Your cookies, your MFA, your SSO are simply there —
there is nothing to sign in to, and nothing to hand over.

That is the whole design decision, and most of what follows from it is a
consequence rather than a feature.

## It reads the page, but not by looking at it

One more thing decides what this can and cannot do, and it is worth knowing
because it is visible in every run below.

Brotto does not take screenshots and ask a vision model to read them. It reads
the **accessibility tree** — the roles, labels, values and references that a
screen reader already navigates by. A button is a button because the page says
it is one, not because something guessed that a rectangle is probably a button.

No vision model, no image tokens, no cost that scales with the size of the
window. And a specific failure mode disappears rather than being reduced: it is
much harder for a page to *look* like something it is not when what gets read
is the structure the page publishes rather than the picture it paints.

## One run, start to finish

This is a real task, not a demo. Brotto adding a branch protection ruleset to
its own public repository, recorded end to end. Nothing below is staged or
cropped; [the screens page](/screens) has all seven panels.

<div class="moment">
  <div class="n label">01</div>
  <div>
    <h3>You ask for it in a sentence</h3>
    <p>
      There is no form and no workflow to learn. The panel is a chat box, and
      whatever you can describe is the whole interface. This is the whole
      product's front door: there is nothing else to set up.
    </p>
  </div>
</div>

<figure class="wide">
  <img src="/assets/img/run-1-the-prompt.webp" alt="Brotto's side panel with the task typed out: go to GitHub, find the Brotto repository, add a branch protection ruleset to main, and open a pull request for it" loading="lazy">
</figure>

<div class="moment">
  <div class="n label">02</div>
  <div>
    <h3>It asks before it leaves</h3>
    <p>
      GitHub is the first domain this run touches, so it stops and waits. The
      reason to gate the <em>domain</em> and not the action is worth a
      sentence: a malicious instruction does not arrive from a search engine,
      it arrives from a page the agent was sent to. If it cannot reach an
      unfamiliar domain without asking you, that whole class of problem shrinks
      considerably.
    </p>
  </div>
</div>

<figure class="wide">
  <img src="/assets/img/run-2-before-it-navigates.webp" alt="Brotto's side panel showing a first-navigation approval card for github.com, with Allow and Deny buttons" loading="lazy">
</figure>

<div class="moment">
  <div class="n label">03</div>
  <div>
    <h3>It stops again when the page offers a choice</h3>
    <p>
      GitHub has two ways to add branch protection, and guessing wrong means
      clicking back through settings. Rather than pick one silently, it hands
      you the question. This is the same card you would get for a sign-in it
      cannot pass — the panel is a conversation, not a log.
    </p>
  </div>
</div>

<figure class="wide">
  <img src="/assets/img/run-3-it-asks-when-unsure.webp" alt="Brotto's side panel stopping to clarify that the repository has two ways to add branch protection, with Skip and Say options" loading="lazy">
</figure>

<div class="moment">
  <div class="n label">04</div>
  <div>
    <h3>It finishes, and the whole thing is on your disk</h3>
    <p>
      Note where the ruleset was written: on github.com, by your own session,
      with your own permissions. Nothing was sent to us. The transcript lands
      in <code>logs/sessions/</code> beside the rest of your files, which is
      what lets you read a run back, resume one that was interrupted, or delete
      it outright.
    </p>
  </div>
</div>

<figure class="wide">
  <img src="/assets/img/run-4-the-ruleset-it-wrote.webp" alt="Brotto reporting DONE: it created a classic branch protection ruleset on the main branch of the Brotto repository, with targets, enforcement status, required checks and force-push settings" loading="lazy">
</figure>

Two stops in a fourteen-step run, both on decisions only you could make. That
is the shape I want by default: the agent is willing, and it is not the one
holding the authority when it matters.

## What it asks about

Once a task is in flight there are three cards, and they resolve in place so
the run reads as a conversation:

<div class="shots">
  <figure>
    <img src="/assets/gifs/approval.gif" alt="Brotto's panel stopping on an approval card for a domain it has not visited in this task, with Deny and Approve buttons" loading="lazy" width="400" height="760">
    <figcaption><b>Approve.</b> A domain it has not visited stops the run until you say yes or no.</figcaption>
  </figure>
  <figure>
    <img src="/assets/gifs/clarify.gif" alt="Brotto's panel asking which time the launch announcement should go out on Tuesday, with a Skip button" loading="lazy" width="400" height="760">
    <figcaption><b>Ask.</b> When the page has two equally good answers, it puts the question to you.</figcaption>
  </figure>
  <figure>
    <img src="/assets/gifs/login.gif" alt="Brotto's panel stopped on a Google sign-in page, waiting for you to sign in before it continues" loading="lazy" width="400" height="760">
    <figcaption><b>Sign in.</b> Your cookies stay yours. Brotto hands the wall back to you and picks up after.</figcaption>
  </figure>
</div>

The third one is the loop closing. When Brotto hits a wall that needs your
credentials, it stops and asks — which is exactly the moment the credential
vault products exist to automate away.

## The part you should read before installing anything

An agent running in your signed-in session is not a sandbox. It acts with the
authority you have, and if it is wrong, it is wrong *as you*. An email it
sends is not flagged as suspicious, because it genuinely came from you.

I think that deserves more than a reassurance, so I wrote down what actually
stops it, what does not, and the fact that every guard in the path is ultimately
a string test — including the ones I am proudest of.

**[An agent holding your cookies](/blog/2026-10-09-what-an-agent-holding-your-cookies-can-do.html)** —
the next post, and the one to read first if that is your question.

## What it is not yet

I would rather these were here than discovered.

- **Installing it is six steps**, not one. A container, an extension, and a
  few settings. [The install](/#try) is written out; a one-command installer is
  next.
- **There is no reliability number, and I am not going to invent one.** Until
  the harness scores real runs against a real model, any percentage in this
  space — mine included — is a guess. What the run above shows is a *shape*,
  not a rate.
- **Google Sheets is genuinely blind.** It draws to a canvas, so there is no
  structure to read. Docs may be fine, because it renders a real DOM, but I
  have not verified it and will not claim it before I have.
- **It needs a model key.** Brotto does not sell tokens or mark them up; it
  supports eight providers, or any OpenAI-compatible endpoint you run yourself.
- **Chrome only.** `chrome.debugger` has no Firefox equivalent.

---

Brotto is [Apache 2.0](https://github.com/suryanshgupta9933/Brotto) and stays
that way. It is written out properly in the
[privacy policy](/privacy) and the [security policy](/security) — including
what it does not protect you from, which is the more useful half.