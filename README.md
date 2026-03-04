# test
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FLOW — Executive Presentation</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:ital,wght@0,300;0,400;0,500;0,600;0,700;1,300;1,400&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
/* ── RESET & BASE ─────────────────────────────────────── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
  --ink:     #09131D;
  --ink2:    #0e1e2e;
  --ink3:    #162840;
  --ink4:    #1e3450;
  --teal:    #00C2CB;
  --teal-dk: #007E85;
  --gold:    #F5A623;
  --mint:    #25D07E;
  --coral:   #F0654E;
  --purp:    #9B72F5;
  --sky:     #38B2F5;
  --slate:   #6B8FAB;
  --pale:    #cce4f5;
  --white:   #ffffff;
}

html, body {
  width: 100%; height: 100%;
  background: #000;
  overflow: hidden;
  font-family: 'DM Sans', sans-serif;
  color: var(--white);
  cursor: none;
}

/* ── CUSTOM CURSOR ───────────────────────────────────── */
.cursor {
  position: fixed;
  width: 12px; height: 12px;
  background: var(--teal);
  border-radius: 50%;
  pointer-events: none;
  z-index: 9999;
  transform: translate(-50%,-50%);
  transition: width .15s, height .15s, opacity .15s;
  mix-blend-mode: screen;
}
.cursor.big { width: 40px; height: 40px; opacity: .4; }

/* ── DECK CONTAINER ──────────────────────────────────── */
#deck {
  position: fixed;
  inset: 0;
  width: 100vw; height: 100vh;
}

/* ── SLIDES ──────────────────────────────────────────── */
.slide {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  opacity: 0;
  pointer-events: none;
  transition: opacity .06s;
}
.slide.active {
  opacity: 1;
  pointer-events: all;
}

/* Clip animation — wipe from left */
.slide.entering  { animation: slideIn .6s cubic-bezier(.77,0,.18,1) forwards; }
.slide.exiting   { animation: slideOut .5s cubic-bezier(.77,0,.18,1) forwards; }

@keyframes slideIn {
  from { clip-path: inset(0 100% 0 0); opacity:1; }
  to   { clip-path: inset(0 0% 0 0);   opacity:1; }
}
@keyframes slideOut {
  from { clip-path: inset(0 0% 0 0);   opacity:1; }
  to   { clip-path: inset(0 0 0 100%); opacity:0; }
}

/* ── TOP ACCENT BAR ──────────────────────────────────── */
.accent-bar {
  height: 5px;
  flex-shrink: 0;
}

/* ── CONTENT AREA ────────────────────────────────────── */
.slide-body {
  flex: 1;
  padding: clamp(28px, 4vw, 56px) clamp(32px, 6vw, 80px);
  display: flex;
  flex-direction: column;
  position: relative;
  overflow: hidden;
}

/* ── SLIDE NUMBER ────────────────────────────────────── */
.slide-num {
  position: absolute;
  top: 18px; right: 32px;
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  color: var(--slate);
  letter-spacing: .15em;
}

/* ── PILL LABEL ──────────────────────────────────────── */
.pill {
  display: inline-block;
  padding: 4px 14px;
  border-radius: 20px;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: .1em;
  text-transform: uppercase;
  margin-bottom: 18px;
  align-self: flex-start;
}

/* ── HEADLINES ───────────────────────────────────────── */
.eyebrow {
  font-size: clamp(16px, 2.2vw, 22px);
  font-weight: 300;
  color: var(--pale);
  line-height: 1.2;
  margin-bottom: 4px;
}
.headline {
  font-family: 'Bebas Neue', sans-serif;
  font-size: clamp(52px, 9vw, 110px);
  line-height: .92;
  letter-spacing: .01em;
  color: var(--white);
}
.subhead {
  font-size: clamp(13px, 1.6vw, 17px);
  font-weight: 400;
  font-style: italic;
  line-height: 1.55;
  color: var(--pale);
  max-width: 640px;
  margin-top: 18px;
}
.rule {
  width: clamp(100px, 30%, 360px);
  height: 3px;
  margin: 16px 0;
  border-radius: 2px;
}

/* ── STAT CARDS (Slide 1) ────────────────────────────── */
.stat-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  margin-top: auto;
}
.stat-card {
  border-radius: 10px;
  padding: 28px 24px 22px;
  border: 1.5px solid;
  position: relative;
  overflow: hidden;
}
.stat-card::before {
  content: '';
  position: absolute;
  inset: 0;
  opacity: .12;
}
.stat-number {
  font-family: 'Bebas Neue', sans-serif;
  font-size: clamp(52px, 7vw, 80px);
  line-height: 1;
  margin-bottom: 8px;
}
.stat-label {
  font-size: clamp(11px, 1.3vw, 14px);
  color: var(--pale);
  line-height: 1.45;
}
.tagline {
  margin-top: 12px;
  font-size: clamp(11px, 1.2vw, 13px);
  font-style: italic;
  text-align: center;
}

/* ── TWO TEAMS (Slide 2) ─────────────────────────────── */
.teams-grid {
  display: grid;
  grid-template-columns: 1fr 60px 1fr;
  gap: 0;
  flex: 1;
  margin-top: 16px;
  min-height: 0;
}
.team-card {
  border-radius: 10px;
  border: 1.5px solid;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}
.team-header {
  padding: 10px 18px;
  font-size: 13px;
  font-weight: 700;
}
.team-rows {
  flex: 1;
  padding: 14px 18px;
  display: flex;
  flex-direction: column;
  gap: 0;
}
.team-row { padding: 10px 0; border-bottom: 1px solid rgba(255,255,255,.06); }
.team-row:last-child { border-bottom: none; }
.team-row-head {
  font-size: clamp(11px, 1.3vw, 13px);
  font-weight: 700;
  margin-bottom: 3px;
  display: flex; align-items: center; gap: 8px;
}
.team-row-head::before { content: '●'; font-size: 8px; }
.team-row-body {
  font-size: clamp(10px, 1.2vw, 12px);
  color: var(--pale);
  font-style: italic;
  padding-left: 16px;
  line-height: 1.4;
}
.team-verdict {
  padding: 10px 18px;
  font-size: 12px;
  font-weight: 700;
  font-style: italic;
  border-top: 1px solid rgba(255,255,255,.1);
}
.vs-col {
  display: flex;
  align-items: center;
  justify-content: center;
}
.vs-badge {
  width: 46px; height: 46px;
  border-radius: 50%;
  background: var(--ink3);
  border: 1px solid var(--ink4);
  display: flex; align-items: center; justify-content: center;
  font-size: 13px;
  font-weight: 700;
  color: var(--slate);
}

