---
layout: default
title: Brotto Cloud — Beta
description: The hosted version of Brotto, by invitation — the same extension with someone else's server running it. Free during the beta, capped, honest.
---

<!-- THE ONE PLACE THE ADDRESS LIVES.
     `waitlist_email` below is the single source for the form action, the
     visible fallback address, the mailto link and the two messages the script
     prints. Change it here and all of them move together.

     The form's action is still a mailto: on purpose. It is what runs when
     JavaScript is off, which is the only path that works without us: no form
     service, no third party holding every address that lands on this page.
     With JavaScript on, the script below intercepts the submit and posts to our
     own relay instead — our server, no one else's. -->
{% assign waitlist_email = "suryanshgupta9933@gmail.com" %}

<h1>Brotto Cloud <span class="badge label">Beta</span></h1>

<h2>What it is</h2>

<p>
  We run the server at <code>agent.brotto.dev</code>, you use the same
  extension, and there is nothing to install but the extension itself. Sign in
  with your email, get a six-digit code, and ask for something in the tab you
  are already signed in to.
</p>

<p>
  Only who runs the server changes. Same extension, same three gates, same
  eight model providers, the same API key you already have.
</p>

<!-- Batched admission, as it actually works: addresses wait, a batch opens,
     an invitation lands. No queue number, because there is not one — and the
     last line is the one the copy keeps making. -->
<figure>
  <img src="/assets/diagrams/batched-invites.svg" width="900" height="280" loading="lazy"
    alt="Admission in batches. Addresses sit on a list with no queue number. When a batch opens, a few seats fill now and the rest wait. What arrives is an email, a six-digit code and the same extension. What it is not: open signup or a paid tier.">
  <figcaption>Admitted in batches, not as addresses arrive. An invitation is not a subscription.</figcaption>
</figure>

<h2>Who it is for</h2>

<div class="cardgrid cardgrid--2">
  <div>
    <h3>For you if</h3>
    <p>
      You want to try Brotto without standing up a server — no container, no
      <code>.env</code>, no terminal.
    </p>
  </div>
  <div>
    <h3>The convenience path</h3>
    <p>
      No container, no terminal &mdash; we run the server.
      <a href="/self-host">Self-hosting</a> stays free and permanent on your
      own disk.
    </p>
  </div>
</div>

<h2>What it costs</h2>

<p>
  Nothing during the beta. There is one limit, because it is our compute: a
  number of tasks a week. If you want no cap on that,
  <a href="/self-host">run it yourself</a>.
</p>

<p>
  A per-task spend ceiling is planned, not on today. Until it ships, a task
  spends whatever your provider charges for the tokens it uses — there is no
  Brotto-imposed ceiling. If you want a hard limit now, run it yourself and
  use your provider's own budget controls: that is the version where the spend
  is already yours to cap.
</p>

<h2>What we can see</h2>

<p>
  Page observations pass through a machine we run, for as long as the task is in
  flight. That is inherent to how the agent works — it is true of a self-hosted
  install too, where the machine is yours and there is no operator on the other
  end. What differs is that here the operator is us, and it is worth being
  exact about what that means.
</p>

<div class="cardgrid cardgrid--2">
  <div>
    <h3>Still there when you come back</h3>
    <p>
      A run's record stays — its prompts, its actions, its timings — so the
      task is there when you return to it. Never the page text, which is not
      written down at all.
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
      No advertising, nothing sold or shared. We do take product analytics —
      counts of whether people can run a task, not what the task was. A failure
      log and one record per sign-in exist too;
      <a href="/privacy">Privacy</a> lists every field.
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

<p class="section-note">
  All of this is written out in full, for both deployments, in
  <a href="/privacy">Privacy</a> and <a href="/security">Security</a>.
</p>

<h2>Join the waitlist</h2>

<form class="waitlist" id="waitlist-form" method="post"
      action="mailto:{{ waitlist_email }}" enctype="text/plain"
      data-endpoint="https://agent.brotto.dev/v1/waitlist">
  <label class="label" for="waitlist-name">Name (optional)</label>
  <input id="waitlist-name" name="name" type="text" maxlength="64"
         autocomplete="name" spellcheck="false">

  <label class="label" for="waitlist-email">Your email</label>
  <div class="actions waitlist-row">
    <input id="waitlist-email" name="email" type="email" required
           autocomplete="email" placeholder="you@example.com">
    <button class="btn" type="submit">Join Waitlist</button>
  </div>
  <p class="section-note" id="waitlist-msg" role="status" aria-live="polite"
     style="margin-top: 14px; display: none;"></p>
