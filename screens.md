---
layout: default
title: Screens
wide: true
description: Every screen in the Brotto panel, and one real run from the first sentence to the branch protection ruleset it wrote.
---

# Screens

<p class="section-note" style="margin-top: -6px;">
  Everything below is the real extension in a real browser. Nothing is mocked,
  staged or cropped to hide a step. The three panels are the surfaces you
  interact with; the run afterwards is what one of them looks like with a task
  in flight.
</p>

<h2>The panel</h2>

<div class="shots">
  <figure>
    <img src="/assets/img/panel-idle.webp" alt="The Brotto panel idle, with suggestions" loading="lazy">
    <figcaption><b>Idle.</b> The panel offers what the page in front of you could be asked to do.</figcaption>
  </figure>
  <figure>
    <img src="/assets/img/panel-session-history.webp" alt="The session history list" loading="lazy">
    <figcaption><b>History.</b> Every run, on your own disk, yours to delete.</figcaption>
  </figure>
  <figure>
    <img src="/assets/img/panel-settings.webp" alt="Brotto's settings: bring your own model key, and the sites it refuses" loading="lazy">
    <figcaption><b>Yours.</b> Your model key, your server, and the list of sites Brotto refuses outright.</figcaption>
  </figure>
</div>

<h2>One run, start to finish</h2>

<p class="section-note">
  One task, four moments: Brotto adding a branch protection ruleset to its own
  public repository. Note where it stops — not once at the end, twice mid-run,
  because both were decisions only you could make.
</p>

<div class="moment">
  <div class="n label">01</div>
  <div>
    <h3>You ask for it in a sentence</h3>
    <p>
      There is no form and no workflow to learn. The panel is a chat box, and
      whatever you can describe is the whole interface.
    </p>
    <img src="/assets/img/run-1-the-prompt.webp" alt="Brotto's panel with the task typed out: go to GitHub, find the Brotto repository, add a branch protection ruleset to main, and open a pull request for it" loading="lazy">
  </div>
</div>

<div class="moment">
  <div class="n label">02</div>
  <div>
    <h3>It asks before it leaves</h3>
    <p>
      GitHub is the first domain this run touches, so it stops and waits. A
      domain you approve is remembered for good — consent is for the site, not
      for the one verb — and a page Brotto has never seen cannot be pre-approved
      by anything but you.
    </p>
    <img src="/assets/img/run-2-before-it-navigates.webp" alt="Brotto's panel showing a first-navigation approval card for github.com, with Allow and Deny buttons" loading="lazy">
  </div>
</div>

<div class="moment">
  <div class="n label">03</div>
  <div>
    <h3>It stops again when the page offers a choice</h3>
    <p>
      GitHub has two ways to add branch protection, and picking wrong means
      clicking back through settings. Rather than guess, it hands you the
      question and waits. This is the same card you would get for a sign-in it
      cannot pass.
    </p>
    <img src="/assets/img/run-3-it-asks-when-unsure.webp" alt="Brotto's panel stopping to clarify that the repository has two ways to add branch protection, with Skip and Say options" loading="lazy">
  </div>
</div>

<div class="moment">
  <div class="n label">04</div>
  <div>
    <h3>The run finishes, and the whole thing is on your disk</h3>
    <p>
      The panel reports what it did and what it would do next. Nothing is sent
      here: the ruleset was written on github.com by your own session, and the
      transcript lands in <code>logs/sessions/</code> beside the rest of your
      files.
    </p>
    <img src="/assets/img/run-4-the-ruleset-it-wrote.webp" alt="Brotto reporting DONE: it created a classic branch protection ruleset on the main branch of the Brotto repository, with targets, enforcement status, required checks and force-push settings" loading="lazy">
  </div>
</div>

<h2>Twenty-five seconds</h2>

<div class="split" style="border-top: 0; padding-top: 8px;">
  <div class="claim">
    <span class="eyebrow label">The video</span>
    <h2>What it looks like in motion</h2>
    <p>
      A pass through the product: the panel opening, a task being read, an
      approval coming back, a run finishing. It is a showcase of the shapes you
      will see, not a recording of one session — the session above is the real
      one, moment for moment.
    </p>
  </div>
  <div class="hero-panel">
    <figure class="demo">
      <video controls playsinline preload="metadata" poster="/assets/poster.jpg">
        <source src="/assets/brag.mp4" type="video/mp4">
        Your browser cannot play this video. <a href="/assets/brag.mp4">Download it instead.</a>
      </video>
    </figure>
  </div>
</div>

<p class="section-note" style="margin-top: 34px;">
  <a href="/#try">Install it yourself</a> — one container and one extension,
  about six steps. Or read
  <a href="https://github.com/suryanshgupta9933/Brotto#screens">the README</a>
  for the same thing with the commands inline.
</p>