/* ── OBJECTIONS (Slide 3) ────────────────────────────── */
.obj-list {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 14px;
  margin-top: 8px;
}
.obj-card {
  border-radius: 10px;
  border: 1.5px solid;
  display: grid;
  grid-template-columns: 1fr 3px 1fr;
  overflow: hidden;
  flex: 1;
}
.obj-left { padding: 14px 20px; }
.obj-divider { }
.obj-right { padding: 14px 20px; }
.obj-tag {
  display: inline-block;
  padding: 3px 12px;
  border-radius: 20px;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: .1em;
  text-transform: uppercase;
  margin-bottom: 8px;
}
.obj-q {
  font-size: clamp(12px, 1.4vw, 15px);
  font-weight: 700;
  margin-bottom: 6px;
}
.obj-a {
  font-size: clamp(10px, 1.2vw, 13px);
  color: var(--pale);
  line-height: 1.5;
}
.obj-proof-label {
  font-size: 9px;
  font-weight: 700;
  letter-spacing: .1em;
  text-transform: uppercase;
  margin-bottom: 6px;
}
.obj-proof-text {
  font-size: clamp(10px, 1.2vw, 13px);
  font-style: italic;
  color: var(--pale);
  line-height: 1.5;
}

/* ── PHASES (Slide 4) ────────────────────────────────── */
.phase-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 14px;
  flex: 1;
  margin-top: 14px;
  min-height: 0;
}
.phase-card {
  border-radius: 10px;
  border: 1.5px solid;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  position: relative;
}
.phase-top {
  padding: 16px 16px 10px;
  text-align: center;
}
.phase-num-circle {
  width: 44px; height: 44px;
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-family: 'Bebas Neue', sans-serif;
  font-size: 26px;
  margin: 0 auto 8px;
}
.phase-title {
  font-size: 14px;
  font-weight: 700;
  margin-bottom: 2px;
}
.phase-month {
  font-size: 11px;
  color: var(--slate);
  font-style: italic;
}
.phase-risk {
  margin: 8px 12px;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: .06em;
  text-align: center;
  text-transform: uppercase;
}
.phase-bullets {
  flex: 1;
  padding: 4px 16px 12px;
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 6px;
}
.phase-bullets li {
  font-size: clamp(10px, 1.1vw, 12px);
  color: var(--pale);
  padding-left: 14px;
  position: relative;
  line-height: 1.35;
}
.phase-bullets li::before {
  content: '●';
  position: absolute;
  left: 0;
  font-size: 6px;
  top: 4px;
}
.phase-punchline {
  padding: 8px 12px;
  border-top: 1px solid rgba(255,255,255,.08);
  font-size: 10px;
  font-style: italic;
  line-height: 1.35;
  text-align: center;
}
.phase-connector {
  display: none; /* handled via grid gap */
}
.slide4-footer {
  margin-top: 10px;
  font-size: clamp(10px, 1.3vw, 13px);
  font-weight: 700;
  text-align: center;
  font-style: italic;
}

/* ── THE ASK (Slide 5) ───────────────────────────────── */
.ask-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  flex: 1;
  margin-top: 14px;
  min-height: 0;
}
.ask-card {
  border-radius: 10px;
  border: 2px solid;
  display: flex;
  flex-direction: column;
  padding: 26px 24px 20px;
  position: relative;
  overflow: hidden;
}
.ask-card::after {
  content: '';
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background: linear-gradient(135deg, currentColor 0%, transparent 60%);
  opacity: .06;
  pointer-events: none;
}
.ask-num {
  font-family: 'Bebas Neue', sans-serif;
  font-size: clamp(42px, 6vw, 64px);
  line-height: 1;
  margin-bottom: 10px;
}
.ask-rule { height: 3px; width: 48px; border-radius: 2px; margin-bottom: 14px; }
.ask-title {
  font-size: clamp(14px, 1.6vw, 18px);
  font-weight: 700;
  margin-bottom: 12px;
  line-height: 1.2;
}
.ask-detail {
  font-size: clamp(11px, 1.2vw, 13px);
  color: var(--pale);
  line-height: 1.6;
  flex: 1;
}
.ask-impact {
  margin-top: 16px;
  padding: 8px 12px;
  border-radius: 6px;
  font-size: clamp(10px, 1.1vw, 12px);
  font-weight: 700;
  font-style: italic;
  line-height: 1.3;
}

/* ── DECORATIVE BLOBS ────────────────────────────────── */
.blob {
  position: absolute;
  border-radius: 50%;
  pointer-events: none;
  filter: blur(1px);
}

/* ── PROGRESS BAR ────────────────────────────────────── */
#progress {
  position: fixed;
  bottom: 0; left: 0;
  height: 3px;
  background: var(--teal);
  transition: width .4s cubic-bezier(.4,0,.2,1);
  z-index: 100;
}

/* ── SLIDE COUNTER ───────────────────────────────────── */
#counter {
  position: fixed;
  bottom: 14px; right: 24px;
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  color: var(--slate);
  letter-spacing: .15em;
  z-index: 100;
}

/* ── NAV ARROWS ──────────────────────────────────────── */
.nav-hint {
  position: fixed;
  bottom: 14px; left: 24px;
  font-size: 11px;
  color: var(--slate);
  z-index: 100;
  letter-spacing: .05em;
  display: flex;
  align-items: center;
  gap: 6px;
}
.nav-hint kbd {
  background: var(--ink3);
  border: 1px solid var(--ink4);
  border-radius: 4px;
  padding: 1px 6px;
  font-family: 'DM Mono', monospace;
  font-size: 10px;
  color: var(--pale);
}

