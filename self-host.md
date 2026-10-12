---
layout: default
title: Run it yourself
wide: true
description: How to run Brotto on your own machine — paste a prompt into your AI coding tool, or follow the steps by hand. Free, permanent, Apache 2.0, no account.
---

# Run it yourself

<p class="section-note" style="margin-top: -6px;">
  One container on your machine — the agent loop, not a browser, about
  510&nbsp;MB — and the extension in Chrome. Free, permanent, Apache 2.0. No
  account, no operator, no cap. Everything Brotto keeps lands on your disk.
</p>

<!-- The whole install as one path. Two doors in at step 01, one outcome at
     step 04; the container carries the heavier rule because it is the object
     that lands on the reader's disk. -->
<figure>
  <img src="/assets/diagrams/install-path.svg" width="900" height="340" loading="lazy"
    alt="The install path in four steps. Step one is the server: an AI prompt or four commands, with Docker the only ask. Step two is a container on your machine at 127.0.0.1:8000 holding the agent loop. Step three is the Chrome extension, with two settings. Step four is a running task in the tab you are already signed in to.">
  <figcaption>Two doors in, one path out. The AI prompt and the four commands do the same job.</figcaption>
</figure>

<h2>Let your AI do it</h2>

<p>
  You do not have to read a terminal tutorial to run Brotto. If you use an AI
  coding tool (Cursor, Claude Code, Copilot, Windsurf — whatever you already
  have), paste the block below into it. The tool does the work; you paste two
  things into the extension yourself, at the end.
</p>

<p class="section-note">
  This sets up the <em>server</em> only. The extension is the next step and
  needs no agent — it installs from the Chrome Web Store in one click.
</p>

<pre><code>Set up Brotto's server on this machine. Brotto is an AI browser agent: a
Chrome extension talks to a small local server that runs the agent loop.

Prerequisite: Docker.

1. Clone https://github.com/suryanshgupta9933/Brotto and work in that
   directory.

2. Copy .env.example to .env. Generate a long random AGENT_SECRET — a
   password generator, or `openssl rand -hex 32`, is fine. Do not reuse a
   password I use anywhere else. Never commit the .env file.

3. Start the server: docker compose up -d

4. Confirm it answers: curl -s http://127.0.0.1:8000/health

5. Stop there. Tell me the server address (http://127.0.0.1:8000) and that
   AGENT_SECRET is what I will paste into the extension's Settings →
   Connection.

Do not paste a model API key into any file. I will add that myself in the
extension's Settings — it belongs there, not in .env.</code></pre>

<p>
  Shorter version, if you would rather type a sentence than paste a block:
</p>

<pre><code>Set up Brotto's local server from
https://github.com/suryanshgupta9933/Brotto — generate a long random
AGENT_SECRET in .env, start it with Docker, and confirm the health check
answers. Don't touch any model API key; I'll add that in the extension
myself.</code></pre>

<h2>Do it by hand</h2>

<p>
  Same four commands. Docker is the only thing you need installed first.
</p>

<pre><code>git clone https://github.com/suryanshgupta9933/Brotto.git
cd Brotto

cp .env.example .env      # set AGENT_SECRET to any long random string
docker compose up -d</code></pre>

<p>
  That is the whole server. It listens on <code>http://127.0.0.1:8000</code>
  with no browser in it — about 510&nbsp;MB, most of which is the model
  provider SDKs rather than Chromium. Check it with:
</p>

<pre><code>curl -s http://127.0.0.1:8000/health</code></pre>

<p>
  If that answers, the server is up and the rest is the extension.
</p>

<h2>The extension</h2>

<p>
  Two ways. The store install is the default path; building from source is
  there for people who want it.
</p>

<h3>Chrome Web Store — the easy path</h3>

<p>
  <a href="https://chromewebstore.google.com/detail/brotto/mahkomofcmohephggjlfgocopgfhkggb"
    >Add Brotto to Chrome</a
  >. Open the side panel and fill in two Settings screens:
</p>

<!-- The two settings as they sit in the panel, rebuilt in markup. A bullet
     list named the same two fields and read as a checklist; as cards they
     read as the two places to paste something. -->
<div class="cardgrid cardgrid--2">
  <div>
    <span class="card-idx label">Settings · Connection</span>
    <h3>Server address</h3>
    <p>
      <code>http://127.0.0.1:8000</code>, and paste the
      <code>AGENT_SECRET</code> you generated.
    </p>
  </div>
  <div>
    <span class="card-idx label">Settings · Model</span>
    <h3>Your model key</h3>
    <p>
      Your key, any of
      <a href="/#how">the providers Brotto supports</a>. Held in memory for
      the run and never written to disk. It goes here, in the extension — not
      in <code>.env</code>, and not in any file on the server.
    </p>
  </div>
</div>

<h3>Build it yourself — the other path</h3>

<pre><code>cd clients/brotto-extension
npm ci &amp;&amp; npm run build</code></pre>

<p>
  Then open <code>chrome://extensions</code>, turn on <b>Developer mode</b>,
  and <b>Load unpacked</b> → <code>clients/brotto-extension/dist</code>. Same
  settings as above.
</p>

<div class="split">
  <div class="claim">
    <span class="eyebrow label">What you have</span>
    <h2>Free, permanent, and yours</h2>
    <p>
      A browser agent that runs where you are already signed in, with no
      account and no operator on the other end. Free, permanent, Apache 2.0 —
      read it, fork it, ship it.
    </p>
  </div>
  <div>
    <div class="cardgrid cardgrid--2">
      <div>
        <h3>The same three gates</h3>
        <p>
          The gates that cannot be switched off are the same ones the cloud
          beta has, and the audit record of every run is a file on your disk.
        </p>
      </div>
      <div>
        <h3>Still to come</h3>
        <p>
          A one-command installer is planned, not built. Until it is, these
          are the steps. If you would rather skip them entirely,
          <a href="/get">Brotto Cloud</a> is the other door — same extension,
          someone else's server, invite-only while it is in beta.
        </p>
      </div>
    </div>
  </div>
</div>

<p class="section-note">
  <a href="/get">Get Brotto</a> ·
  <a href="/privacy">Privacy</a> ·
  <a href="/security">Security</a> ·
  <a href="/">Back to the front page</a>
</p>
