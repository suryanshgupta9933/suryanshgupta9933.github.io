---
layout: default
title: The closed beta
description: What the Brotto Cloud closed beta is, what it gives you, and what we can see while it runs.
---

# The closed beta

<p>
  You have been admitted to Brotto Cloud: the same extension, with our server
  running it instead of yours. This page is what that means in practice — what
  you get, what we ask of you, and exactly what we can see while it runs.
</p>

<h2>What you get</h2>

<p>
  <strong>100 tasks a week</strong>, and the count resets every Monday. It is
  generous on purpose: the thing we are watching for is whether you come back
  and use it, and a cap low enough to interrupt somebody mid-week would be
  measuring the wrong thing.
</p>

<p>
  No cap on how long a single task runs. If a job is going to take twenty
  minutes, it takes twenty minutes. A per-task spend ceiling is planned, not
  on today: until it ships, a task spends whatever your provider charges for
  the tokens it uses, with no Brotto-imposed ceiling. If you want a hard limit
  now, <a href="/self-host">run it yourself</a> and use your provider's own
  budget controls.
</p>

<p>
  You still bring your own model key, so the page you are looking at goes to
  your provider and not to us. The provider catalogue is the same one the
  self-hosted install reads.
</p>

<p>
  <strong
    ><a href="https://chromewebstore.google.com/detail/brotto/mahkomofcmohephggjlfgocopgfhkggb"
      >Add Brotto to Chrome</a
    ></strong
  >, sign in with your email, get a six-digit code, and ask for something in the
  tab you are already signed in to. That is the whole setup.
</p>

<h2>What we ask of you</h2>

<p>
  Two things, and they are the whole ask.
</p>

<p>
  <strong>Tell us when it breaks.</strong> When a run fails, the panel offers to
  send us the reason code and your account id. Refusing it costs you nothing
  except that we find out about the bug from somebody else.
</p>

<p>
  <strong>Just reply.</strong> The address we invited is a mailbox somebody
  reads. A sentence about what you tried and what happened is worth more to us
  than any form.
</p>

<h2>What we can see</h2>

<p>
  Page observations pass through a machine we run, for as long as the task is in
  flight. That is inherent to how the agent works &mdash; it is true of a
  self-hosted install too, where the machine is yours and there is no operator
  on the other end. What differs here is that the operator is us, and it is
  worth being exact about what that means.
</p>

<div class="cardgrid cardgrid--2" style="margin-top: 26px;">
  <div>
    <h3>Thirty days, then gone</h3>
    <p>
      Each run's record is deleted automatically 30 days after it last moved.
      That is its prompts, its actions and its timings &mdash; never the page
      text, which is not written down at all. A restart or a deploy clears the
      disk as well.
    </p>
  </div>
  <div>
    <h3>Stripped before it goes further</h3>
    <p>
      Credentials, API keys, bearer tokens and card numbers are redacted in code
      before page text reaches your model provider. It is a best-effort pattern
      match rather than a guarantee, and
      <a href="/privacy">the policy</a> says exactly what it covers.
    </p>
  </div>
  <div>
    <h3>Nothing sold, nothing profiled</h3>
    <p>
      No analytics, no advertising, nothing sold or shared. We keep two things.
      A failure log &mdash; when a run breaks, the reason code and your account
      id, so we can find the bug and fix it. And one record per sign-in: your
      account id, the network you came from (a /24 or /48, not the address),
      and the browser, so we can tell a new laptop from somebody else holding
      the account. No page content, no prompts, no task text, no URLs.
    </p>
  </div>
  <div>
    <h3>Yours to delete</h3>
    <p>
      Every session has a delete button in the panel. You can also leave, at
      any time, by replying to the invitation &mdash; there is nothing to
      uninstall first, and writing back is the whole exit.
    </p>
  </div>
</div>

<p class="section-note" style="margin-top: 24px;">
  All of this is written out in full, for both deployments, in
  <a href="/privacy">Privacy</a> and <a href="/security">Security</a>.
</p>

<h2>When it ends</h2>

<p>
  The beta ends when it ends. There is no announced date and nothing is
  scheduled; what we are looking for is whether a few people keep choosing this
  over installing it themselves. If it stops being worth our time to run, we
  will say so, and anyone who wants to keep it forever can
  <a href="/self-host">self-host</a> &mdash; which is free, permanent, and was never
  part of the beta to begin with.
</p>

<p class="section-note">
  <a href="/waitlist">About the beta, and the invite list</a> &middot;
  <a href="/privacy">Privacy</a> &middot;
  <a href="/">Back to the front page</a>
</p>