/* ── SPEAKER NOTES PANEL ─────────────────────────────── */
#notes-panel {
  position: fixed;
  bottom: -100%;
  left: 0; right: 0;
  height: 35vh;
  background: rgba(9,19,29,.97);
  border-top: 2px solid var(--teal);
  padding: 20px 40px;
  z-index: 200;
  transition: bottom .4s cubic-bezier(.4,0,.2,1);
  overflow-y: auto;
  backdrop-filter: blur(12px);
}
#notes-panel.open { bottom: 0; }
#notes-panel h3 {
  font-size: 11px;
  font-weight: 700;
  letter-spacing: .12em;
  text-transform: uppercase;
  color: var(--teal);
  margin-bottom: 12px;
}
#notes-content {
  font-size: 13px;
  line-height: 1.7;
  color: var(--pale);
  white-space: pre-line;
}
#notes-close {
  position: absolute;
  top: 16px; right: 24px;
  background: none;
  border: 1px solid var(--ink4);
  color: var(--slate);
  cursor: pointer;
  padding: 4px 12px;
  border-radius: 4px;
  font-size: 11px;
  font-family: 'DM Mono', monospace;
}
#notes-close:hover { color: var(--white); border-color: var(--teal); }

/* ── NOTES TOGGLE BUTTON ─────────────────────────────── */
#notes-btn {
  position: fixed;
  bottom: 10px; left: 50%; transform: translateX(-50%);
  background: var(--ink3);
  border: 1px solid var(--ink4);
  color: var(--slate);
  cursor: pointer;
  padding: 5px 16px;
  border-radius: 20px;
  font-size: 10px;
  font-family: 'DM Mono', monospace;
  letter-spacing: .08em;
  z-index: 100;
  transition: color .2s, border-color .2s;
}
#notes-btn:hover { color: var(--white); border-color: var(--teal); }

/* ── ANIMATIONS ──────────────────────────────────────── */
@keyframes fadeUp {
  from { opacity:0; transform: translateY(24px); }
  to   { opacity:1; transform: translateY(0); }
}
.slide.active .animate {
  animation: fadeUp .55s cubic-bezier(.4,0,.2,1) both;
}
.slide.active .animate-1 { animation-delay: .1s; }
.slide.active .animate-2 { animation-delay: .22s; }
.slide.active .animate-3 { animation-delay: .34s; }
.slide.active .animate-4 { animation-delay: .44s; }
.slide.active .animate-5 { animation-delay: .52s; }

/* ── SLIDE-SPECIFIC BACKGROUNDS ──────────────────────── */
.s1-bg { background: var(--ink); }
.s2-bg { background: var(--ink2); }
.s3-bg { background: var(--ink); }
.s4-bg { background: var(--ink2); }
.s5-bg { background: var(--ink); }

</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div id="progress"></div>
<div id="counter">1 / 5</div>
<div class="nav-hint">
  <kbd>←</kbd><kbd>→</kbd> navigate &nbsp;·&nbsp; <kbd>N</kbd> speaker notes &nbsp;·&nbsp; <kbd>F</kbd> fullscreen
</div>
<button id="notes-btn">SPEAKER NOTES</button>

<div id="notes-panel">
  <button id="notes-close">CLOSE ✕</button>
  <h3>Speaker Notes — Slide <span id="notes-slide-num">1</span></h3>
  <div id="notes-content"></div>
</div>

<div id="deck">

<!-- ══════════════════════════════════════════════════════
     SLIDE 1 — THE BURNING PLATFORM
══════════════════════════════════════════════════════ -->
<div class="slide s1-bg active" id="slide-1"
     data-notes="Open with conviction — not an apology.\n\nSay: 'I'm not here to ask you to abandon what we've built. I'm here to show you that what we proved — building code directly from requirements with AI — is not a one-off. It's a system. And this is what that system looks like.'\n\nPause on the three numbers. Let each one land before moving on. The 20–30% should make every exec wince — that's meetings they've sat in. The 'Days' is money left on the table. The 3× is a structural waste problem, not a people problem.\n\nClose the slide by saying: 'The question is not whether we need to change. It is whether we lead the change or react to it.'">

  <!-- Decorative blobs -->
  <div class="blob" style="width:600px;height:600px;background:radial-gradient(circle,rgba(0,194,203,.12) 0%,transparent 70%);top:-160px;right:-100px;"></div>
  <div class="blob" style="width:400px;height:400px;background:radial-gradient(circle,rgba(0,126,133,.08) 0%,transparent 70%);bottom:-100px;left:-80px;"></div>

  <div class="accent-bar" style="background:var(--teal);"></div>
  <div class="slide-body">
    <div class="slide-num">01 / 06</div>

    <div class="pill animate animate-1" style="background:rgba(0,194,203,.15);border:1px solid var(--teal);color:var(--teal);">The Situation</div>

    <div class="animate animate-2">
      <div class="eyebrow">While we were perfecting Scrum,</div>
      <div class="headline">the rules<br>changed.</div>
    </div>

    <div class="rule animate animate-3" style="background:var(--teal);"></div>

    <div class="subhead animate animate-3">Our team already proved it: we connected AI to GitHub, Jira and Confluence and built production code directly from requirements. That wasn't a demo — that was a glimpse of a structurally faster way to work.</div>

    <div class="stat-grid animate animate-4">
      <div class="stat-card" style="border-color:var(--coral);background:rgba(240,101,78,.07);">
        <div class="stat-number" style="color:var(--coral);">20–30%</div>
        <div class="stat-label">of every sprint consumed by ceremonies.<br>Zero code shipped.</div>
      </div>
      <div class="stat-card" style="border-color:var(--gold);background:rgba(245,166,35,.07);">
        <div class="stat-number" style="color:var(--gold);">Days</div>
        <div class="stat-label">lost at sprint boundaries for work that is already done and ready to ship.</div>
      </div>
      <div class="stat-card" style="border-color:var(--purp);background:rgba(155,114,245,.07);">
        <div class="stat-number" style="color:var(--purp);">3×</div>
        <div class="stat-label">the handoffs between requirements, development and QA phases.</div>
      </div>
    </div>

    <div class="tagline animate animate-5" style="color:var(--teal);">
      The question is not whether to adapt. It is whether we lead or catch up.
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════════════════
     SLIDE 2 — TWO TEAMS (ROI)
