---
layout: default
title: Brotto
description: A browser agent that works in the Chrome tab you are already signed in to. Self-hosted, bring your own key, free and open source under Apache 2.0.
---

<div class="hero">
  <img class="hero-mark" src="/assets/logo.svg" alt="">
  <h1 class="hero-title">Brotto</h1>
  <p class="hero-line">
    An agent that works in the browser tab you are already signed in to.
    Self-hosted, bring your own key, and it stops and asks before anything
    irreversible.
  </p>
  <div class="actions">
    <a class="btn" href="https://github.com/suryanshgupta9933/Brotto">Get Brotto</a>
    <!-- Chrome Web Store link goes here once the listing is published and has
         an item id. A link to a search page is worse than no link. -->
    <a class="btn btn--ghost" href="#writing">Writing</a>
  </div>
</div>

## What it does

You tell it a task in plain English and it carries that out in a tab you
select. Attach to your own browser, start a run, close the panel.

- **Reads the accessibility tree, not screenshots.** Roles, labels, values and
  stable backend node ids — no vision model, no image tokens.
- **Asks before anything irreversible**, with no setting to turn that off.
- **Asks before it visits a domain for the first time.** That is where indirect
  prompt injection has to come through.
- **Writes an audit document per run** to disk, on your own disk.

## Try it

Chrome only. The extension is the client; the agent loop runs on a container
on your own machine.

```bash
export AGENT_SECRET="$(python3 -c 'import secrets;print(secrets.token_urlsafe(32))')"
docker compose up -d
```

Apache 2.0. The image is about 510 MB and contains no browser.

## Writing {#writing}

- [**An agent holding your cookies**](blog/2026-10-09-what-an-agent-holding-your-cookies-can-do.html)
  — 2026-10-09. What an agent with your sessions can do as *you*, the three
  gates that stop it, and the fact that all of them are made of strings.
- [**The browser is not a picture**](blog/2026-10-08-the-browser-is-not-a-picture.html)
  — 2026-10-08. On accessibility trees versus screenshots, and on the gap
  between a reference that resolves and a reference that can be clicked.
{: .post-list}