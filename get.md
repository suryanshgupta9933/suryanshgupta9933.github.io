---
layout: default
title: Get Brotto
wide: true
description: Two ways to run Brotto — install it yourself, free and permanent, or ask for a seat on the Brotto Cloud beta. Same extension, same gates, same model key.
---

# Get Brotto

<p class="section-note" style="margin-top: -6px;">
  Two ways to run it. The same extension, the same three gates that cannot be
  switched off, and the same model key you already have — what changes is who
  runs the server.
</p>

<!-- The fork in one glance. The middle box is the only one that differs, so
     it carries the heavier rule — hierarchy by border weight, same as the
     rest of the system. -->
<figure>
  <img src="/assets/diagrams/two-ways-to-run.svg" width="900" height="420" loading="lazy"
    alt="Two ways to run the same extension. On your machine, the extension talks to a container on your disk and then to your model provider. On our machine, the extension talks to agent.brotto.dev and then to the same provider. Only the middle box changes.">
  <figcaption>Only the middle box changes. Same extension, same key, same three gates.</figcaption>
</figure>

<div class="cardgrid cardgrid--2 cardgrid--fork" style="margin-top: 36px;">
  <div>
    <span class="card-idx label">Option 01</span>
    <h3>Run it yourself</h3>
    <p>
      One container on your machine — the agent loop, not a browser, about
      510&nbsp;MB — and the extension from the Chrome Web Store.
    </p>
    <ul>
      <li>Free, permanent, Apache 2.0. No account, no operator, no cap.</li>
      <li>Everything it keeps lands on your disk. Read it, export it, delete it.</li>
      <li>Your model key, your provider, your money. Cost is nothing beyond the
        calls you make.</li>
    </ul>
    <div class="actions">
      <a class="btn" href="/self-host">Install it yourself</a>
    </div>
  </div>
  <div>
    <span class="card-idx label">Option 02</span>
    <h3>Brotto Cloud <span class="badge label">Beta</span></h3>
    <p>
      We run the orchestrator at <code>agent.brotto.dev</code>. Nothing to
      install but the extension itself.
    </p>
    <ul>
      <li>Invite-only, admitted in batches. Not open signup.</li>
      <li>Free during the beta, because it is our compute: a weekly task cap.</li>
      <li>Still your model key — we run the agent, not the model.</li>
    </ul>
    <div class="actions">
      <a class="btn" href="/waitlist">Join Waitlist</a>
    </div>
  </div>
</div>

<h2>Side by side</h2>

<table class="spec spec--fork">
  <tr>
    <th scope="col">Two ways</th>
    <th scope="col">Run it yourself</th>
    <th scope="col">Brotto Cloud</th>
  </tr>
  <tr>
    <td>Server</td>
    <td>You run it</td>
    <td>We run it, at <code>agent.brotto.dev</code></td>
  </tr>
  <tr>
    <td>Account</td>
    <td>None</td>
    <td>Email and a six-digit code</td>
  </tr>
  <tr>
    <td>Cost</td>
    <td>Nothing, beyond the model calls you make</td>
    <td>Free during the beta</td>
  </tr>
  <tr>
    <td>Task cap</td>
    <td>None</td>
    <td>A weekly task cap</td>
  </tr>
  <tr>
    <td>Per-task spend</td>
    <td>Your call — your provider's own budget controls</td>
    <td>No ceiling yet. A task spends what your provider charges; a Brotto
      ceiling is planned.</td>
  </tr>
  <tr>
    <td>Page text in flight</td>
    <td>Through a machine you run</td>
    <td>Through a machine we run</td>
  </tr>
  <tr>
    <td>Run record</td>
    <td>Your disk</td>
    <td>Our machine, swept after 30 days</td>
  </tr>
  <tr>
    <td>Model key</td>
    <td>Yours — your provider sees your page</td>
    <td>Yours — your provider sees your page</td>
  </tr>
  <tr>
    <td>How long</td>
    <td>Permanent. Apache 2.0.</td>
    <td>A beta that may not become a permanent service</td>
  </tr>
</table>

<p class="section-note">
  A per-task spend ceiling is planned, not on today. Until it ships, a task
  spends whatever your provider charges for the tokens it uses — there is no
  Brotto-imposed ceiling. If you want a hard limit now,
  <a href="/self-host">run it yourself</a> and use your provider's own budget
  controls: that is the version where the spend is already yours to cap.
</p>

<p class="section-note">
  What the cloud beta keeps, and what it does not, is written out in full on
  <a href="/waitlist">Brotto Cloud</a> and in
  <a href="/privacy">the privacy policy</a>. An invitation is not a
  subscription.
</p>

<div class="split">
  <div class="claim">
    <span class="eyebrow label">Which one?</span>
    <h2>Self-hosting is the product</h2>
    <p>
      Free, permanent, and the version with no operator on the other end.
      Brotto Cloud is the convenience path beside it — no container, no
      terminal — and it is a beta that exists to answer a few questions about
      how people actually use this. It may not become a permanent hosted
      service.
    </p>
  </div>
  <div>
    <p>
      Pick the one that fits today; neither is the upgrade of the other.
    </p>
    <p>
      Either way the free build is the whole product, nothing about it is on
      sale, and the three gates stay on. If you would rather look before you
      choose, <a href="/screens">Screens</a> shows one real run from the first
      sentence to the last click.
    </p>
    <div class="cardgrid cardgrid--2">
      <div>
        <h3>Run it yourself</h3>
        <p>
          Free, permanent, Apache 2.0. No account, no operator, no cap —
          <a href="/self-host">the install</a> is one page.
        </p>
      </div>
      <div>
        <h3>Brotto Cloud</h3>
        <p>
          Same extension, someone else's server, invite-only while it is in
          beta. <a href="/waitlist">Join the waitlist</a>.
        </p>
      </div>
    </div>
  </div>
</div>

<p class="section-note">
  Brotto is Apache 2.0 and stays that way.
  <a href="/">Back to the front page</a> ·
  <a href="/privacy">Privacy</a> ·
  <a href="/security">Security</a>
</p>