══════════════════════════════════════════════════════ -->
<div class="slide s2-bg" id="slide-2"
     data-notes="This is your ROI slide — but delivered as a story, not a spreadsheet.\n\nSay: 'I want you to imagine two teams starting today. Same people, same backlog, same pressures. One team keeps Scrum and adds AI as a better autocomplete. The other restructures how work actually flows. In 12 months, Team B ships in days what Team A ships in sprints. That gap compounds. It does not close.'\n\nKeep it hypothetical — don't use your own team names yet. It feels safer, and the implication is obvious to every exec in the room.\n\nIf someone asks 'how do you know the 40–60%?' say: 'That is the cycle time drop we see when sprint boundary gates are removed from work that is already done. We measure it from Month 1. You'll have the data.'">

  <div class="blob" style="width:500px;height:500px;background:radial-gradient(circle,rgba(245,166,35,.08) 0%,transparent 70%);top:-100px;right:-80px;"></div>

  <div class="accent-bar" style="background:var(--gold);"></div>
  <div class="slide-body">
    <div class="slide-num">02 / 06</div>

    <div class="pill animate animate-1" style="background:rgba(245,166,35,.15);border:1px solid var(--gold);color:var(--gold);">The ROI</div>

    <div class="animate animate-2" style="margin-bottom:6px;">
      <div class="headline" style="font-size:clamp(36px,5.5vw,68px);line-height:1.05;">Imagine two teams.<br><span style="color:var(--gold);">Same size. Same problem. Different choice.</span></div>
    </div>

    <div class="teams-grid animate animate-3">
      <div class="team-card" style="border-color:var(--coral);background:rgba(240,101,78,.06);">
        <div class="team-header" style="background:rgba(240,101,78,.15);color:var(--coral);">Team A — Stays with Scrum</div>
        <div class="team-rows">
          <div class="team-row">
            <div class="team-row-head" style="color:var(--coral);">Sprint boundaries still gate releases</div>
            <div class="team-row-body">Features ready Tuesday wait until Friday. Customers wait.</div>
          </div>
          <div class="team-row">
            <div class="team-row-head" style="color:var(--coral);">Estimation consumes planning time</div>
            <div class="team-row-body">Hours arguing points instead of building value.</div>
          </div>
          <div class="team-row">
            <div class="team-row-head" style="color:var(--coral);">AI used as autocomplete only</div>
            <div class="team-row-body">15–20% velocity gain — better than nothing, far below potential.</div>
          </div>
          <div class="team-row">
            <div class="team-row-head" style="color:var(--coral);">Context lives in people's heads</div>
            <div class="team-row-body">When a developer leaves, the AI context goes with them.</div>
          </div>
        </div>
        <div class="team-verdict" style="color:var(--coral);background:rgba(240,101,78,.1);">In 12 months: incremental improvement.</div>
      </div>

      <div class="vs-col">
        <div class="vs-badge">VS</div>
      </div>

      <div class="team-card" style="border-color:var(--mint);background:rgba(37,208,126,.05);">
        <div class="team-header" style="background:rgba(37,208,126,.14);color:var(--mint);">Team B — Adopts FLOW</div>
        <div class="team-rows">
          <div class="team-row">
            <div class="team-row-head" style="color:var(--mint);">Continuous delivery — no sprint gate</div>
            <div class="team-row-body">Features ship when done. Cycle time drops 40–60%.</div>
          </div>
          <div class="team-row">
            <div class="team-row-head" style="color:var(--mint);">AI generates first drafts at every stage</div>
            <div class="team-row-body">Plans, code, tests, PR reviews — humans judge, not write.</div>
          </div>
          <div class="team-row">
            <div class="team-row-head" style="color:var(--mint);">Context lives in Confluence + tools</div>
            <div class="team-row-body">Every new developer onboards in hours, not weeks.</div>
          </div>
          <div class="team-row">
            <div class="team-row-head" style="color:var(--mint);">Quality is structural, not a phase</div>
            <div class="team-row-body">Gates catch issues before merge. Rework rate falls measurably.</div>
          </div>
        </div>
        <div class="team-verdict" style="color:var(--mint);background:rgba(37,208,126,.1);">In 12 months: structurally faster delivery.</div>
      </div>
    </div>

    <div class="tagline animate animate-4" style="color:var(--gold);margin-top:10px;">
      This is the fork in the road we are standing at right now.
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════════════════
     SLIDE 3 — "BUT WHAT ABOUT...?"
══════════════════════════════════════════════════════ -->
<div class="slide s3-bg" id="slide-3"
     data-notes="This is your credibility slide. Read the room before showing it.\n\nFor change fatigue: 'Month 1 changes nothing that touches delivery. We remove estimation sessions — that's all. The team experiences less overhead from Day 1. This is a reduction in change, not an addition to it.'\n\nFor AI risk: be specific and sharp. Say 'No generated code merges unless a named developer can explain every single block. That is not a guideline — it is a gate with a named owner and an SLA. The AI generates. Humans decide.' Watch the room relax.\n\nFor ROI: 'We will baseline current cycle time in Month 1. You will have before-and-after data in your hands by Month 3. We are not asking you to trust us. We are asking you to measure us.'\n\nIf someone says 'we just finished implementing Scrum': 'FLOW keeps the rhythm Scrum taught us — weekly direction, continuous learning. We remove the overhead. The discipline stays. The ceremony waste goes.'">

  <div class="blob" style="width:450px;height:450px;background:radial-gradient(circle,rgba(155,114,245,.1) 0%,transparent 70%);top:-80px;right:-60px;"></div>

  <div class="accent-bar" style="background:var(--purp);"></div>
  <div class="slide-body">
    <div class="slide-num">03 / 06</div>

    <div class="pill animate animate-1" style="background:rgba(155,114,245,.15);border:1px solid var(--purp);color:var(--purp);">Objection Handling</div>

    <div class="headline animate animate-2" style="font-size:clamp(42px,6vw,78px);margin-bottom:4px;">"But what about...?"</div>
    <div style="font-size:clamp(12px,1.4vw,15px);font-style:italic;color:var(--purp);margin-bottom:14px;" class="animate animate-2">We heard every concern. We designed FLOW around them.</div>

    <div class="obj-list animate animate-3">

      <div class="obj-card" style="border-color:var(--gold);background:rgba(245,166,35,.05);">
        <div class="obj-left">
          <div class="obj-tag" style="background:rgba(245,166,35,.2);color:var(--gold);">Change Fatigue</div>
          <div class="obj-q" style="color:var(--gold);">"Won't this disrupt the team?"</div>
          <div class="obj-a">Month 1 changes nothing that touches delivery. We remove estimation and add one template. That's it. The team experiences less overhead immediately — not more change.</div>
        </div>
        <div class="obj-divider" style="background:var(--gold);opacity:.3;"></div>
        <div class="obj-right">
          <div class="obj-proof-label" style="color:var(--gold);">How we enforce it</div>
          <div class="obj-proof-text">Phase 1 is structural only. No ceremony changes. Teams report it as relief, not disruption. You can stop after Month 1 and still be ahead.</div>
        </div>
      </div>

      <div class="obj-card" style="border-color:var(--coral);background:rgba(240,101,78,.05);">
        <div class="obj-left">
          <div class="obj-tag" style="background:rgba(240,101,78,.2);color:var(--coral);">AI Quality Risk</div>
          <div class="obj-q" style="color:var(--coral);">"How do we know AI won't ship bad code?"</div>
          <div class="obj-a">It cannot. Four named humans own every gate. Nothing merges unless a developer can explain every block. Nothing ships without structured pre-production validation. AI generates — humans decide.</div>
        </div>
        <div class="obj-divider" style="background:var(--coral);opacity:.3;"></div>
        <div class="obj-right">
          <div class="obj-proof-label" style="color:var(--coral);">How we enforce it</div>
          <div class="obj-proof-text">The 'Understand-It Rule': if you cannot explain the code, it does not merge. Ownership is named at creation, not assumed after the fact.</div>
        </div>
      </div>

      <div class="obj-card" style="border-color:var(--mint);background:rgba(37,208,126,.04);">
        <div class="obj-left">
          <div class="obj-tag" style="background:rgba(37,208,126,.2);color:var(--mint);">ROI</div>
          <div class="obj-q" style="color:var(--mint);">"What's the actual return?"</div>
          <div class="obj-a">Cycle time drops 40–60% when sprint boundaries are removed. Code review time drops when AI pre-checks against standards. Rework falls when quality is structural. Measurable from Month 2.</div>
        </div>
        <div class="obj-divider" style="background:var(--mint);opacity:.3;"></div>
        <div class="obj-right">
          <div class="obj-proof-label" style="color:var(--mint);">How we enforce it</div>
          <div class="obj-proof-text">We baseline cycle time in Month 1. You have before-and-after data by Month 3. We are not asking you to trust us. We are asking you to measure us.</div>
        </div>
      </div>

    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════════════════
     SLIDE 4 — THE TRANSITION: SAFE BY DESIGN
