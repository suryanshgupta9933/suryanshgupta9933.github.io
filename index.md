---
layout: default
title: Brotto
wide: true
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
    <a class="btn btn--ghost" href="https://github.com/suryanshgupta9933/Brotto/discussions">Feedback</a>
    <!-- The store listing is still under review, so there is no install target
         to point at yet. When it publishes, this becomes
         chromewebstore.google.com/detail/brotto/<id> and takes the hero's
         primary slot. A search URL must not stand in for it: chromewebstore
         .google.com/search/brotto also matches extensions we do not control. -->
  </div>
</div>

<!-- The panel's own status bar, carrying a real run: 14 steps, 41.2% context
     used, outcome DONE. It is the product's interface rather than a picture
     of it, so it is worth saying in markup what a screenshot would blur. -->
<div class="statusbar">
  <div class="cell"><span class="label">Steps</span><span class="value">14</span></div>
  <div class="cell"><span class="label">Active</span><span class="value">377.3s</span></div>
  <div class="cell"><span class="label">Context</span><span class="value">41.2%</span></div>
  <div class="cell outcome" data-state="done">
    <span class="label">Outcome</span><span class="value">Done</span>
  </div>
</div>

## What it does {#what}

You tell it a task in plain English and it carries that out in a tab you
select. Attach to your own browser, start a run, close the panel — the loop
keeps going because it is not in the panel.

<div class="grid-2">
  <div>
    <h3 class="mini">Reads the accessibility tree, not screenshots</h3>
    <p>
      Roles, labels, values and stable backend node ids. No vision model, no
      image tokens, and a click lands where a sighted user would have put it
      because the target came from the same tree the browser draws from.
    </p>
  </div>
  <div>
    <h3 class="mini">Asks before anything irreversible</h3>
    <p>
      Spending money, sending a message, deleting a thing — each one stops the
      run and puts a card in front of you. There is no setting that turns this
      off, and no way for the agent to approve on your behalf.
    </p>
  </div>
  <div>
    <h3 class="mini">Asks before the first visit to a domain</h3>
    <p>
      That is where indirect prompt injection has to come through, so it is a
      gate rather than a heuristic. The grant is yours and it outlives the run
      that gave it.
    </p>
  </div>
  <div>
    <h3 class="mini">Writes an audit document per run</h3>
    <p>
      Every step, every action and its outcome, to a nested JSON file on your
      own disk. That file is the record — there is no database, and nothing is
      sent anywhere you did not start.
    </p>
  </div>
</div>

## A run, from the inside {#how}

The panel below is not an illustration. It is the actual card the extension
renders, rebuilt in markup so you can read what it says.

<div class="panel">
  <div class="panel-head">
    <img class="panel-logo" src="/assets/logo.svg" alt="">
    <span class="panel-brand">Brotto</span>
    <span class="panel-pill label">Connected</span>
  </div>
  <div class="panel-body">
    <div class="bubble bubble--user">Find me the cheapest direct flight to Lisbon in November</div>

    <div class="step">
      <span class="step-mark" aria-hidden="true"></span>
      <div class="step-body">
        <span class="step-head">Opened Google Flights and set the destination to Lisbon (LIS)</span>
        <span class="step-meta">Step 12 · 28.4s</span>
      </div>
    </div>

    <div class="card card--approval">
      <div class="card-top">
        <span class="badge label">Approval needed</span>
      </div>
      <p class="card-body">
        Booking a flight spends your money, so Brotto stops and asks. It cannot
        approve this itself, and neither can anything you install later.
      </p>
      <p class="card-url">https://kayak.com/checkout</p>
      <div class="card-actions">
        <span class="btn-sm btn-sm--danger">Deny</span>
        <span class="btn-sm btn-sm--primary">Approve</span>
      </div>
    </div>

    <div class="step">
      <span class="step-mark" aria-hidden="true"></span>
      <div class="step-body">
        <span class="step-head">Read the three cheapest direct results</span>
        <span class="step-meta">Step 13 · 26.1s</span>
      </div>
    </div>
  </div>
