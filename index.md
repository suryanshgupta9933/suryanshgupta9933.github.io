---
layout: default
title: Brotto — an AI browser agent that runs where you're already signed in
wide: true
description: Brotto is a self-hosted AI browser agent for Chrome. It works in the tab you are already signed in to, asks before anything you cannot undo, and writes down exactly what it did. Apache 2.0, bring your own key.
---

<div class="hero">
  <div>
    <img class="hero-mark" src="/assets/logo.svg" alt="">
    <h1 class="hero-title">Brotto</h1>
    <p class="hero-line">It asks before it does anything you can't undo — and you can see exactly what it did.</p>
    <p class="hero-sub">
      Brotto is a Chrome extension and an AI agent that carries out a task in
      the browser tab you are already signed in to. Your inbox, your bank, your
      admin panel. Not a cloud browser you have never logged into, and not a
      screenshot of a page it cannot read.
    </p>
    <div class="actions">
      <a class="btn" href="#try">Get Brotto</a>
      <a class="btn btn--ghost" href="#what">See what it does</a>
      <a class="btn btn--ghost" href="/screens">Screens</a>
    </div>
    <div class="soon-row">
      <span class="soon">Chrome Web Store · Under review</span>
      <span>One click to install as soon as it clears. Until then it is one container and one extension.</span>
    </div>
  </div>

  <!-- The panel's own status bar, rebuilt in markup with the numbers a real
       run produced: 14 steps, 41.2% context used, outcome DONE. Text stays
       text, so it is readable, selectable and sharp on any screen — none of
       which a screenshot is. The video below it is a showcase, not this run. -->
  <div class="hero-panel">
    <div class="statusbar">
      <div class="cell"><span class="label">Steps</span><span class="value">14</span></div>
      <div class="cell"><span class="label">Active</span><span class="value">377.3s</span></div>
      <div class="cell"><span class="label">Context</span><span class="value">41.2%</span></div>
      <div class="cell outcome" data-state="done">
        <span class="label">Outcome</span><span class="value">Done</span>
      </div>
    </div>
    <figure class="demo">
      <video controls playsinline preload="metadata" poster="/assets/poster.jpg">
        <source src="/assets/brag.mp4" type="video/mp4">
        Your browser cannot play this video. <a href="/assets/brag.mp4">Download it instead.</a>
      </video>
      <figcaption>
        Twenty-five seconds of Brotto: the panel, a task being read, an approval
        coming back, a run finishing. A tour of the shapes you will see — for one
        task in full, see <a href="/screens">Screens</a>.
      </figcaption>
    </figure>
  </div>
</div>

<div class="split" id="what">
  <div class="claim">
    <span class="eyebrow label">What it does</span>
    <h2>Three things worth asking it</h2>
    <p>
      There is no form and no workflow to learn. The panel is a chat box, so
      whatever you can describe is the whole interface.
    </p>
  </div>
  <div class="cardgrid">
    <div>
      <span class="card-idx label">01</span>
      <h3 class="ask">"Find me the cheapest direct flight to Lisbon in November."</h3>
      <p>
        It searches, compares and answers — and stops dead before it spends
        your money, because that part is yours.
      </p>
    </div>
    <div>
      <span class="card-idx label">02</span>
      <h3 class="ask">"Pull Q3 numbers from the admin panel and summarise them."</h3>
      <p>
        Your cookies, your SSO and your MFA are already there, so there is
        nothing to sign in to and no second browser to trust.
      </p>
    </div>
    <div>
      <span class="card-idx label">03</span>
      <h3 class="ask">"Add a branch protection ruleset to our repo."</h3>
      <p>
        The real run on <a href="/screens">the screens page</a>, start to
        finish. It stops twice, both times on decisions only you can make.
      </p>
    </div>
  </div>
</div>

<div class="split" id="how">
  <div class="claim">
    <span class="eyebrow label">Why you can leave it running</span>
    <h2>An agent holding your cookies</h2>
    <p>
      One wrong click and an agent with your sessions can do a lot of damage as
      <em>you</em>. Three things are built around that, and none of them can be
      switched off.
    </p>
    <p>
      An agent you can disable the safety on is an agent you cannot leave
      running. That is the whole argument for having the gates at all.
    </p>
  </div>
  <div class="cardgrid" style="grid-template-columns: 1fr;">
    <div>
      <span class="card-idx label">Gate 01</span>
      <h3>It stops and asks before anything irreversible</h3>
      <p>
        Before it sends an email, takes a payment, deletes something, publishes
        or changes a password — and before it visits a domain for the first time.
        The card names the action, so approving it is a decision and not a
        gesture.
      </p>
      <span class="gate-lock label">No setting turns this off</span>
    </div>
    <div>
      <span class="card-idx label">Gate 02</span>
      <h3>It writes down what it did</h3>
      <p>
        Every run produces a per-session record — each observation, prompt,
        action, approval and timing — in a document on your disk. That is what
        lets you read a run back afterwards, resume one that was interrupted,
        or delete it outright. It is a record, not a chat transcript.
      </p>
      <span class="gate-lock label">A file, not a database</span>
    </div>
    <div>
      <span class="card-idx label">Gate 03</span>
      <h3>It tells you why it couldn't act</h3>
      <p>
        When a button is off-screen, covered by a cookie banner, or disabled,
        Brotto says so on the line the model reads — and records the reason
        <em>without a coordinate</em>, so it never retries the same wrong click.
      </p>
      <span class="gate-lock label">A reason, not a retry</span>
    </div>
  </div>