══════════════════════════════════════════════════════ -->
<div class="slide s4-bg" id="slide-4"
     data-notes="This is your risk-mitigation slide. Lead with the last line first.\n\nOpen by saying: 'I am not asking you to approve a 4-month transformation today. I am asking you to approve Month 1. It removes estimation sessions — that is all. It takes nothing away from delivery. And it gives us a before-state so we can measure every subsequent improvement.'\n\nFor change-fatigued execs: 'Month 1 is actually a reduction in change. We remove process, we do not add it.'\n\nIf they push back on Month 3: 'We do not commit to Month 3 until Month 2 data tells us we're ready. Every phase gate is evidence-based, not faith-based. You see the data before you approve the next step.'\n\nThe CHANGE POINT badge on Month 3 is there deliberately — acknowledge it honestly. Say: 'Month 3 is the real shift. Sprint boundaries come down. That is the structural change. We only do that when Month 2 data earns it.'">

  <div class="blob" style="width:500px;height:500px;background:radial-gradient(circle,rgba(0,194,203,.09) 0%,transparent 70%);bottom:-100px;right:-80px;"></div>

  <div class="accent-bar" style="background:var(--teal);"></div>
  <div class="slide-body">
    <div class="slide-num">04 / 06</div>

    <div class="pill animate animate-1" style="background:rgba(0,194,203,.15);border:1px solid var(--teal);color:var(--teal);">The Transition</div>

    <div class="headline animate animate-2" style="font-size:clamp(36px,5vw,62px);line-height:1.05;margin-bottom:4px;">We don't flip a switch.<br><span style="color:var(--teal);">We shift in four steps.</span></div>
    <div style="font-size:clamp(11px,1.3vw,14px);font-style:italic;color:var(--teal);margin-bottom:10px;" class="animate animate-2">Each phase is proven before the next begins. You can stop after Month 1 and still be ahead.</div>

    <div class="phase-grid animate animate-3">

      <div class="phase-card" style="border-color:var(--teal);background:rgba(0,194,203,.06);">
        <div class="phase-top">
          <div class="phase-num-circle" style="background:var(--teal);color:var(--ink);">1</div>
          <div class="phase-title" style="color:var(--teal);">Foundation</div>
          <div class="phase-month">Month 1</div>
        </div>
        <div class="phase-risk" style="background:rgba(37,208,126,.15);color:var(--mint);">Zero Delivery Risk</div>
        <ul class="phase-bullets">
          <li style="--c:var(--teal);">Remove story points + estimation</li>
          <li>Create the Intent Document template</li>
          <li>Simplify Jira to 3 issue types</li>
          <li>Baseline current cycle time</li>
        </ul>
        <div class="phase-punchline" style="color:var(--teal);border-top-color:rgba(0,194,203,.2);">Team saves 4–6 hrs per sprint from Day 1.</div>
      </div>

      <div class="phase-card" style="border-color:var(--gold);background:rgba(245,166,35,.06);">
        <div class="phase-top">
          <div class="phase-num-circle" style="background:var(--gold);color:var(--ink);">2</div>
          <div class="phase-title" style="color:var(--gold);">AI Integration</div>
          <div class="phase-month">Month 2</div>
        </div>
        <div class="phase-risk" style="background:rgba(245,166,35,.15);color:var(--gold);">Low Risk — sprints as rhythm</div>
        <ul class="phase-bullets">
          <li>AI decomposes intent docs into tasks</li>
          <li>Automated PR pre-review active</li>
          <li>Gate 2 plan reviews begin</li>
          <li>Claude confidence flag activates</li>
        </ul>
        <div class="phase-punchline" style="color:var(--gold);border-top-color:rgba(245,166,35,.2);">First AI-generated tasks reviewed by developers.</div>
      </div>

      <div class="phase-card" style="border-color:var(--purp);background:rgba(155,114,245,.06);">
        <div class="phase-top">
          <div class="phase-num-circle" style="background:var(--purp);color:var(--ink);">3</div>
          <div class="phase-title" style="color:var(--purp);">Full Flow</div>
          <div class="phase-month">Month 3</div>
        </div>
        <div class="phase-risk" style="background:rgba(240,101,78,.15);color:var(--coral);">Change Point — sprints removed</div>
        <ul class="phase-bullets">
          <li>Continuous delivery replaces sprint releases</li>
          <li>Async daily signals replace standup</li>
          <li>All 4 gates active with named owners</li>
          <li>Direction + Learning replace all ceremonies</li>
        </ul>
        <div class="phase-punchline" style="color:var(--purp);border-top-color:rgba(155,114,245,.2);">Cycle time data shows the before vs. after.</div>
      </div>

      <div class="phase-card" style="border-color:var(--sky);background:rgba(56,178,245,.05);">
        <div class="phase-top">
          <div class="phase-num-circle" style="background:var(--sky);color:var(--ink);">4</div>
          <div class="phase-title" style="color:var(--sky);">Optimise</div>
          <div class="phase-month">Month 4+</div>
        </div>
        <div class="phase-risk" style="background:rgba(56,178,245,.15);color:var(--sky);">Iterative — tune and scale</div>
        <ul class="phase-bullets">
          <li>Tune AI thresholds from real cycle time data</li>
          <li>Monthly exec dashboard goes live</li>
          <li>Scale FLOW to adjacent teams</li>
          <li>FLOW becomes the default, not the experiment</li>
        </ul>
        <div class="phase-punchline" style="color:var(--sky);border-top-color:rgba(56,178,245,.2);">Exec dashboard shows ROI. Decision: scale.</div>
      </div>

    </div>

    <div class="slide4-footer animate animate-4" style="color:var(--teal);">
      You approve Month 1 today. Not the whole transformation. Just the first safe step.
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════════════════
     SLIDE 5 — INDUSTRY VALIDATION