</div>

Three gates, all made of the same few lines of code, and none of them optional:
irreversible actions, first visits to a domain, and the sign-in wall. A run
that hits one of them waits. That is the whole security model.

## Watch a run {#demo}

<figure class="demo">
  <video controls playsinline preload="metadata" poster="/assets/poster.jpg">
    <source src="/assets/brag.mp4" type="video/mp4">
    Your browser cannot play this video.
    <a href="/assets/brag.mp4">Download it instead.</a>
  </video>
  <figcaption>
    Twenty-five seconds of a real run on a real booking site — the plan it
    wrote, the domain consent, the approval card, and the answer it came back
    with. No cuts, no staging.
  </figcaption>
</figure>

## The panel {#screens}

<p class="section-note">
  Five screens from the extension. Everything here is the shipped build.
</p>

<div class="shots">
  <figure>
    <img src="/assets/shots/01-the-ruleset-it-wrote.png" alt="Brotto showing the rules it wrote for itself before starting" loading="lazy">
    <figcaption>The ruleset it wrote</figcaption>
  </figure>
  <figure>
    <img src="/assets/shots/02-it-asks-when-it-is-unsure.png" alt="Brotto asking a clarifying question mid-run" loading="lazy">
    <figcaption>It asks when it is unsure</figcaption>
  </figure>
  <figure>
    <img src="/assets/shots/03-the-prompt-you-start-from.png" alt="Brotto panel open on an idle page with the prompt box" loading="lazy">
    <figcaption>The prompt you start from</figcaption>
  </figure>
  <figure>
    <img src="/assets/shots/04-approves-before-it-navigates.png" alt="Brotto asking to approve navigation to a domain" loading="lazy">
    <figcaption>It approves before it navigates</figcaption>
  </figure>
  <figure>
    <img src="/assets/shots/05-privacy-and-settings.png" alt="Brotto settings panel showing privacy and provider options" loading="lazy">
    <figcaption>Privacy and settings</figcaption>
  </figure>
</div>

## Try it {#try}

Chrome only. The extension is the client; the agent loop runs in a container on
your own machine.

```bash
export AGENT_SECRET="$(python3 -c 'import secrets;print(secrets.token_urlsafe(32))')"
docker compose up -d
```

<table>
  <tr><td>Licence</td><td>Apache 2.0 — read it, fork it, ship it</td></tr>
  <tr><td>Image</td><td>About 510 MB, and it contains no browser</td></tr>
  <tr><td>Keys</td><td>Yours. Eight providers, or any OpenAI-compatible one</td></tr>
  <tr><td>Your data</td><td>Audit files on your disk. The server transits page text and never stores it</td></tr>
  <tr><td>Cost</td><td>Nothing, beyond the model calls you make</td></tr>
</table>

<p class="section-note">
  Source, issues and releases are on
  <a href="https://github.com/suryanshgupta9933/Brotto">GitHub</a>. If something
  is wrong with it, the
  <a href="https://github.com/suryanshgupta9933/Brotto/discussions">discussions</a>
  tab is the fastest way to say so.
</p>

## Writing {#writing}

Two essays on the parts of this that are harder than they look.

<ul class="post-list">
  <li>
    <a href="blog/2026-10-09-what-an-agent-holding-your-cookies-can-do.html">An agent holding your cookies</a>
    <span class="post-when">2026-10-09</span>
    <span class="post-stand">What an agent with your sessions can do as <em>you</em>, the three
    gates that stop it, and the fact that all of them are made of strings.</span>
  </li>
  <li>
    <a href="blog/2026-10-08-the-browser-is-not-a-picture.html">The browser is not a picture</a>
    <span class="post-when">2026-10-08</span>
    <span class="post-stand">On accessibility trees versus screenshots, and on the gap
    between a reference that resolves and a reference that can be clicked.</span>
  </li>
</ul>