</div>

<div class="split split--flip">
  <div class="claim">
    <span class="eyebrow label">The part everyone asks about</span>
    <h2>It stops before it spends your money</h2>
    <p>
      Booking a flight costs real money and cannot be undone with an undo
      button, so the agent asks first. Every time — not the first time, not
      only when it is unsure.
    </p>
    <p>
      This is the same card you get for a sign-in it cannot pass, a delete it
      cannot undo, or a domain it has never visited. It has no way to approve
      itself, and neither would anything you installed later.
    </p>
  </div>

  <!-- The panel below is not an illustration. It is the actual card the
       extension renders, rebuilt in markup so you can read what it says. -->
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

      <div class="card">
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
</div>

<div class="split">
  <div class="claim">
    <span class="eyebrow label">Why it's built this way</span>
    <h2>Two decisions, and everything else follows</h2>
    <p>
      Most browser agents run somewhere you have never logged in. A cloud browser
      has no cookie jar, so every site starts at the sign-in wall — and no
      reputation, so the sites you actually care about serve it a bot challenge.
    </p>
  </div>
  <div>
    <div class="arch">
      <div class="node">
        <span class="label">Your machine</span>
        <b>Chrome extension</b>
        <span>A pure actuator. Handed a target, asked for a box model.</span>
      </div>
      <div class="link">
        <span class="label">WebSocket</span>
      </div>
      <div class="node">
        <span class="label">Your machine</span>
        <b>Container</b>
        <span>The agent loop. Chrome suspends idle MV3 workers, so the loop does not live here.</span>
      </div>
      <div class="link">
        <span class="label">Your key</span>
      </div>
      <div class="node">
        <span class="label">Your provider</span>
        <b>Any of eight</b>
        <span>Anthropic, OpenAI, Gemini, MiniMax, OpenRouter, DeepSeek, Groq, or your own.</span>
      </div>
    </div>
    <div class="cardgrid cardgrid--2" style="margin-top: 26px;">
      <div>
        <h3>It drives your tab, not a cloud browser</h3>
        <p>
          Your cookies, your MFA, your SSO: simply there. Nothing to sign in to,
          because it is already signed in.
        </p>
      </div>
      <div>
        <h3>It reads the accessibility tree, not pixels</h3>
        <p>
          Roles, labels, values and stable references — the structure a screen
          reader already navigates by. No vision model, no image tokens.
        </p>
      </div>
    </div>
  </div>
</div>

<div class="band">
  <div class="claim">
    <span class="eyebrow label">In the panel</span>
    <h2>Three cards</h2>
    <p>
      Brotto stops and asks rather than guessing. A site it has not visited, a
      question only you can answer, a sign-in only you can do. Each one resolves
      in place, so the run reads as a conversation and not a log — and these are
      the real panel, rendered from the extension itself.
      <a href="/screens">All seven screens</a>, including one run in four moments.
    </p>
  </div>
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
</div>

<div class="split" id="try">
  <div class="claim">
    <span class="eyebrow label">Install</span>
    <h2>One container, one extension</h2>
    <p>
      The container holds the agent loop; it never launches a browser. About
      510 MB, most of which is the model provider SDKs rather than Chromium.
    </p>
    <p>
      Six steps, and they are on their way out — a one-command installer is next,
      then a hosted option. Everything Brotto keeps lands in one Docker volume on
      your disk.
    </p>
  </div>
  <div>
<pre><code>git clone https://github.com/suryanshgupta9933/Brotto.git
cd Brotto

cp .env.example .env      # set AGENT_SECRET to any long random string
docker compose up -d</code></pre>
<p class="section-note" style="margin-top: 22px;">
  That is the whole server, and it listens on <code>:8000</code> with no browser
  in it. Then build and load the extension:
</p>
<pre><code>cd clients/brotto-extension
npm ci &amp;&amp; npm run build</code></pre>
<p class="section-note" style="margin-top: 22px;">
  In Chrome, open <code>chrome://extensions</code>, turn on
  <b>Developer mode</b>, and <b>Load unpacked</b> →
  <code>clients/brotto-extension/dist</code>. Open the Brotto side panel, set the
  server address to <code>http://127.0.0.1:8000</code>, paste
  <code>AGENT_SECRET</code> into <b>Settings → Connection</b>, and paste your
  model key under <b>Settings → Model</b>. The key is held in memory for the run
  and never written to disk.