══════════════════════════════════════════════════════ -->
<div class="slide s2-bg" id="slide-5"
     data-notes="This slide is your external credibility moment. Use it to defuse the 'are we the only ones doing this?' concern.\n\nOpen with: 'We did not invent this from thin air. AWS, Bain, EPAM and Gartner are all pointing at the same destination independently. We have simply already built the hardest part — the connected toolchain — which most of the industry is still figuring out.'\n\nOn AWS AI-DLC: 'In August 2025 AWS launched a formal methodology that replaces sprints with short work cycles measured in hours or days. Wipro built four production modules in 20 hours using it. That is not a pilot — that is production delivery. Our FLOW bolts onto the same principle.'\n\nOn the METR trial finding (19% slower): 'This is the most important data point in the room. Teams using AI without structure actually got slower. That is the risk of doing nothing — or doing AI ad hoc. Structure is the differentiator. FLOW is that structure.'\n\nOn KodeNerds: 'A team delivered a full HIPAA-compliant healthcare platform with 30% of a traditional team size using intent-driven development — the same principle as our Intent Document. This is not theoretical.'\n\nClose with: 'Every major analyst and cloud provider is converging on FLOW's principles. The only question is whether we get there first or spend the next 18 months watching others do it.'">

  <div class="blob" style="width:550px;height:550px;background:radial-gradient(circle,rgba(56,178,245,.09) 0%,transparent 70%);top:-120px;right:-80px;"></div>
  <div class="blob" style="width:380px;height:380px;background:radial-gradient(circle,rgba(155,114,245,.07) 0%,transparent 70%);bottom:-80px;left:-60px;"></div>

  <div class="accent-bar" style="background:var(--sky);"></div>
  <div class="slide-body">
    <div class="slide-num">05 / 06</div>

    <div class="pill animate animate-1" style="background:rgba(56,178,245,.15);border:1px solid var(--sky);color:var(--sky);">Industry Validation</div>

    <div class="animate animate-2" style="margin-bottom:10px;">
      <div class="headline" style="font-size:clamp(34px,5vw,60px);line-height:1.0;">FLOW isn't ahead<br>of the industry —<br><span style="color:var(--sky);">it's where the industry<br>is landing.</span></div>
    </div>

    <!-- 4-column validation cards -->
    <div class="animate animate-3" style="display:grid;grid-template-columns:repeat(4,1fr);gap:12px;flex:1;margin-top:8px;min-height:0;">

      <!-- AWS -->
      <div style="border-radius:10px;border:1.5px solid var(--teal);background:rgba(0,194,203,.06);display:flex;flex-direction:column;overflow:hidden;">
        <div style="padding:12px 14px 8px;border-bottom:1px solid rgba(0,194,203,.15);">
          <div style="font-size:9px;font-weight:700;letter-spacing:.1em;color:var(--teal);text-transform:uppercase;margin-bottom:6px;">AWS · Aug 2025</div>
          <div style="font-size:clamp(12px,1.4vw,15px);font-weight:700;color:var(--white);line-height:1.2;">AI-Driven Development Lifecycle</div>
        </div>
        <div style="padding:10px 14px;flex:1;font-size:clamp(10px,1.1vw,12px);color:var(--pale);line-height:1.5;">
          AWS formally replaced sprints with short work cycles measured in hours or days. Used in production by Wipro, S&amp;P Global and HackerRank.
          <div style="margin-top:8px;padding:7px 10px;border-radius:6px;background:rgba(0,194,203,.12);color:var(--teal);font-size:10px;font-weight:700;font-style:italic;">Wipro: 4 production modules in 20 hours.</div>
        </div>
        <div style="padding:8px 14px;border-top:1px solid rgba(0,194,203,.12);">
          <div style="font-size:9px;color:var(--teal);font-weight:700;">FLOW PARALLEL</div>
          <div style="font-size:10px;color:var(--slate);font-style:italic;margin-top:2px;">Continuous delivery · no sprint gate</div>
        </div>
      </div>

      <!-- Bain / Industry -->
      <div style="border-radius:10px;border:1.5px solid var(--gold);background:rgba(245,166,35,.06);display:flex;flex-direction:column;overflow:hidden;">
        <div style="padding:12px 14px 8px;border-bottom:1px solid rgba(245,166,35,.15);">
          <div style="font-size:9px;font-weight:700;letter-spacing:.1em;color:var(--gold);text-transform:uppercase;margin-bottom:6px;">Bain · Tech Report 2025</div>
          <div style="font-size:clamp(12px,1.4vw,15px);font-weight:700;color:var(--white);line-height:1.2;">Restructured Workflows = Real Gains</div>
        </div>
        <div style="padding:10px 14px;flex:1;font-size:clamp(10px,1.1vw,12px);color:var(--pale);line-height:1.5;">
          Two thirds of software firms have rolled out gen AI — but gains evaporate without restructured workflows. Calls for dedicated "intent engineers" and "AI orchestrators."
          <div style="margin-top:8px;padding:7px 10px;border-radius:6px;background:rgba(245,166,35,.12);color:var(--gold);font-size:10px;font-weight:700;font-style:italic;">AI alone doesn't move the needle. Structure does.</div>
        </div>
        <div style="padding:8px 14px;border-top:1px solid rgba(245,166,35,.12);">
          <div style="font-size:9px;color:var(--gold);font-weight:700;">FLOW PARALLEL</div>
          <div style="font-size:10px;color:var(--slate);font-style:italic;margin-top:2px;">Context Curator + named human gates</div>
        </div>
      </div>

      <!-- EPAM / KodeNerds -->
      <div style="border-radius:10px;border:1.5px solid var(--mint);background:rgba(37,208,126,.05);display:flex;flex-direction:column;overflow:hidden;">
        <div style="padding:12px 14px 8px;border-bottom:1px solid rgba(37,208,126,.15);">
          <div style="font-size:9px;font-weight:700;letter-spacing:.1em;color:var(--mint);text-transform:uppercase;margin-bottom:6px;">EPAM · 2025 AI/SDLC</div>
          <div style="font-size:clamp(12px,1.4vw,15px);font-weight:700;color:var(--white);line-height:1.2;">Context Engineering &amp; Intent-Driven Dev</div>
        </div>
        <div style="padding:10px 14px;flex:1;font-size:clamp(10px,1.1vw,12px);color:var(--pale);line-height:1.5;">
          EPAM formally named "context engineering" — AI building on living documentation to answer questions like "How are retries handled in payments?" A HIPAA-compliant platform shipped at 30% of traditional team size using intent-driven development.
          <div style="margin-top:8px;padding:7px 10px;border-radius:6px;background:rgba(37,208,126,.12);color:var(--mint);font-size:10px;font-weight:700;font-style:italic;">Intent docs → 30% of team size needed.</div>
        </div>
        <div style="padding:8px 14px;border-top:1px solid rgba(37,208,126,.12);">
          <div style="font-size:9px;color:var(--mint);font-weight:700;">FLOW PARALLEL</div>
          <div style="font-size:10px;color:var(--slate);font-style:italic;margin-top:2px;">Intent Document + Confluence as context layer</div>
        </div>
      </div>

      <!-- METR Warning -->
      <div style="border-radius:10px;border:1.5px solid var(--coral);background:rgba(240,101,78,.06);display:flex;flex-direction:column;overflow:hidden;">
        <div style="padding:12px 14px 8px;border-bottom:1px solid rgba(240,101,78,.15);">
          <div style="font-size:9px;font-weight:700;letter-spacing:.1em;color:var(--coral);text-transform:uppercase;margin-bottom:6px;">METR RCT · 2025</div>
          <div style="font-size:clamp(12px,1.4vw,15px);font-weight:700;color:var(--white);line-height:1.2;">AI Without Structure = Slower Teams</div>
        </div>
        <div style="padding:10px 14px;flex:1;font-size:clamp(10px,1.1vw,12px);color:var(--pale);line-height:1.5;">
          Randomised controlled trial: experienced developers using AI tools with no workflow change took <strong style="color:var(--coral);">19% longer</strong> than without AI. The culprit: lack of structured workflow, not AI capability.
          <div style="margin-top:8px;padding:7px 10px;border-radius:6px;background:rgba(240,101,78,.14);color:var(--coral);font-size:10px;font-weight:700;font-style:italic;">This is the risk of doing nothing. FLOW is the fix.</div>
        </div>
        <div style="padding:8px 14px;border-top:1px solid rgba(240,101,78,.12);">
          <div style="font-size:9px;color:var(--coral);font-weight:700;">FLOW RESPONSE</div>
          <div style="font-size:10px;color:var(--slate);font-style:italic;margin-top:2px;">Structure before AI. Gates. Named owners. SLAs.</div>
        </div>
      </div>

    </div><!-- /grid -->

    <div class="animate animate-4" style="margin-top:10px;display:flex;align-items:center;gap:16px;">
      <div style="height:2px;flex:1;background:linear-gradient(90deg,var(--sky),transparent);border-radius:2px;"></div>
      <div style="font-size:clamp(10px,1.2vw,13px);font-style:italic;color:var(--sky);text-align:center;">
        AWS · Bain · EPAM · Gartner are all converging on FLOW's principles. We have already built what they are still designing.
      </div>
      <div style="height:2px;flex:1;background:linear-gradient(90deg,transparent,var(--sky));border-radius:2px;"></div>
    </div>

  </div>