</form>

<div class="waitlist-done" id="waitlist-done" role="status" tabindex="-1" hidden>
  <p class="waitlist-done-mark" aria-hidden="true">&check;</p>
  <h3 class="waitlist-done-h">You are on the list</h3>
  <p class="waitlist-done-p">
    We will write to <span id="waitlist-echo"></span> when there is an invite,
    and once in a while after that with something worth reading.

    Or skip the wait entirely — <a href="/self-host">install Brotto yourself</a>.
    It is free, permanent, and yours.
  </p>
</div>

<script>
// Progressive enhancement over the mailto: form above. The form still submits
// to the mail client when this does not run or when fetch is unavailable, so
// the page is never a dead button; this just makes the address arrive without
// a person having to compose it.
//
// Every branch says something. A form that fails silently is worse than no
// form, because the visitor leaves believing they are on a list they are not.
(function () {
  var form = document.getElementById('waitlist-form');
  if (!form || !window.fetch) return;
  var input = document.getElementById('waitlist-email');
  var nameInput = document.getElementById('waitlist-name');
  var button = form.querySelector('button[type="submit"]');
  var msg = document.getElementById('waitlist-msg');
  var done = document.getElementById('waitlist-done');
  var echo = document.getElementById('waitlist-echo');
  var ADDRESS = '{{ waitlist_email }}';

  // One line per status the relay can return. 404 is deliberately not folded
  // into the generic case: it is not the visitor's fault and not a transient
  // fault, it means this page is pointed at a server with no waitlist
  // configured, and the owner needs to see that rather than see "try later".
  var REPLIES = {
    400: 'That does not look like a valid email address — check it and try again.',
    429: 'Too many attempts from this browser — wait a few minutes and try again.',
    502: 'We could not write your address to the list, so nothing was sent. Try again in a little while.',
    404: 'The invite list is not switched on on our server, so nothing was sent. Write to ' + ADDRESS + ' and we will add you by hand.'
  };

  function say(text, colour) {
    msg.textContent = text;
    msg.style.color = colour;
    msg.style.display = 'block';
  }

  form.addEventListener('submit', function (event) {
    event.preventDefault();
    var email = input.value.trim();
    if (!email) return;

    button.disabled = true;
    button.textContent = 'Sending…';
    msg.style.display = 'none';

    fetch(form.dataset.endpoint, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      // `name` is optional and the relay treats a missing one the same as an
      // empty one — same two keys the extension's own waitlist form sends.
      body: JSON.stringify({
        email: email,
        name: nameInput ? nameInput.value.trim() : ''
      })
    }).then(function (res) {
      // A proxy or a crash can answer with HTML, so the body is not trusted
      // to be JSON; the status line is what decides the message.
      return res.json().catch(function () { return {}; }).then(function (body) {
        return { status: res.status, ok: res.ok, body: body };
      });
    }).then(function (result) {
      if (result.ok && result.body.ok === true) {
        // The confirmation replaces the form rather than printing under it,
        // so the answer is the thing on screen and not a line of small grey
        // text under a button that has already gone dead.
        //
        // One message for a new address and one already on the list. The
        // relay answers both with 200 on purpose — a form that says "you are
        // already signed up" is a way to ask whether a stranger is on it.
        button.disabled = true;
        button.textContent = 'On the list';
        echo.textContent = email;
        form.hidden = true;
        done.hidden = false;
        done.focus();
        return;
      }
      var known = REPLIES[result.status];
      say(known || 'That did not go through, so nothing was sent. Try again, or write to ' + ADDRESS + '.',
          'var(--bad)');
      button.disabled = false;
      button.textContent = 'Join Waitlist';
    }).catch(function () {
      say('That never reached us, so nothing was sent. Check your connection and try again, or write to ' + ADDRESS + '.',
          'var(--bad)');
      button.disabled = false;
      button.textContent = 'Join Waitlist';
    });
  });
})();
</script>

<h2>If you would rather just run it</h2>

<p>
  Brotto is Apache 2.0 and the self-hosted install is free and permanent. One
  container, and a one-click
  <a href="https://chromewebstore.google.com/detail/brotto/kblfiddjaeekmlpmgpgchcfbakjhflpd"
    >Chrome Web Store install</a
  >; everything Brotto keeps stays on your own disk. That is the whole product;
  this page is the shortcut past the install.
</p>

<p class="section-note">
  <a href="/closed-beta">Already in the closed beta</a> ·
  <a href="/self-host">Install Brotto yourself</a> ·
  <a href="/">Back to the front page</a>
</p>