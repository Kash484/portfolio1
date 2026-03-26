---
layout: post
title: CS111 Blog — Kashyap Tubati
description: My CS111 final project walkthrough — a 3-level game I built covering OOP, data types, control structures, operators, I/O, debugging, and API integration.
author: Kashyap Tubati
date: 2026-03-23
permalink: /individual/
---

<style>
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;0,900;1,400;1,600&family=Lora:ital,wght@0,400;0,500;0,600;1,400&family=Courier+Prime:ital,wght@0,400;0,700;1,400&family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&display=swap');

  :root {
    --espresso:    #120b05;
    --roast:       #1e1008;
    --dark-wood:   #2a1a0c;
    --medium-wood: #3d2710;
    --warm-border: #5a3920;
    --tan:         #9c7450;
    --parchment:   #e8d5b7;
    --cream:       #f2e8d5;
    --ivory:       #faf4e8;
    --amber:       #c8832a;
    --gold:        #d4a030;
    --rust:        #a0522d;
    --moss:        #5c7a4a;
    --slate-blue:  #4a6070;
    --muted:       #7a5c40;
  }

  *, *::before, *::after {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body, .page-content {
    background: var(--espresso);
    color: var(--parchment);
    font-family: 'Lora', Georgia, serif;
    font-size: 16px;
    line-height: 1.75;
  }

  /* Subtle grain texture overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='300' height='300' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
    opacity: 0.6;
  }

  a {
    color: var(--amber);
    text-decoration: none;
    transition: all 0.2s ease;
    border-bottom: 1px solid transparent;
  }
  a:hover {
    color: var(--gold);
    border-bottom-color: var(--gold);
  }

  .blog-wrap {
    max-width: 940px;
    margin: 0 auto;
    padding: 60px 28px 100px;
    position: relative;
    z-index: 1;
  }

  /* ── Header ─────────────────────────────────────────── */
  .meta {
    text-align: center;
    color: var(--tan);
    font-family: 'Cormorant Garamond', serif;
    font-size: 14px;
    margin-bottom: 20px;
    letter-spacing: 3px;
    text-transform: uppercase;
    font-style: italic;
  }

  h1.title {
    text-align: center;
    font-size: 68px;
    font-weight: 900;
    color: var(--ivory);
    margin-bottom: 16px;
    line-height: 1.0;
    font-family: 'Playfair Display', Georgia, serif;
    font-style: italic;
    text-shadow:
      0 2px 8px rgba(200, 131, 42, 0.35),
      0 0 60px rgba(200, 131, 42, 0.12);
    letter-spacing: -1px;
  }

  .subtitle {
    text-align: center;
    color: var(--tan);
    font-size: 16px;
    max-width: 640px;
    margin: 0 auto 60px;
    font-family: 'Cormorant Garamond', serif;
    font-size: 19px;
    font-style: italic;
    line-height: 1.6;
  }

  /* Decorative divider */
  hr {
    border: none;
    margin: 64px 0;
    display: flex;
    align-items: center;
    text-align: center;
    position: relative;
  }
  hr::before {
    content: '✦ ✦ ✦';
    display: block;
    color: var(--warm-border);
    font-size: 13px;
    letter-spacing: 10px;
    width: 100%;
    font-family: 'Cormorant Garamond', serif;
  }

  /* ── Headings ────────────────────────────────────────── */
  h2 {
    font-size: 13px;
    font-weight: 700;
    color: var(--amber);
    margin: 60px 0 20px;
    padding-bottom: 14px;
    border-bottom: 1px solid var(--warm-border);
    text-transform: uppercase;
    letter-spacing: 3px;
    font-family: 'Lora', serif;
    position: relative;
  }
  h2::before {
    content: '';
    position: absolute;
    bottom: -1px;
    left: 0;
    width: 48px;
    height: 2px;
    background: var(--amber);
  }

  h3 {
    font-size: 24px;
    font-weight: 600;
    color: var(--ivory);
    margin: 36px 0 14px;
    font-family: 'Playfair Display', serif;
    font-style: italic;
  }

  h4 {
    font-size: 11px;
    font-weight: 700;
    color: var(--tan);
    text-transform: uppercase;
    letter-spacing: 2px;
    margin: 28px 0 12px;
    font-family: 'Lora', serif;
  }

  p {
    margin-bottom: 18px;
    color: var(--parchment);
    font-size: 15.5px;
    line-height: 1.8;
  }

  ul {
    margin: 0 0 22px 28px;
  }
  ul li {
    color: var(--parchment);
    font-size: 15.5px;
    margin-bottom: 10px;
    line-height: 1.75;
  }

  /* ── Tables ──────────────────────────────────────────── */
  .table-wrap {
    overflow-x: auto;
    margin-bottom: 32px;
    border-radius: 6px;
    border: 1px solid var(--warm-border);
    background: var(--dark-wood);
  }
  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 14px;
  }
  th {
    background: var(--medium-wood);
    color: var(--amber);
    font-weight: 700;
    text-align: left;
    padding: 13px 18px;
    border: 1px solid var(--warm-border);
    font-size: 10px;
    font-family: 'Lora', serif;
    letter-spacing: 2px;
    text-transform: uppercase;
  }
  td {
    padding: 13px 18px;
    border: 1px solid var(--warm-border);
    color: var(--parchment);
    background: var(--roast);
    vertical-align: top;
    font-size: 14px;
    line-height: 1.7;
  }
  tr:hover td {
    background: var(--dark-wood);
  }

  /* ── Code ────────────────────────────────────────────── */
  code {
    font-family: 'Courier Prime', 'Courier New', monospace;
    font-size: 13.5px;
    background: var(--dark-wood);
    color: var(--gold);
    padding: 2px 8px;
    border-radius: 3px;
    border: 1px solid var(--warm-border);
  }

  pre {
    background: var(--roast);
    border: 1px solid var(--warm-border);
    border-radius: 6px;
    padding: 22px 26px;
    overflow-x: auto;
    margin-bottom: 22px;
    font-family: 'Courier Prime', monospace;
    font-size: 13.5px;
    line-height: 1.85;
    box-shadow: inset 0 2px 12px rgba(0,0,0,0.4);
  }
  pre code {
    background: none;
    border: none;
    padding: 0;
    color: var(--parchment);
  }

  /* Syntax tokens */
  .kw   { color: #d4916a; }         /* keywords — warm rust */
  .fn   { color: var(--gold); }     /* functions — golden amber */
  .str  { color: #8fba7a; }         /* strings — sage green */
  .num  { color: #e0b86a; }         /* numbers — warm yellow */
  .cm   { color: var(--muted); font-style: italic; } /* comments — muted tan */
  .cls  { color: var(--amber); }    /* classes — amber */
  .bool { color: #c88a6a; }

  /* ── Callouts & Annotations ──────────────────────────── */
  .annotation {
    background: var(--dark-wood);
    border: 1px solid var(--warm-border);
    border-radius: 6px;
    padding: 18px 24px;
    margin-bottom: 16px;
    color: var(--parchment);
    line-height: 1.75;
    font-style: italic;
    font-family: 'Cormorant Garamond', serif;
    font-size: 17px;
  }
  .annotation strong { color: var(--cream); font-style: normal; }

  .callout {
    background: var(--dark-wood);
    border: 1px solid var(--warm-border);
    border-radius: 8px;
    padding: 18px 24px;
    margin-bottom: 26px;
    font-size: 15px;
    color: var(--parchment);
    line-height: 1.75;
  }
  .callout strong { color: var(--ivory); }

  .callout-blue   { border-color: var(--slate-blue);  background: #0d1a22; }
  .callout-green  { border-color: var(--moss);         background: #0f1a0c; }
  .callout-orange { border-color: var(--amber);        background: #1e1008; }
  .callout-yellow { border-color: var(--gold);         background: #1c1505; }

  /* ── Badges ──────────────────────────────────────────── */
  .badge {
    display: inline-block;
    font-size: 11px;
    font-weight: 700;
    padding: 3px 12px;
    border-radius: 2px;
    margin-right: 8px;
    font-family: 'Lora', serif;
    letter-spacing: 1px;
    text-transform: uppercase;
    border: 1px solid;
  }
  .b-blue   { background: #0d1a22;  color: #7aabcc; border-color: #4a6070; }
  .b-green  { background: #0f1a0c;  color: #8fba7a; border-color: #5c7a4a; }
  .b-orange { background: #1e1008;  color: var(--amber); border-color: #5a3920; }
  .b-purple { background: #1a1020;  color: #b09abf; border-color: #6a507a; }
  .b-red    { background: #1f0d08;  color: #c87060; border-color: #6a3028; }

  /* ── Tree ────────────────────────────────────────────── */
  .tree {
    background: var(--roast);
    border: 1px solid var(--warm-border);
    border-radius: 8px;
    padding: 22px 28px;
    font-family: 'Courier Prime', monospace;
    font-size: 14.5px;
    line-height: 2.2;
    margin-bottom: 28px;
    color: var(--parchment);
  }
  .tree-l0 {
    color: var(--amber);
    font-weight: 700;
    display: block;
  }
  .tree-l1 {
    color: var(--gold);
    margin-left: 28px;
    display: block;
  }
  .tree-note {
    color: var(--muted);
    font-size: 12.5px;
    font-style: italic;
  }

  /* ── TOC ─────────────────────────────────────────────── */
  .toc {
    background: var(--dark-wood);
    border: 1px solid var(--warm-border);
    border-radius: 8px;
    padding: 28px 32px;
    margin-bottom: 52px;
    font-size: 15px;
    position: relative;
  }
  .toc::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--amber), var(--rust), transparent);
    border-radius: 8px 8px 0 0;
  }
  .toc h4 {
    margin: 0 0 18px;
    color: var(--ivory);
    font-family: 'Playfair Display', serif;
    font-style: italic;
    font-size: 20px;
    font-weight: 600;
    letter-spacing: 0;
    text-transform: none;
  }
  .toc ol {
    margin-left: 22px;
    columns: 2;
    column-gap: 32px;
  }
  .toc li {
    margin-bottom: 9px;
    break-inside: avoid;
  }
  .toc a {
    color: var(--tan);
    border-bottom-color: transparent;
  }
  .toc a:hover {
    color: var(--amber);
    border-bottom-color: var(--amber);
  }

  @media (max-width: 600px) {
    .toc ol { columns: 1; }
    h1.title { font-size: 44px; }
  }

  /* ── Play Buttons ────────────────────────────────────── */
  .play-button {
    display: inline-block;
    background: var(--dark-wood);
    color: var(--amber);
    border: 1px solid var(--amber);
    border-radius: 4px;
    padding: 12px 24px;
    font-weight: 700;
    font-size: 13px;
    text-decoration: none;
    font-family: 'Lora', serif;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    margin: 6px;
    transition: all 0.22s ease;
    border-bottom: 1px solid var(--amber);
  }
  .play-button:hover {
    background: var(--amber);
    color: var(--espresso);
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(200, 131, 42, 0.3);
    border-bottom-color: var(--amber);
  }

  /* ── Game iframe ─────────────────────────────────────── */
  #game-section {
    background: var(--dark-wood);
    border: 1px solid var(--warm-border);
    border-top: 3px solid var(--amber);
    border-radius: 8px;
    padding: 24px;
    margin: 36px calc(-1 * (50vw - 470px));
    box-shadow: 0 4px 30px rgba(0,0,0,0.5);
  }

  @media (max-width: 980px) {
    #game-section {
      margin: 36px -20px;
      border-radius: 0;
    }
  }
  #game-section h3 {
    margin-top: 0;
    color: var(--ivory);
    font-size: 18px;
    letter-spacing: 0.5px;
  }
  #game-controls {
    text-align: center;
    margin-top: 16px;
    font-family: 'Courier Prime', monospace;
    font-size: 13px;
    color: var(--muted);
    letter-spacing: 1px;
  }
  #game-controls span {
    margin: 0 16px;
    display: inline-block;
  }

  /* ── Footer ──────────────────────────────────────────── */
  .footer {
    margin-top: 90px;
    padding-top: 36px;
    border-top: 1px solid var(--warm-border);
    text-align: center;
    font-size: 13px;
    color: var(--muted);
    line-height: 2.0;
    font-family: 'Cormorant Garamond', serif;
    font-style: italic;
    letter-spacing: 0.5px;
  }
</style>

<div class="blog-wrap">

<div class="meta">Mar 23, 2026 &nbsp;·&nbsp; Kashyap Tubati &nbsp;·&nbsp; Sprint 6 Final Project</div>
<h1 class="title">CS111 Blog</h1>
<p class="subtitle">
  My final project walkthrough — 3 levels, 3 totally different mechanics, and basically every CS111 concept packed into one game.
</p>

<div class="callout callout-orange">
  <strong>What this blog is:</strong> A walkthrough of every CS111 topic — OOP, data types, operators, control structures, I/O, debugging, and API — showing exactly where each one lives in the game I built.
</div>

<div class="toc">
  <h4>Table of Contents</h4>
  <ol>
    <li><a href="#overview">Game Overview — All 3 Levels</a></li>
    <li><a href="#zonecatch">Zone Catch Deep Dive (my level!)</a></li>
    <li><a href="#oop">OOP — Classes & Constructors</a></li>
    <li><a href="#methods">Methods & Parameters</a></li>
    <li><a href="#datatypes">Data Types</a></li>
    <li><a href="#operators">Operators</a></li>
    <li><a href="#control">Control Structures</a></li>
    <li><a href="#io">Input / Output</a></li>
    <li><a href="#api">API Integration</a></li>
    <li><a href="#comments">JSDoc Comments</a></li>
    <li><a href="#debugging">Debugging</a></li>
    <li><a href="#testing">Testing</a></li>
    <li><a href="#other-games">Other Games</a></li>
    <li><a href="#homework-links">Homework</a></li>
  </ol>
</div>

<hr>

<div id="game-section">
  <h3>▶ Play the Game — 3 Levels</h3>
  <iframe
    src="https://phantom-deploy.github.io/portfolio/gamify/gategame"
    width="100%"
    height="700"
    style="border: 1px solid #5a3920; border-radius: 6px; display: block; background: #120b05; min-height: 640px;"
    allowfullscreen
    title="Kashyap's 3-Level Game — Cannonball, Escape Room, Zone Catch"
  ></iframe>
  <div id="game-controls">
    <span>WASD — Move</span>
    <span>E — Interact with Gate</span>
    <span>ESC — Next Level</span>
  </div>
</div>

<hr>

<h2 id="overview">Game Overview — All 3 Levels</h2>

<p>
  Three levels, each one completely different. Level 1 is reflex-based, Level 2 is a maze, and Level 3 — the one I made — is a zone survival game that keeps shifting on you every few seconds. Here's the quick rundown:
</p>

<div class="table-wrap">
  <table>
    <tr><th>Level</th><th>Name</th><th>Goal</th><th>Main CS Concept</th></tr>
    <tr><td>1</td><td>Cannonball Dodge</td><td>Dodge cannonballs with W/S, advance to the gate, press ESC</td><td>DOM elements, AABB collision, round loop, vertical movement lock</td></tr>
    <tr><td>2</td><td>Escape Room</td><td>Navigate a barrier maze to find the master gate NPC</td><td>Barrier class, NPC interaction, OOP class composition</td></tr>
    <tr><td>3</td><td>Zone Catch</td><td>Stand in the correct coloured zone for 10 rounds, escape through the golden gate</td><td>Canvas overlay, pixel colour sampling, boolean survival check, phase timers</td></tr>
  </table>
</div>

<div class="callout callout-blue">
  <strong>Controls:</strong> WASD to move &nbsp;·&nbsp; E to interact with the gate &nbsp;·&nbsp; ESC to go to the next level
</div>

<hr>

<h2 id="zonecatch">Zone Catch — My Level (Level 3)</h2>

<p>
  Zone Catch is the level I designed and wrote from scratch. The idea is: every few seconds two coloured circles appear on screen, and a banner tells you which one is safe. You have to get into the right one before the timer hits zero — if you're standing outside it, or in the wrong one, you get eliminated. Survive 10 rounds, or find the golden gate that shows up from Round 6 and press E near it to escape early and win.
</p>

<p>
  Under the hood it runs as a <code>ZoneCatchOverlay</code> class drawn on a separate fixed <code>canvas</code> stacked on top of the game engine's canvas using <code>z-index: 9999</code>. That way I didn't need to touch any engine code — just layered my logic right on top.
</p>

<h3>How the Class is Set Up</h3>

<div class="annotation">
  Every property in the constructor is a different data type on purpose. <code>round</code> and <code>totalRounds</code> are Numbers compared each time a round ends. <code>roundActive</code>, <code>won</code>, and <code>gameOver</code> are Booleans that guard every update and draw method — if the game is over, nothing runs. <code>circles</code> is an Array of Objects where each object has a <code>safe</code> boolean telling the survival check which zone the player needs to be in.
</div>

<pre><code><span class="cm">/**
 * ZoneCatchOverlay — handles all Zone Catch game logic.
 * Drawn on a fixed canvas layered above the main game engine.
 * @class ZoneCatchOverlay
 */</span>
<span class="kw">class</span> <span class="cls">ZoneCatchOverlay</span> {
  <span class="fn">constructor</span>(gameEnv) {
    <span class="kw">this</span>.round       = <span class="num">0</span>;       <span class="cm">// Number — current round</span>
    <span class="kw">this</span>.totalRounds = <span class="num">10</span>;      <span class="cm">// Number — rounds needed to win</span>
    <span class="kw">this</span>.roundActive = <span class="bool">false</span>;   <span class="cm">// Boolean — is a round running?</span>
    <span class="kw">this</span>.won         = <span class="bool">false</span>;   <span class="cm">// Boolean — did player escape?</span>
    <span class="kw">this</span>.gameOver    = <span class="bool">false</span>;   <span class="cm">// Boolean — is game over?</span>
    <span class="kw">this</span>.circles     = [];      <span class="cm">// Array — two zone objects per round</span>
    <span class="kw">this</span>.colorPairs  = [        <span class="cm">// Array of String pairs — zone colours</span>
      [<span class="str">'#e63946'</span>, <span class="str">'#457b9d'</span>],
      [<span class="str">'#f4a261'</span>, <span class="str">'#2a9d8f'</span>],
    ];
  }
}</code></pre>

<h3>The Survival Check — Nested Conditionals + Operators</h3>

<p>
  At the end of each round, <code>_checkSurvivalAtRoundEnd()</code> runs. It reads pixel colours directly off the canvas under the player's centre using <code>getImageData</code>, then uses nested conditionals and logical operators to decide if the player made it or not.
</p>

<div class="annotation">
  The final <code>if</code> chains three conditions with <code>||</code>: die if there are no coloured pixels under the player (outside both zones), die if the safe colour is too far away (in the wrong circle), or die if the danger colour is actually closer (still wrong). Three completely different failure modes, handled in one line with logical operators.
</div>

<pre><code><span class="cm">// Sample a cross of pixels under the player centre</span>
<span class="kw">for</span> (<span class="kw">const</span> [dx, dy] <span class="kw">of</span> samplePoints) {
  <span class="kw">const</span> pixel = <span class="kw">this</span>.ctx.<span class="fn">getImageData</span>(cx+dx, cy+dy, <span class="num">1</span>, <span class="num">1</span>).data;
  <span class="kw">if</span> (pixel[<span class="num">3</span>] < <span class="num">30</span>) <span class="kw">continue</span>;  <span class="cm">// transparent = outside both circles</span>
  <span class="kw">const</span> sd = Math.<span class="fn">sqrt</span>((pixel[<span class="num">0</span>]-safeRGB.r)**<span class="num">2</span> + (pixel[<span class="num">1</span>]-safeRGB.g)**<span class="num">2</span> + (pixel[<span class="num">2</span>]-safeRGB.b)**<span class="num">2</span>);
  <span class="kw">if</span> (sd < bestSafeDist) bestSafeDist = sd;
}

<span class="cm">// Three nested conditions — any one failing = eliminated</span>
<span class="kw">if</span> (!hasOpaquePixel || bestSafeDist > <span class="num">80</span> || bestSafeDist >= bestDangerDist) {
  <span class="kw">this</span>.<span class="fn">_triggerDeath</span>();
}</code></pre>

<h3>Zone Sizing — Math Operators</h3>

<div class="annotation">
  <code>safeIdx === 0</code> evaluates to a Boolean — that's how each circle object knows if it's the safe one, without needing a separate tracking variable. The whole zone randomly repositions and potentially shrinks every round, so the player can't just memorise a spot and camp it.
</div>

<pre><code><span class="fn">_newZone</span>() {
  <span class="cm">// Zone radius shrinks by 3 pixels every round, minimum 50</span>
  <span class="kw">const</span> baseR  = Math.<span class="fn">max</span>(<span class="num">50</span>, <span class="num">95</span> - <span class="kw">this</span>.round * <span class="num">3</span>);
  <span class="kw">const</span> margin = baseR + <span class="num">16</span>;

  <span class="cm">// Random positions within the arena, factoring in margin</span>
  <span class="kw">const</span> x0 = a.x + margin + Math.<span class="fn">random</span>() * Math.<span class="fn">max</span>(<span class="num">1</span>, halfW - margin * <span class="num">2</span>);
  <span class="kw">const</span> y0 = a.y + margin + Math.<span class="fn">random</span>() * Math.<span class="fn">max</span>(<span class="num">1</span>, a.h - margin * <span class="num">2</span> - <span class="num">60</span>);

  this.circles = [
    { x: x0, y: y0, r: baseR, color: shuffled[<span class="num">0</span>], safe: safeIdx === <span class="num">0</span> },
    { x: x1, y: y1, r: baseR, color: shuffled[<span class="num">1</span>], safe: safeIdx === <span class="num">1</span> },
  ];
}</code></pre>

<h3>Gate Interaction — I/O + Boolean Guards</h3>

<pre><code><span class="cm">// Gate key handler — bound only when the gate first spawns (Round 6+)</span>
<span class="kw">this</span>._gateKeyHandler = (e) => {
  <span class="kw">if</span> (e.key !== <span class="str">'e'</span> && e.key !== <span class="str">'E'</span>) <span class="kw">return</span>;        <span class="cm">// String check</span>
  <span class="kw">if</span> (!<span class="kw">this</span>.roundActive || !<span class="kw">this</span>.gateVisible) <span class="kw">return</span>; <span class="cm">// Boolean guards</span>
  <span class="kw">const</span> p = <span class="kw">this</span>.<span class="fn">_getPlayerCenter</span>();
  <span class="kw">if</span> (p && <span class="kw">this</span>.<span class="fn">_dist</span>(p.x, p.y, g.x, g.y) < g.r * <span class="num">1.5</span>) {
    <span class="kw">this</span>.<span class="fn">_triggerWin</span>();                                 <span class="cm">// Number distance check</span>
  }
};</code></pre>

<div class="callout callout-yellow">
  <strong>Why I built it this way:</strong> Stacking an overlay canvas on top meant I could write all this logic without modifying a single line of the game engine — that's composition, building new behaviour by combining independent objects rather than rewriting what's already there.
</div>

<hr>

<h2 id="oop">OOP — Classes & Constructors</h2>

<p>
  Each level is its own class. This keeps everything cleanly separated — each one handles its own setup, update logic, and cleanup without stepping on the others.
</p>

<div class="tree">
  <span class="tree-l0">GameLevelCannonball<span class="tree-note">  ← Level 1 — cannonball dodge, DOM elements, round loop</span></span>
  <span class="tree-l0">GameLevelEscaperoom<span class="tree-note">  ← Level 2 — barrier maze, NPC gate, class composition</span></span>
  <span class="tree-l0">GameLevelZonecatch<span class="tree-note">   ← Level 3 — spawns ZoneCatchOverlay</span></span>
  <span class="tree-l1">↳ ZoneCatchOverlay<span class="tree-note">   ← the class I wrote, runs the actual zone game</span></span>
</div>

<h3>Classes & Methods Homework</h3>
<p>This is the homework where I first practiced building classes with constructors and calling methods on objects — the same exact pattern every game level uses:</p>

<div class="annotation">
  Same structure as the game levels: pass data into the constructor, store it on <code>this</code>, call methods on the object. <code>shutdown()</code> calling <code>drain()</code> internally is constructor chaining in action — just like <code>GameLevelZonecatch</code>'s constructor calling <code>new ZoneCatchOverlay(gameEnv)</code>.
</div>

<pre><code><span class="kw">class</span> <span class="cls">Robot</span> {
  <span class="fn">constructor</span>(power) {
    <span class="kw">this</span>.power = power;  <span class="cm">// Number stored on the object</span>
  }

  <span class="fn">drain</span>() {
    <span class="kw">this</span>.power -= <span class="num">10</span>;
    <span class="kw">if</span> (<span class="kw">this</span>.power < <span class="num">0</span>) <span class="kw">this</span>.power = <span class="num">0</span>;
  }

  <span class="fn">shutdown</span>() {
    <span class="kw">while</span> (<span class="kw">this</span>.power > <span class="num">0</span>) {
      <span class="kw">this</span>.<span class="fn">drain</span>();  <span class="cm">// calls drain() until power hits 0</span>
    }
  }
}

<span class="kw">let</span> myRobot = <span class="kw">new</span> <span class="cls">Robot</span>(<span class="num">35</span>);
console.<span class="fn">log</span>(myRobot.power);  <span class="cm">// 35</span>
myRobot.<span class="fn">shutdown</span>();
console.<span class="fn">log</span>(myRobot.power);  <span class="cm">// 0</span></code></pre>

<h3>Data Abstractions Homework</h3>
<p>This homework showed how <code>extends</code> and inheritance work — the game engine uses this everywhere with <code>Player</code>, <code>Npc</code>, and <code>Barrier</code> all extending a base class:</p>
<pre><code><span class="kw">class</span> <span class="cls">Pet</span> {
  <span class="fn">eat</span>() { console.<span class="fn">log</span>(<span class="str">"Nom nom nom"</span>); }
}

<span class="kw">class</span> <span class="cls">Dog</span> <span class="kw">extends</span> <span class="cls">Pet</span> {
  <span class="fn">bark</span>() { console.<span class="fn">log</span>(<span class="str">"Woof woof!"</span>); }
}

<span class="kw">const</span> myDog = <span class="kw">new</span> <span class="cls">Dog</span>();
myDog.<span class="fn">eat</span>();   <span class="cm">// inherited from Pet</span>
myDog.<span class="fn">bark</span>(); <span class="cm">// Dog's own method</span>

<span class="cm">// Calculator showing method abstraction with parameters</span>
<span class="kw">function</span> <span class="fn">calculator</span>(num1, num2, operator) {
  <span class="kw">if</span>      (operator === <span class="str">"+"</span>) <span class="kw">return</span> num1 + num2;
  <span class="kw">else if</span> (operator === <span class="str">"-"</span>) <span class="kw">return</span> num1 - num2;
  <span class="kw">else if</span> (operator === <span class="str">"*"</span>) <span class="kw">return</span> num1 * num2;
  <span class="kw">else if</span> (operator === <span class="str">"/"</span>) <span class="kw">return</span> num1 / num2;
  <span class="kw">else</span> <span class="kw">return</span> <span class="str">"Invalid operator"</span>;
}
console.<span class="fn">log</span>(<span class="fn">calculator</span>(<span class="num">10</span>, <span class="num">5</span>, <span class="str">"+"</span>));  <span class="cm">// 15</span></code></pre>

<hr>

<h2 id="methods">Methods & Parameters</h2>

<p>Here are the key methods across all three levels, each one taking parameters and returning a specific type:</p>

<h3>_dist(ax, ay, bx, by) — returns Number</h3>
<pre><code><span class="cm">/**
 * Calculates distance between two points in viewport pixels.
 * Used to check if the player is close enough to the gate.
 * @returns {number}
 */</span>
<span class="fn">_dist</span>(ax, ay, bx, by) {
  <span class="kw">return</span> Math.<span class="fn">sqrt</span>((ax - bx) ** <span class="num">2</span> + (ay - by) ** <span class="num">2</span>);
}</code></pre>

<h3>_inCircle(p, c) — returns Boolean</h3>
<pre><code><span class="cm">/**
 * Returns true if a point is inside a circle.
 * @param {Object} p - player centre with x and y properties
 * @param {Object} c - zone circle with x, y, and r properties
 * @returns {boolean}
 */</span>
<span class="fn">_inCircle</span>(p, c) {
  <span class="kw">return</span> <span class="kw">this</span>.<span class="fn">_dist</span>(p.x, p.y, c.x, c.y) < c.r;
}</code></pre>

<h3>_roundDuration() — returns Number that decreases each round</h3>
<pre><code><span class="cm">/**
 * How long the current round lasts. Gets 200ms shorter each round.
 * @returns {number} duration in milliseconds (min 3800)
 */</span>
<span class="fn">_roundDuration</span>() {
  <span class="kw">return</span> Math.<span class="fn">max</span>(<span class="num">3800</span>, <span class="kw">this</span>.baseRoundDuration - (<span class="kw">this</span>.round - <span class="num">1</span>) * <span class="num">200</span>);
}</code></pre>

<h3>_hexToRgb(hex) — takes String, returns Object</h3>
<pre><code><span class="cm">/**
 * Converts a hex colour string to RGB for pixel comparison.
 * @param {string} hex - e.g. "#e63946"
 * @returns {Object|null} Object with r, g, b number properties, or null
 */</span>
<span class="fn">_hexToRgb</span>(hex) {
  <span class="kw">const</span> m = <span class="str">/^#([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i</span>.<span class="fn">exec</span>(hex);
  <span class="kw">return</span> m ? { r: <span class="fn">parseInt</span>(m[<span class="num">1</span>],<span class="num">16</span>), g: <span class="fn">parseInt</span>(m[<span class="num">2</span>],<span class="num">16</span>), b: <span class="fn">parseInt</span>(m[<span class="num">3</span>],<span class="num">16</span>) } : <span class="bool">null</span>;
}</code></pre>

<h3>_collidesWithPlayer(player) — AABB check, returns Boolean</h3>
<pre><code><span class="cm">/**
 * Checks if the cannonball overlaps the player hitbox (Level 1).
 * Uses axis-aligned bounding box collision.
 * @returns {boolean}
 */</span>
<span class="fn">_collidesWithPlayer</span>(player) {
  <span class="kw">const</span> hbW = player.spriteData?.hitbox?.widthPercentage  ?? <span class="num">0.4</span>;
  <span class="kw">const</span> hbH = player.spriteData?.hitbox?.heightPercentage ?? <span class="num">0.4</span>;
  <span class="kw">const</span> sx  = pw * (<span class="num">1</span> - hbW) / <span class="num">2</span>;
  <span class="kw">const</span> pb  = { x: px+sx, y: py+sy, x2: px+pw-sx, y2: py+ph-sy };
  <span class="kw">return</span> !(cb.x2 < pb.x || cb.x > pb.x2 || cb.y2 < pb.y || cb.y > pb.y2);
}</code></pre>

<hr>

<h2 id="datatypes">Data Types</h2>

<div class="table-wrap">
  <table>
    <tr><th>Type</th><th>Where It Shows Up</th><th>Example from the Game</th></tr>
    <tr><td><span class="badge b-orange">Number</span></td><td>Round counter, zone radius, timer durations, pixel colour distances, speed — basically everywhere there's math.</td><td><code>this.round = 0</code> · <code>baseR = 95 - round * 3</code></td></tr>
    <tr><td><span class="badge b-blue">String</span></td><td>Zone colours stored as hex strings. The keyboard handler compares <code>e.key</code> to strings. All HUD labels are strings built with template literals.</td><td><code>color: '#e63946'</code> · <code>e.key !== 'e'</code></td></tr>
    <tr><td><span class="badge b-red">Boolean</span></td><td><code>roundActive</code>, <code>won</code>, and <code>gameOver</code> control which screen gets drawn. Each circle has a <code>safe</code> boolean. <code>_inCircle()</code> returns a boolean.</td><td><code>this.roundActive = false</code> · <code>safe: safeIdx === 0</code></td></tr>
    <tr><td><span class="badge b-green">Array</span></td><td><code>this.circles</code> holds the two zone objects. <code>colorPairs</code> stores the colour options. <code>samplePoints</code> is an array of pixel offsets.</td><td><code>this.circles = []</code> · <code>colorPairs = [['#e63946','#457b9d'],...]</code></td></tr>
    <tr><td><span class="badge b-purple">Object</span></td><td>Each circle is an object with x, y, r, color, and safe properties. The gate is an object. Player position returns as an object with x and y from <code>_getPlayerCenter()</code>.</td><td><code>{ x:400, y:300, r:80, color:'#e63946', safe:true }</code></td></tr>
  </table>
</div>

<h3>JSON Homework</h3>
<p>The same <code>stringify</code> and <code>parse</code> pattern used in the leaderboard API call — practiced right here:</p>
<pre><code><span class="kw">const</span> resume = {
  fullName:  <span class="str">"Kash Tubati"</span>,
  email:     <span class="str">"kash.tubati@gmail.com"</span>,
  education: <span class="str">"9th Grade"</span>,
  address:   { city: <span class="str">"San Diego"</span>, state: <span class="str">"California"</span>, country: <span class="str">"USA"</span> },
  skills:    [<span class="str">"JavaScript"</span>, <span class="str">"Python"</span>, <span class="str">"Problem Solving"</span>, <span class="str">"Debugging"</span>]
};

console.<span class="fn">log</span>(<span class="str">"City: "</span> + resume.address.city);  <span class="cm">// dot notation on nested object</span>

<span class="kw">let</span> jsonString   = JSON.<span class="fn">stringify</span>(resume);   <span class="cm">// convert to JSON string</span>
<span class="kw">let</span> parsedResume = JSON.<span class="fn">parse</span>(jsonString);    <span class="cm">// parse back to object</span>
console.<span class="fn">log</span>(parsedResume);</code></pre>

<h3>Arrays Homework</h3>
<p>Array manipulation — looping, modifying, and accessing by index, the same operations I do on <code>this.circles</code> every round:</p>
<pre><code><span class="kw">const</span> myGames = [<span class="str">"COD"</span>, <span class="str">"Minecraft"</span>, <span class="str">"Forza"</span>, <span class="str">"Clash"</span>, <span class="str">"Roblox"</span>];
console.<span class="fn">log</span>(<span class="str">"First:"</span>, myGames[<span class="num">0</span>]);
console.<span class="fn">log</span>(<span class="str">"Last:"</span>,  myGames[myGames.length - <span class="num">1</span>]);

<span class="kw">let</span> shoppingList = [<span class="str">"milk"</span>, <span class="str">"eggs"</span>, <span class="str">"bread"</span>, <span class="str">"cheese"</span>];
shoppingList[<span class="num">1</span>] = <span class="str">"butter"</span>;   <span class="cm">// replace by index</span>
shoppingList.<span class="fn">push</span>(<span class="str">"yogurt"</span>); <span class="cm">// add to end</span>
shoppingList.<span class="fn">splice</span>(<span class="num">2</span>, <span class="num">1</span>);   <span class="cm">// remove at index 2</span>

<span class="kw">const</span> numbers = [<span class="num">10</span>, <span class="num">25</span>, <span class="num">30</span>, <span class="num">15</span>, <span class="num">20</span>];
<span class="kw">let</span> sum = <span class="num">0</span>;
<span class="kw">for</span> (<span class="kw">let</span> i = <span class="num">0</span>; i < numbers.length; i++) {
  sum += numbers[i];
}
console.<span class="fn">log</span>(<span class="str">"Total:"</span>, sum);</code></pre>

<h3>Strings Homework</h3>
<p>String length, indexing, and template literals — all over the HUD code and colour hex handling:</p>
<pre><code><span class="kw">let</span> str1 = <span class="str">"Homework"</span>, str2 = <span class="str">"JavaScript is fun"</span>, str3 = <span class="str">"I like coding"</span>;

console.<span class="fn">log</span>(<span class="str">`Length of str1: ${str1.length}`</span>);
console.<span class="fn">log</span>(<span class="str">`str1 — first: ${str1[0]}, last: ${str1[str1.length - 1]}`</span>);

<span class="cm">// Template literal — same pattern used for all HUD text in the game</span>
<span class="kw">let</span> sentence = <span class="str">`${str1}: ${str2}. ${str3}!`</span>;
console.<span class="fn">log</span>(sentence);</code></pre>

<hr>

<h2 id="operators">Operators</h2>

<div class="table-wrap">
  <table>
    <tr><th>Type</th><th>Operators Used</th><th>What They Do in the Game</th></tr>
    <tr><td>Mathematical</td><td><code>+</code> <code>-</code> <code>*</code> <code>/</code> <code>**</code> <code>%</code> <code>Math.sqrt()</code> <code>Math.max()</code></td><td><code>95 - round * 3</code> shrinks the zone each round. <code>(ax-bx)**2</code> is the distance formula. <code>Math.max(50, ...)</code> stops zones from getting impossibly small.</td></tr>
    <tr><td>Boolean / Logical</td><td><code>&&</code> <code>||</code> <code>!</code> <code>===</code> <code>!==</code> <code>&lt;</code> <code>&gt;</code></td><td><code>!roundActive || !gateVisible</code> short-circuits the gate check. <code>bestSafeDist >= bestDangerDist</code> catches standing in the wrong zone.</td></tr>
    <tr><td>Assignment</td><td><code>=</code> <code>+=</code> <code>-=</code> <code>++</code></td><td><code>this.round++</code> advances the counter. <code>gateCircle.alpha -= fadeRate</code> makes the gate pulse and slowly disappear.</td></tr>
    <tr><td>Nullish / Optional</td><td><code>??</code> <code>?.</code></td><td><code>player.spriteData?.hitbox?.widthPercentage ?? 0.4</code> safely reads a nested property with a fallback — stops crashes when hitbox data is missing.</td></tr>
  </table>
</div>

<h3>Mathematical Expressions Homework</h3>
<p>Modulo and arithmetic — the same patterns used in zone sizing and phase timing:</p>
<pre><code><span class="cm">// Divisibility check with modulo — same as checking phase/round conditions</span>
<span class="kw">let</span> y = <span class="num">17</span>;
<span class="kw">let</span> remainder = y % <span class="num">5</span>;
<span class="kw">if</span> (remainder === <span class="num">0</span>) {
  console.<span class="fn">log</span>(y + <span class="str">" is divisible by 5."</span>);
} <span class="kw">else</span> {
  console.<span class="fn">log</span>(y + <span class="str">" is NOT divisible by 5. Remainder: "</span> + remainder);
}

<span class="cm">// Variable sum — same as accumulating colour distances in the survival check</span>
<span class="kw">let</span> a = <span class="num">15</span>, b = <span class="num">25</span>;
<span class="kw">let</span> sum = a + b;
console.<span class="fn">log</span>(<span class="str">"Total: "</span> + sum);</code></pre>

<hr>

<h2 id="control">Control Structures</h2>

<h3>Iterations Homework</h3>
<p>The for loop pattern I rely on constantly — iterating over pixels, game objects, and round counters:</p>
<pre><code><span class="cm">/**
 * Sum numbers from 1 to n — same loop structure as iterating samplePoints.
 */</span>
<span class="kw">function</span> <span class="fn">sumNumbers</span>(n) {
  <span class="kw">let</span> sum = <span class="num">0</span>;
  <span class="kw">for</span> (<span class="kw">let</span> i = <span class="num">1</span>; i <= n; i++) {
    sum += i;
  }
  <span class="kw">return</span> sum;
}

<span class="kw">let</span> result = <span class="fn">sumNumbers</span>(<span class="num">5</span>);
console.<span class="fn">log</span>(<span class="str">"Sum 1 to 5:"</span>, result);  <span class="cm">// 15</span></code></pre>

<h3>Nested Conditionals Homework</h3>
<p>Multiple levels of if/else — the direct foundation of the Zone Catch survival check's layered decision logic:</p>

<div class="annotation">
  Five levels of nesting — and this is exactly the structure Zone Catch uses: first check if there are opaque pixels, then check colour distance to safe, then compare against danger. Layered conditions are the only way to handle decisions that have multiple independent requirements.
</div>

<pre><code><span class="kw">const</span> factorsOf50 = [<span class="num">1</span>, <span class="num">2</span>, <span class="num">5</span>, <span class="num">10</span>, <span class="num">25</span>, <span class="num">50</span>];

<span class="kw">for</span> (<span class="kw">let</span> i = <span class="num">1</span>; i <= <span class="num">50</span>; i++) {
  <span class="cm">// Level 1: upper vs lower range</span>
  <span class="kw">if</span> (i > <span class="num">25</span>) {
    <span class="cm">// Level 2: factor of 50?</span>
    <span class="kw">if</span> (factorsOf50.<span class="fn">includes</span>(i)) {
      console.<span class="fn">log</span>(<span class="str">`${i} is in the upper range and is a factor of 50.`</span>);
    } <span class="kw">else</span> {
      <span class="cm">// Level 3: divisible by 3?</span>
      <span class="kw">if</span> (i % <span class="num">3</span> === <span class="num">0</span>) {
        console.<span class="fn">log</span>(<span class="str">`${i} is in the upper range and divisible by 3.`</span>);
      } <span class="kw">else</span> {
        console.<span class="fn">log</span>(<span class="str">`${i} is in the upper range (no match).`</span>);
      }
    }
  } <span class="kw">else</span> {
    <span class="kw">if</span> (factorsOf50.<span class="fn">includes</span>(i)) {
      <span class="cm">// Level 3: even or odd factor?</span>
      <span class="kw">if</span> (i % <span class="num">2</span> === <span class="num">0</span>) {
        console.<span class="fn">log</span>(<span class="str">`${i} is an EVEN factor of 50.`</span>);
      } <span class="kw">else</span> {
        console.<span class="fn">log</span>(<span class="str">`${i} is an ODD factor of 50.`</span>);
      }
    } <span class="kw">else</span> {
      <span class="kw">if</span> (i % <span class="num">3</span> === <span class="num">0</span>) {
        console.<span class="fn">log</span>(<span class="str">`${i} is 25 or less and divisible by 3.`</span>);
      } <span class="kw">else</span> {
        console.<span class="fn">log</span>(<span class="str">`${i} is 25 or less (no match).`</span>);
      }
    }
  }
}</code></pre>

<h3>Booleans Homework</h3>
<p>The <code>&&</code> and <code>||</code> logic that powers every guard clause in the game:</p>
<pre><code><span class="cm">// Check if a number is both positive AND even</span>
<span class="kw">function</span> <span class="fn">isPositiveAndEven</span>(num) {
  <span class="kw">let</span> isPositive = num > <span class="num">0</span>;        <span class="cm">// Boolean</span>
  <span class="kw">let</span> isEven     = num % <span class="num">2</span> === <span class="num">0</span>;  <span class="cm">// Boolean</span>
  <span class="kw">return</span> isPositive && isEven;      <span class="cm">// both must be true</span>
}

console.<span class="fn">log</span>(<span class="fn">isPositiveAndEven</span>(<span class="num">8</span>));   <span class="cm">// true</span>
console.<span class="fn">log</span>(<span class="fn">isPositiveAndEven</span>(-<span class="num">4</span>));  <span class="cm">// false — positive check fails</span></code></pre>

<hr>

<h2 id="io">Input / Output</h2>

<h3>Keyboard Input</h3>
<p>
  All three levels read keyboard input through event listeners. In Zone Catch I bind my own handler for the E key — but only when the gate spawns in Round 6 so it's not wasting memory before that. When the level ends I always remove the listener to keep things clean.
</p>

<pre><code><span class="cm">// Only bind the gate key when the gate actually appears</span>
<span class="kw">this</span>._gateKeyHandler = (e) => {
  <span class="kw">if</span> (e.key !== <span class="str">'e'</span> && e.key !== <span class="str">'E'</span>) <span class="kw">return</span>;
  <span class="kw">if</span> (!<span class="kw">this</span>.roundActive || !<span class="kw">this</span>.gateVisible) <span class="kw">return</span>;
  <span class="kw">const</span> p = <span class="kw">this</span>.<span class="fn">_getPlayerCenter</span>();
  <span class="kw">if</span> (p && <span class="kw">this</span>.<span class="fn">_dist</span>(p.x, p.y, g.x, g.y) < g.r * <span class="num">1.5</span>) {
    <span class="kw">this</span>.<span class="fn">_triggerWin</span>();
  }
};
window.<span class="fn">addEventListener</span>(<span class="str">'keydown'</span>, <span class="kw">this</span>._gateKeyHandler);

<span class="cm">// Always clean up when the level ends</span>
<span class="fn">_unbindGateKey</span>() {
  window.<span class="fn">removeEventListener</span>(<span class="str">'keydown'</span>, <span class="kw">this</span>._gateKeyHandler);
}</code></pre>

<h3>Canvas Output — the Game Loop</h3>
<pre><code><span class="cm">// 60fps render loop — update state then draw each frame</span>
<span class="fn">_loop</span>() {
  <span class="kw">this</span>._animFrame = <span class="fn">requestAnimationFrame</span>(() => <span class="kw">this</span>.<span class="fn">_loop</span>());
  <span class="kw">this</span>.<span class="fn">_resize</span>();   <span class="cm">// sync canvas to viewport size</span>
  <span class="kw">this</span>.<span class="fn">_update</span>();   <span class="cm">// advance game state</span>
  <span class="kw">this</span>.<span class="fn">_draw</span>();     <span class="cm">// render everything to canvas</span>
}</code></pre>

<hr>

<h2 id="api">API Integration</h2>

<p>
  The game connects to a leaderboard API using <code>async/await</code> and <code>fetch</code>. The score gets converted to JSON, sent as a POST request, and the response is parsed back out — same <code>stringify</code>/<code>parse</code> pattern from the JSON homework:
</p>

<pre><code><span class="cm">/**
 * Posts the player's score to the leaderboard API.
 * @param {string} playerName
 * @param {number} score
 * @returns {Promise} resolves to the response Object
 */</span>
<span class="kw">async</span> <span class="fn">postScore</span>(playerName, score) {
  <span class="kw">try</span> {
    <span class="kw">const</span> response = <span class="kw">await</span> <span class="fn">fetch</span>(<span class="str">`${<span class="kw">this</span>.gameEnv.pythonURI}/api/leaderboard`</span>, {
      method:  <span class="str">'POST'</span>,
      headers: { <span class="str">'Content-Type'</span>: <span class="str">'application/json'</span> },
      body:    JSON.<span class="fn">stringify</span>({ player: playerName, score })
    });
    <span class="kw">if</span> (!response.ok) <span class="kw">throw</span> <span class="kw">new</span> <span class="cls">Error</span>(<span class="str">`HTTP ${response.status}`</span>);
    <span class="kw">return</span> <span class="kw">await</span> response.<span class="fn">json</span>();
  } <span class="kw">catch</span> (err) {
    console.<span class="fn">error</span>(<span class="str">'[API] POST failed:'</span>, err.message);
    <span class="kw">return</span> <span class="bool">null</span>;
  }
}</code></pre>

<hr>

<h2 id="comments">JSDoc Comments</h2>

<p>Every method in Zone Catch has a JSDoc block. Here's the pattern I used throughout:</p>

<pre><code><span class="cm">/**
 * ZoneCatchOverlay — overlay class for Level 3.
 * Stacks on top of the game engine canvas using z-index: 9999.
 * Player survives by standing in the safe colour zone each round.
 *
 * @class ZoneCatchOverlay
 * @param {Object} gameEnv - game environment from the engine
 * @example
 * gameEnv._zoneCatchOverlay = new ZoneCatchOverlay(gameEnv);
 */</span>

<span class="cm">/**
 * Runs at the end of each round to check if the player survived.
 * Samples pixel colours under the player centre on the overlay canvas.
 * @returns {void} — calls _triggerDeath() or continues to next round
 */</span>
<span class="fn">_checkSurvivalAtRoundEnd</span>() { ... }

<span class="cm">/**
 * Converts a hex colour string to RGB for colour distance comparison.
 * @param {string} hex - colour in #rrggbb format
 * @returns {Object|null} Object with r, g, b number properties
 */</span>
<span class="fn">_hexToRgb</span>(hex) { ... }</code></pre>

<hr>

<h2 id="debugging">Debugging</h2>

<div class="table-wrap">
  <table>
    <tr><th>DevTools Tab</th><th>What I Used It For</th></tr>
    <tr><td><strong>Console</strong></td><td>Logged round transitions, pixel sample values, and player coordinates to debug the survival check. Prefixed everything with <code>[ZoneCatch]</code> so logs were easy to filter.</td></tr>
    <tr><td><strong>Sources</strong></td><td>Set breakpoints inside <code>_checkSurvivalAtRoundEnd()</code> to step through pixel sampling and figure out why players were dying even when they looked inside the zone.</td></tr>
    <tr><td><strong>Network</strong></td><td>Confirmed the leaderboard POST was sending the right JSON body and getting back 200 instead of 401 or 500.</td></tr>
    <tr><td><strong>Application</strong></td><td>Checked localStorage for auth tokens to make sure API requests were going out with the right session credentials.</td></tr>
    <tr><td><strong>Elements</strong></td><td>Inspected the overlay canvas to confirm <code>z-index</code> was actually stacking it above the game canvas, and that <code>pointer-events: none</code> wasn't blocking player movement.</td></tr>
  </table>
</div>

<h4>Logging Pattern</h4>
<pre><code>console.<span class="fn">log</span>(<span class="str">`[ZoneCatch] Round ${<span class="kw">this</span>.round} — duration: ${<span class="kw">this</span>.<span class="fn">_roundDuration</span>()}ms`</span>);
console.<span class="fn">log</span>(<span class="str">`[ZoneCatch] Safe: ${safe.color}, bestSafeDist: ${bestSafeDist.<span class="fn">toFixed</span>(1)}`</span>);
console.<span class="fn">log</span>(<span class="str">`[ZoneCatch] Player at (${cx}, ${cy}), hasOpaquePixel: ${hasOpaquePixel}`</span>);
console.<span class="fn">error</span>(<span class="str">`[API] POST failed: ${error.message}`</span>);</code></pre>

<hr>

<h2 id="testing">Testing</h2>

<p>
  I played through all three levels multiple times. For Zone Catch specifically, I tested: standing right on the border of a zone circle (semi-transparent pixels near the edge — solved by sampling a cross-pattern instead of just one pixel), pressing E right as the gate was fading out, and completing all 10 rounds without touching the gate to verify the full-survival win path still works.
</p>

<pre><code><span class="cm">// Edge case: player on zone border — alpha ~28, just under the 30 threshold</span>
<span class="cm">// Fix: sample a 3x3 cross pattern instead of single centre pixel</span>

<span class="cm">// Edge case: gate key fires between rounds when roundActive = false</span>
<span class="cm">// Fix: !this.roundActive guard at top of handler blocks it</span>

<span class="cm">// Edge case: cannonball collision registered on multiple frames</span>
<span class="cm">// Fix: this.collisionHappened flag prevents double-firing per round</span></code></pre>

<hr>

<h2 id="other-games">Other Games My Team Built</h2>

<p>On top of the three levels I made, my teammates built some other games that hit the same CS111 concepts from different directions:</p>

<div style="text-align:center; margin: 28px 0;">
  <a class="play-button" href="https://rashig-1804.github.io/csse_teamrepo/hacks/TicTacToe/" target="_blank" rel="noopener noreferrer">▶ Tic-Tac-Toe</a>
  <a class="play-button" href="https://rashig-1804.github.io/csse_teamrepo/connect4/" target="_blank" rel="noopener noreferrer">▶ Connect 4</a>
  <a class="play-button" href="https://aadis12.github.io/student/hacks/whackamole" target="_blank" rel="noopener noreferrer">▶ Whack-a-Mole</a>
</div>

<div class="callout callout-blue">
  <strong>How they connect:</strong> Tic-Tac-Toe shows 2D array win checking and DOM I/O. Connect 4 has multiple cooperating classes with timer-driven state. Whack-a-Mole uses inheritance (Entity → Mole/Bomb), method overriding, and localStorage for high scores — all the same OOP and control structure concepts, just in a totally different game format.
</div>

<hr>

<h2 id="homework-links">Homework</h2>

<p>Every homework below connects directly to something in the game — these aren't just random exercises, they're the actual building blocks:</p>

<ul>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/24/nestedconditionals-redo.html" target="_blank">Nested Conditionals</a></strong> — the multi-level if/else is the backbone of Zone Catch's survival check</li>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/24/iterationshomework-redo.html" target="_blank">Iterations</a></strong> — for loops used in pixel sampling, bullet processing, and round scheduling</li>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/24/arrays-homework.html" target="_blank">Arrays</a></strong> — circles array, colorPairs, samplePoints all drive Zone Catch logic</li>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/24/booleans-redo.html" target="_blank">Booleans</a></strong> — every guard clause and state flag in the game is a boolean</li>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/24/mathematicalexpressions-redo.html" target="_blank">Mathematical Expressions</a></strong> — modulo, arithmetic, and Math methods used in zone sizing and distance checks</li>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/24/jsonhw-redo.html" target="_blank">JSON</a></strong> — JSON.stringify and JSON.parse used directly in the leaderboard API</li>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/24/dataabstractions-redo.html" target="_blank">Data Abstractions</a></strong> — encapsulating state into class properties and abstracting repeated logic into methods</li>
  <li><strong><a href="https://kash484.github.io/portfolio/js/strings-hw" target="_blank">Strings</a></strong> — template literals, string indexing, and hex colour strings throughout</li>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/25/Classes&Methods-redo.html" target="_blank">Classes & Methods</a></strong> — the constructor/method pattern every level class is built on</li>
</ul>

<div class="callout callout-green">
  <strong>The point:</strong> Every single homework has a real equivalent somewhere in the game. It's not just practice — the concepts genuinely show up in the final project.
</div>

<div class="footer">
  Built with JavaScript &nbsp;·&nbsp; HTML5 Canvas &nbsp;·&nbsp; Game Engine v1 &nbsp;·&nbsp; requestAnimationFrame<br>
  CSSE Final Project — Sprint 6 &nbsp;·&nbsp; Kashyap Tubati &nbsp;·&nbsp; Mar 23, 2026
</div>

</div>