</div>

<!-- ══════════════════════════════════════════════════════
     SLIDE 6 — THE ASK
══════════════════════════════════════════════════════ -->
<div class="slide s5-bg" id="slide-6"
     data-notes="This is the close. Keep your energy up — this is the moment.\n\nDon't end with 'any questions?' — end with a direct ask.\n\nSay: 'I want to make this as easy a yes as possible. We are not asking for transformation approval today. Three decisions. The first — Month 1 — starts this week if you say yes right now. The second costs nothing except a conversation with your Tech Lead. The third is 30 minutes a month.'\n\nIf someone hesitates: 'What would you need to see in Month 1 data to feel confident about Month 2? Tell me that now and we will track it specifically for you.'\n\nIf someone says they want to think about it: 'Of course. What specifically concerns you? Because if it's delivery risk, Month 1 has zero. If it's AI quality, we have four human gates. If it's ROI, we baseline in Month 1. Tell me what would close it for you today.'\n\nClose with: 'We already proved this works. FLOW is just the version of that proof that scales to the whole program.'">

  <div class="blob" style="width:600px;height:600px;background:radial-gradient(circle,rgba(0,126,133,.12) 0%,transparent 70%);top:-150px;right:-100px;"></div>
  <div class="blob" style="width:350px;height:350px;background:radial-gradient(circle,rgba(37,208,126,.07) 0%,transparent 70%);bottom:-80px;left:100px;"></div>

  <div class="accent-bar" style="background:var(--teal);"></div>
  <div class="slide-body">
    <div class="slide-num">06 / 06</div>

    <div class="pill animate animate-1" style="background:rgba(0,194,203,.15);border:1px solid var(--teal);color:var(--teal);">The Ask</div>

    <div class="animate animate-2">
      <div class="headline" style="font-size:clamp(38px,5.5vw,66px);color:var(--teal);margin-bottom:6px;">We have already proven<br>the hardest part.</div>
      <div class="subhead" style="margin-top:0;">We connected the tools. We built the code. FLOW is that success — made systematic, made safe, made repeatable across the whole program.</div>
    </div>

    <div class="rule animate animate-3" style="background:var(--teal);width:200px;margin:14px 0 10px;"></div>
    <div style="font-size:clamp(13px,1.5vw,16px);font-weight:700;margin-bottom:14px;color:var(--white);" class="animate animate-3">Three decisions. That's all we need today.</div>

    <div class="ask-grid animate animate-4">

      <div class="ask-card" style="border-color:var(--teal);background:rgba(0,194,203,.07);color:var(--teal);">
        <div class="ask-num">01</div>
        <div class="ask-rule" style="background:var(--teal);"></div>
        <div class="ask-title" style="color:var(--teal);">Approve Month 1</div>
        <div class="ask-detail">Authorise us to remove estimation, publish the Intent Document template, and baseline our current cycle time. Zero delivery risk. Reversible at any point.</div>
        <div class="ask-impact" style="background:rgba(0,194,203,.15);color:var(--teal);">Team saves 4–6 hrs per sprint from Day 1.</div>
      </div>

      <div class="ask-card" style="border-color:var(--gold);background:rgba(245,166,35,.07);color:var(--gold);">
        <div class="ask-num">02</div>
        <div class="ask-rule" style="background:var(--gold);"></div>
        <div class="ask-title" style="color:var(--gold);">Name the Context Curator</div>
        <div class="ask-detail">One Tech Lead gets protected time to own Confluence quality. This single role determines the quality of everything AI generates. It is the highest-leverage appointment in this program.</div>
        <div class="ask-impact" style="background:rgba(245,166,35,.15);color:var(--gold);">Context quality = AI output quality. Non-negotiable.</div>
      </div>

      <div class="ask-card" style="border-color:var(--mint);background:rgba(37,208,126,.06);color:var(--mint);">
        <div class="ask-num">03</div>
        <div class="ask-rule" style="background:var(--mint);"></div>
        <div class="ask-title" style="color:var(--mint);">30 min monthly — exec dashboard</div>
        <div class="ask-detail">One standing review per month. Cycle time, gate health, outcome delivery rate. You see the ROI data as it accumulates — not at the end of a project when it's too late to course-correct.</div>
        <div class="ask-impact" style="background:rgba(37,208,126,.15);color:var(--mint);">You stay in the loop without being in the process.</div>
      </div>

    </div>

    <div class="tagline animate animate-5" style="color:var(--slate);margin-top:10px;font-size:11px;">
      FLOW · Fast, Lean, Outcome-driven Workflow · The teams ahead in 12 months are the ones who started today.
    </div>
  </div>
