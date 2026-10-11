---
layout: default
title: Brotto Cloud
description: The hosted version of Brotto, by invitation — the same extension with someone else's server running it. Free during the beta, capped, and honest about what we see.
---

<!-- THE ONE PLACE THE ADDRESS LIVES.
     `waitlist_email` below is the single source for the form action, the
     visible fallback address and the mailto link. Change it here and all three
     move together. It is a mailto: on purpose — no form service, no third
     party holding every address that lands on this page — and it degrades to
     a plain email if a browser has no mail handler. -->
{% assign waitlist_email = "suryanshgupta9933@gmail.com" %}

# Brotto Cloud

<h2>What it is</h2>

<p>
  We run the orchestrator at <code>agent.brotto.dev</code>, you use the same
  extension, and there is nothing to install but the extension itself. Sign in
  with your email, get a six-digit code, and ask for something in the tab you
  are already signed in to.
</p>

<p>
  Only who runs the server changes. Same extension, same three gates, same
  eight model providers, the same API key you already have.
</p>

<h2>Who it is for</h2>

<p>
  For you if you want to try Brotto without standing up a server — no
  container, no <code>.env</code>, no terminal.
</p>

<p>
  It is not the better version. Self-hosting is, and it is
  <a href="/#try">free and permanent</a>. This is the convenience path beside
  it, not a replacement for it.
</p>

<h2>What it costs</h2>

<p>
  Nothing during the beta. There are limits, because it is our compute: a
  number of tasks a week, and a ceiling on what a single task may spend. If you
  want no cap on either, self-host.
</p>

<h2>What we can see</h2>

<p>
  Page observations pass through a machine we run, for as long as the task is in
  flight. That is inherent to how the agent works — it is true of a self-hosted
  install too, where the machine is yours and there is no operator on the other
  end. What differs is that here the operator is us, and it is worth being
  exact about what that means.
</p>

<div class="cardgrid cardgrid--2" style="margin-top: 26px;">
  <div>
    <h3>Only while a task runs</h3>
    <p>
      The relay holds observations for the life of the task and no longer. That
      disk is ephemeral: a restart or a deploy erases it.
    </p>
  </div>
  <div>
    <h3>Stripped before it goes further</h3>
    <p>
      Credentials, API keys, bearer tokens, card numbers and government
      identifiers are redacted in code on every task, before anything reaches
      your model provider. No setting turns it off.
    </p>
  </div>
  <div>
    <h3>No analytics, no third party</h3>
    <p>
      No telemetry, no advertising, nothing sold or shared. You bring your own
      model key, so your model provider sees your page — as it does on any
      deployment.
    </p>
  </div>
  <div>
    <h3>Yours to delete</h3>
    <p>
      Every session has a delete button in the panel. Self-hosting is the
      version where the record is yours to keep on your own disk.
    </p>
  </div>
</div>

<p class="section-note" style="margin-top: 24px;">
  All of this is written out in full, for both deployments, in
  <a href="/privacy">Privacy</a> and <a href="/security">Security</a>.
</p>

<h2>Ask for an invitation</h2>

<form class="waitlist" action="mailto:{{ waitlist_email }}" method="post"
      enctype="text/plain">
  <label class="label" for="waitlist-email">Your email</label>
  <div class="actions waitlist-row">
    <input id="waitlist-email" name="email" type="email" required
           autocomplete="email" placeholder="you@example.com"
           aria-describedby="waitlist-note">
    <button class="btn" type="submit">Ask for an invite</button>
  </div>
  <p class="section-note" id="waitlist-note" style="margin-top: 14px;">
    This opens your own mail app — there is no form service behind it, no
    account, and nothing on this page that records who you are. The address is
    used to send an invitation and nothing else, and one reply unsubscribes.
    If mail does not open, write to
    <a href="mailto:{{ waitlist_email }}">{{ waitlist_email }}</a>.
  </p>
</form>

<h2>If you would rather just run it</h2>

<p>
  Brotto is Apache 2.0 and the self-hosted install is free and permanent. One
  container, one extension, about six steps, and everything Brotto keeps stays
  on your own disk. That is the whole product; this page is the shortcut past
  the install.
</p>

<p class="section-note">
  <a href="/#try">Install Brotto yourself</a> ·
  <a href="/">Back to the front page</a>
</p>