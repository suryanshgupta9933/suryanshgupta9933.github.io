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
  your provider and not to us. The same providers the self-hosted install
  supports.
</p>

<p>
  <strong
    ><a href="https://chromewebstore.google.com/detail/brotto/kblfiddjaeekmlpmgpgchcfbakjhflpd"
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

<figure>
  <img src="/assets/diagrams/what-the-relay-keeps.svg" width="900" loading="lazy"
    alt="Two records only — a failure log, and one row per sign-in. Page content, prompts, task text, URLs and model responses are on the other side of a hard line and never written down.">
  <figcaption>Two records, and a hard line after them.</figcaption>
</figure>

<div class="cardgrid cardgrid--2">
  <div>
    <h3>Still there when you come back</h3>
    <p>
      A run's record stays &mdash; its prompts, its actions, its timings &mdash;
      so the task is there when you return to it. Never the page text, which is
      not written down at all.
    </p>
  </div>
  <div>
    <h3>Stripped before it goes further</h3>
    <p>
      Credentials, API keys, bearer tokens and card numbers are redacted in code
      before page text reaches your model provider.
      <a href="/privacy">The policy</a> says exactly what it covers.
    </p>
  </div>
  <div>
    <h3>Nothing sold, nothing profiled</h3>
    <p>
      No advertising, nothing sold or shared. We do take product analytics
      &mdash; counts of whether people can run a task, not what the task was.
      A failure log and one record per sign-in exist too;
      <a href="/privacy">Privacy</a> lists every field.
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

<p class="section-note">
  All of this is written out in full, for both deployments, in
  <a href="/privacy">Privacy</a> and <a href="/security">Security</a>.
</p>

<h2>When it ends</h2>

<p>
  There is no announced end date and nothing is scheduled. If that changes, we
  will write to the address we invited and say what happens next.
  <a href="/self-host">Self-hosting</a> is not part of the beta: free,
  permanent, Apache 2.0, and yours to run.
</p>

<p class="section-note">
  <a href="/waitlist">About the beta, and the invite list</a> &middot;
  <a href="/privacy">Privacy</a> &middot;
  <a href="/">Back to the front page</a>
</p>