</div>

</div><!-- #deck -->

<script>
// ── STATE ─────────────────────────────────────────────────
let current = 0;
const slides = document.querySelectorAll('.slide');
const total  = slides.length; // now 6
const notes  = document.getElementById('notes-panel');
const notesContent = document.getElementById('notes-content');
const notesSlideNum = document.getElementById('notes-slide-num');
const counter = document.getElementById('counter');
const progress = document.getElementById('progress');

function goTo(idx, dir = 1) {
  if (idx < 0 || idx >= total) return;

  const prev = slides[current];
  const next = slides[idx];

  prev.classList.remove('active');
  prev.classList.add('exiting');
  setTimeout(() => prev.classList.remove('exiting'), 520);

  next.classList.add('active', 'entering');
  setTimeout(() => next.classList.remove('entering'), 620);

  current = idx;

  counter.textContent = `${current + 1} / ${total}`;
  progress.style.width = `${((current + 1) / total) * 100}%`;

  if (!notes.classList.contains('open')) return;
  updateNotes();
}

function updateNotes() {
  const slide = slides[current];
  notesContent.textContent = slide.dataset.notes || 'No speaker notes for this slide.';
  notesSlideNum.textContent = current + 1;
}

// ── KEYBOARD ──────────────────────────────────────────────
document.addEventListener('keydown', e => {
  if (e.key === 'ArrowRight' || e.key === ' ' || e.key === 'PageDown') goTo(current + 1, 1);
  if (e.key === 'ArrowLeft'  || e.key === 'PageUp')   goTo(current - 1, -1);
  if (e.key === 'n' || e.key === 'N') toggleNotes();
  if (e.key === 'f' || e.key === 'F') document.documentElement.requestFullscreen?.();
  if (e.key === 'Escape') closeNotes();
});

// ── TOUCH / SWIPE ─────────────────────────────────────────
let touchStartX = 0;
document.addEventListener('touchstart', e => touchStartX = e.touches[0].clientX);
document.addEventListener('touchend', e => {
  const dx = e.changedTouches[0].clientX - touchStartX;
  if (dx < -50) goTo(current + 1, 1);
  if (dx > 50)  goTo(current - 1, -1);
});

// ── CLICK TO ADVANCE ─────────────────────────────────────
document.getElementById('deck').addEventListener('click', e => {
  if (e.target.closest('#notes-panel')) return;
  if (e.target.closest('#notes-btn'))   return;
  goTo(current + 1, 1);
});

// ── NOTES ─────────────────────────────────────────────────
function toggleNotes() {
  notes.classList.toggle('open');
  if (notes.classList.contains('open')) updateNotes();
}
function closeNotes() { notes.classList.remove('open'); }

document.getElementById('notes-btn').addEventListener('click', e => {
  e.stopPropagation();
  toggleNotes();
});
document.getElementById('notes-close').addEventListener('click', e => {
  e.stopPropagation();
  closeNotes();
});

// ── CUSTOM CURSOR ─────────────────────────────────────────
const cursor = document.getElementById('cursor');
document.addEventListener('mousemove', e => {
  cursor.style.left = e.clientX + 'px';
  cursor.style.top  = e.clientY + 'px';
});
document.addEventListener('mouseenter', () => cursor.style.opacity = '1');
document.addEventListener('mouseleave', () => cursor.style.opacity = '0');
document.querySelectorAll('button, a').forEach(el => {
  el.addEventListener('mouseenter', () => cursor.classList.add('big'));
  el.addEventListener('mouseleave', () => cursor.classList.remove('big'));
});

// ── INIT ──────────────────────────────────────────────────
progress.style.width = `${(1 / total) * 100}%`;
slides[0].classList.add('active');
</script>

</body>
</html>