</p>
    <table class="spec">
      <tr><td>Licence</td><td>Apache 2.0 — read it, fork it, ship it</td></tr>
      <tr><td>Cost</td><td>Nothing, beyond the model calls you make</td></tr>
      <tr><td>Your data</td><td>Audit files on your disk. The server transits page text and never stores it.</td></tr>
      <tr><td>Providers</td><td>Eight, or any OpenAI-compatible endpoint you run</td></tr>
      <tr><td>Chrome only</td><td><code>chrome.debugger</code> has no Firefox equivalent</td></tr>
    </table>
    <p class="section-note" style="margin-top: 22px;">
      Full instructions, honest limitations and the roadmap are on
      <a href="https://github.com/suryanshgupta9933/Brotto">GitHub</a>.
    </p>
  </div>
</div>

<div class="split">
  <div class="claim">
    <span class="eyebrow label">Next</span>
    <h2>Not built yet</h2>
    <p>
      Ordered by what unblocks the most people. Two of these are the reason a
      person who doesn't write code cannot use Brotto yet, and removing them is
      the top priority rather than a someday item.
    </p>
  </div>
  <div class="cardgrid">
    <div>
      <span class="card-idx label">01 · Soon</span>
      <h3>The store listing clears</h3>
      <p>
        The extension becomes one click to install. That takes the install from
        six steps to one, and it needs nothing from us but a review.
      </p>
    </div>
    <div>
      <span class="card-idx label">02 · Planned</span>
      <h3>Remove the last step</h3>
      <p>
        A one-command installer for the container, then a hosted option — at
        which point there is nothing left to run yourself.
      </p>
    </div>
    <div>
      <span class="card-idx label">03 · Planned</span>
      <h3>Canvas surfaces</h3>
      <p>
        Google Sheets genuinely draws to a canvas and is the one place Brotto is
        blind. Worth checking separately; Docs renders a real DOM.
      </p>
    </div>
    <div>
      <span class="card-idx label">04 · Planned</span>
      <h3>A published benchmark</h3>
      <p>
        Until it scores real runs, any reliability number in this space is a
        guess — including ours. The harness measures perception and actions
        with no model in the loop.
      </p>
    </div>
    <div>
      <span class="card-idx label">05 · Planned</span>
      <h3>Routines</h3>
      <p>
        Saved, reusable tasks — <em>every weekday, summarise these</em> — and
        re-running or resuming from the record.
      </p>
    </div>
    <div>
      <span class="card-idx label">06 · Not released</span>
      <h3>Pro</h3>
      <p>
        Multi-tab parallelism, a speed pack, routines and per-run cost caps.
        Brotto stays Apache 2.0, and the free build is the whole product as it
        stands.
      </p>
    </div>
  </div>
</div>

<div class="split">
  <div class="claim">
    <span class="eyebrow label">Where your data goes</span>
    <h2>Your pages reach the model. They do not reach anyone else.</h2>
    <p>
      The browser runs on your machine. The agent loop runs on a server
      <em>you</em> run, so page observations transit it — that is inherent to
      the design. What you choose is that nobody is on the other end.
    </p>
  </div>
  <div>
    <div class="cardgrid cardgrid--2">
      <div>
        <h3>Page text is redacted first</h3>
        <p>
          Credentials, API keys, bearer tokens, card numbers and government
          identifiers are stripped before it reaches the provider — in code, on
          every task, with no setting to disable it.
        </p>
      </div>
      <div>
        <h3>Nothing but a digest reaches disk</h3>
        <p>
          A run leaves a 200-character digest of each page rather than a copy.
          What you typed and the model's prose about it do persist in the record.
        </p>
      </div>
      <div>
        <h3>Your key never touches disk</h3>
        <p>
          Held in memory for the run, by Brotto, anywhere. There is no account,
          no credit balance and nothing to top up.
        </p>
      </div>
      <div>
        <h3>Deletion is yours</h3>
        <p>
          Every session has a delete button with a confirmation, and
          <code>DELETE /v1/sessions</code> takes the lot.
        </p>
      </div>
    </div>
    <p class="section-note" style="margin-top: 24px;">
      Both of those are written out in full:
      <a href="/privacy">Privacy</a> and <a href="/security">Security</a>.
    </p>
  </div>
</div>

<div class="split" id="writing">
  <div class="claim">
    <span class="eyebrow label">Writing</span>
    <h2>How it actually works</h2>
    <p>
      Notes on the parts of this that took the most work, written for anyone
      deciding whether to trust a browser agent with their own session.
    </p>
  </div>
  <div>
    <ul class="post-list">
      <li>
        <a href="/blog/2026-10-09-what-an-agent-holding-your-cookies-can-do.html">An agent holding your cookies</a>
        <span class="post-when">2026-10-09</span>
        <span class="post-stand">What an agent with your sessions can do as <em>you</em>, the three
        gates that stop it, and the fact that all of them are made of strings.</span>
      </li>
    </ul>
    <p class="section-note" style="margin-top: 22px;">
      <a href="/writing">All writing</a>
    </p>
  </div>
</div>