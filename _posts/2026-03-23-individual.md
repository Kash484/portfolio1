---
layout: post
title: CS111 Blog — Kashyap Tubati
description: My CS111 final project walkthrough — a 3-level game covering control structures, data types, and operators.
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

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body, .page-content {
    background: var(--espresso);
    color: var(--parchment);
    font-family: 'Lora', Georgia, serif;
    font-size: 16px;
    line-height: 1.75;
  }

  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='300' height='300' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
    opacity: 0.6;
  }

  a { color: var(--amber); text-decoration: none; transition: all 0.2s ease; border-bottom: 1px solid transparent; }
  a:hover { color: var(--gold); border-bottom-color: var(--gold); }

  .blog-wrap { max-width: 940px; margin: 0 auto; padding: 60px 28px 100px; position: relative; z-index: 1; }

  .meta {
    text-align: center; color: var(--tan); font-family: 'Cormorant Garamond', serif;
    font-size: 14px; margin-bottom: 20px; letter-spacing: 3px;
    text-transform: uppercase; font-style: italic;
  }

  h1.title {
    text-align: center; font-size: 68px; font-weight: 900; color: var(--ivory);
    margin-bottom: 16px; line-height: 1.0; font-family: 'Playfair Display', Georgia, serif;
    font-style: italic; letter-spacing: -1px;
    text-shadow: 0 2px 8px rgba(200,131,42,0.35), 0 0 60px rgba(200,131,42,0.12);
  }

  .subtitle {
    text-align: center; color: var(--tan); max-width: 640px; margin: 0 auto 60px;
    font-family: 'Cormorant Garamond', serif; font-size: 19px; font-style: italic; line-height: 1.6;
  }

  hr { border: none; margin: 64px 0; text-align: center; position: relative; }
  hr::before {
    content: '✦ ✦ ✦'; display: block; color: var(--warm-border);
    font-size: 13px; letter-spacing: 10px; font-family: 'Cormorant Garamond', serif;
  }

  h2 {
    font-size: 13px; font-weight: 700; color: var(--amber); margin: 60px 0 20px;
    padding-bottom: 14px; border-bottom: 1px solid var(--warm-border);
    text-transform: uppercase; letter-spacing: 3px; font-family: 'Lora', serif; position: relative;
  }
  h2::before {
    content: ''; position: absolute; bottom: -1px; left: 0;
    width: 48px; height: 2px; background: var(--amber);
  }

  h3 {
    font-size: 24px; font-weight: 600; color: var(--ivory); margin: 36px 0 14px;
    font-family: 'Playfair Display', serif; font-style: italic;
  }

  h4 {
    font-size: 11px; font-weight: 700; color: var(--tan);
    text-transform: uppercase; letter-spacing: 2px; margin: 28px 0 12px; font-family: 'Lora', serif;
  }

  p { margin-bottom: 18px; color: var(--parchment); font-size: 15.5px; line-height: 1.8; }

  ul { margin: 0 0 22px 28px; }
  ul li { color: var(--parchment); font-size: 15.5px; margin-bottom: 10px; line-height: 1.75; }

  .table-wrap { overflow-x: auto; margin-bottom: 32px; border-radius: 6px; border: 1px solid var(--warm-border); background: var(--dark-wood); }
  table { width: 100%; border-collapse: collapse; font-size: 14px; }
  th {
    background: var(--medium-wood); color: var(--amber); font-weight: 700; text-align: left;
    padding: 13px 18px; border: 1px solid var(--warm-border); font-size: 10px;
    font-family: 'Lora', serif; letter-spacing: 2px; text-transform: uppercase;
  }
  td {
    padding: 13px 18px; border: 1px solid var(--warm-border); color: var(--parchment);
    background: var(--roast); vertical-align: top; font-size: 14px; line-height: 1.7;
  }
  tr:hover td { background: var(--dark-wood); }

  code {
    font-family: 'Courier Prime', 'Courier New', monospace; font-size: 13.5px;
    background: var(--dark-wood); color: var(--gold); padding: 2px 8px;
    border-radius: 3px; border: 1px solid var(--warm-border);
  }

  pre {
    background: var(--roast); border: 1px solid var(--warm-border); border-radius: 6px;
    padding: 22px 26px; overflow-x: auto; margin-bottom: 22px;
    font-family: 'Courier Prime', monospace; font-size: 13.5px; line-height: 1.85;
    box-shadow: inset 0 2px 12px rgba(0,0,0,0.4);
  }
  pre code { background: none; border: none; padding: 0; color: var(--parchment); }

  .kw   { color: #d4916a; }
  .fn   { color: var(--gold); }
  .str  { color: #8fba7a; }
  .num  { color: #e0b86a; }
  .cm   { color: var(--muted); font-style: italic; }
  .cls  { color: var(--amber); }
  .bool { color: #c88a6a; }

  .annotation {
    background: var(--dark-wood); border: 1px solid var(--warm-border); border-radius: 6px;
    padding: 18px 24px; margin-bottom: 16px; color: var(--parchment); line-height: 1.75;
    font-style: italic; font-family: 'Cormorant Garamond', serif; font-size: 17px;
  }
  .annotation strong { color: var(--cream); font-style: normal; }

  .callout {
    background: var(--dark-wood); border: 1px solid var(--warm-border); border-radius: 8px;
    padding: 18px 24px; margin-bottom: 26px; font-size: 15px; color: var(--parchment); line-height: 1.75;
  }
  .callout strong { color: var(--ivory); }
  .callout-blue   { border-color: var(--slate-blue); background: #0d1a22; }
  .callout-green  { border-color: var(--moss);       background: #0f1a0c; }
  .callout-orange { border-color: var(--amber);      background: #1e1008; }
  .callout-yellow { border-color: var(--gold);       background: #1c1505; }

  .badge {
    display: inline-block; font-size: 11px; font-weight: 700; padding: 3px 12px;
    border-radius: 2px; margin-right: 8px; font-family: 'Lora', serif;
    letter-spacing: 1px; text-transform: uppercase; border: 1px solid;
  }
  .b-blue   { background: #0d1a22; color: #7aabcc;      border-color: #4a6070; }
  .b-green  { background: #0f1a0c; color: #8fba7a;      border-color: #5c7a4a; }
  .b-orange { background: #1e1008; color: var(--amber); border-color: #5a3920; }
  .b-purple { background: #1a1020; color: #b09abf;      border-color: #6a507a; }
  .b-red    { background: #1f0d08; color: #c87060;      border-color: #6a3028; }

  .toc {
    background: var(--dark-wood); border: 1px solid var(--warm-border); border-radius: 8px;
    padding: 28px 32px; margin-bottom: 52px; font-size: 15px; position: relative;
  }
  .toc::before {
    content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px;
    background: linear-gradient(90deg, var(--amber), var(--rust), transparent);
    border-radius: 8px 8px 0 0;
  }
  .toc h4 {
    margin: 0 0 18px; color: var(--ivory); font-family: 'Playfair Display', serif;
    font-style: italic; font-size: 20px; font-weight: 600; letter-spacing: 0; text-transform: none;
  }
  .toc ol { margin-left: 22px; columns: 2; column-gap: 32px; }
  .toc li { margin-bottom: 9px; break-inside: avoid; }
  .toc a { color: var(--tan); border-bottom-color: transparent; }
  .toc a:hover { color: var(--amber); border-bottom-color: var(--amber); }

  @media (max-width: 600px) { .toc ol { columns: 1; } h1.title { font-size: 44px; } }

  .play-button {
    display: inline-block; background: var(--dark-wood); color: var(--amber);
    border: 1px solid var(--amber); border-radius: 4px; padding: 12px 24px;
    font-weight: 700; font-size: 13px; text-decoration: none; font-family: 'Lora', serif;
    letter-spacing: 1.5px; text-transform: uppercase; margin: 6px; transition: all 0.22s ease;
  }
  .play-button:hover {
    background: var(--amber); color: var(--espresso); transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(200,131,42,0.3);
  }

  #game-section {
    background: var(--dark-wood); border: 1px solid var(--warm-border);
    border-top: 3px solid var(--amber); border-radius: 8px; padding: 24px;
    margin: 36px calc(-1 * (50vw - 470px)); box-shadow: 0 4px 30px rgba(0,0,0,0.5);
  }
  @media (max-width: 980px) { #game-section { margin: 36px -20px; border-radius: 0; } }
  #game-section h3 { margin-top: 0; color: var(--ivory); font-size: 18px; }
  #game-controls {
    text-align: center; margin-top: 16px; font-family: 'Courier Prime', monospace;
    font-size: 13px; color: var(--muted); letter-spacing: 1px;
  }
  #game-controls span { margin: 0 16px; display: inline-block; }

  .footer {
    margin-top: 90px; padding-top: 36px; border-top: 1px solid var(--warm-border);
    text-align: center; font-size: 13px; color: var(--muted); line-height: 2.0;
    font-family: 'Cormorant Garamond', serif; font-style: italic; letter-spacing: 0.5px;
  }
</style>

<div class="blog-wrap">

<div class="meta">Mar 23, 2026 &nbsp;·&nbsp; Kashyap Tubati &nbsp;·&nbsp; Sprint 6 Final Project</div>
<h1 class="title">CS111 Blog</h1>
<p class="subtitle">
  My final project walkthrough — 3 levels, 3 totally different mechanics, and every CS111 concept packed into one game.
</p>

<div class="callout callout-orange">
  <strong>What this blog covers:</strong> Control Structures (iteration, conditionals, nested conditions) · Data Types (numbers, strings, booleans, arrays, objects) · Operators (mathematical, string operations, boolean expressions) — all shown directly in the game I built.
</div>

<div class="toc">
  <h4>Table of Contents</h4>
  <ol>
    <li><a href="#overview">Game Overview — All 3 Levels</a></li>
    <li><a href="#zonecatch">Zone Catch Deep Dive</a></li>
    <li><a href="#control">Control Structures</a></li>
    <li><a href="#datatypes">Data Types</a></li>
    <li><a href="#operators">Operators</a></li>
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

<p>Three levels, each one completely different. Level 1 is reflex-based, Level 2 is a maze, and Level 3 — the one I made — is a zone survival game that keeps shifting on you every few seconds.</p>

<div class="table-wrap">
  <table>
    <tr><th>Level</th><th>Name</th><th>Goal</th><th>Main CS Concept</th></tr>
    <tr><td>1</td><td>Cannonball Dodge</td><td>Dodge cannonballs with W/S, advance to the gate, press ESC</td><td>AABB collision, for loop round cycle, boolean collision flag</td></tr>
    <tr><td>2</td><td>Escape Room</td><td>Navigate a barrier maze to find the master gate NPC</td><td>Nested conditionals for barrier detection, string NPC state</td></tr>
    <tr><td>3</td><td>Zone Catch</td><td>Stand in the correct coloured zone for 10 rounds</td><td>Boolean survival check, array of zone objects, Math operators</td></tr>
  </table>
</div>

<div class="callout callout-blue">
  <strong>Controls:</strong> WASD to move &nbsp;·&nbsp; E to interact with the gate &nbsp;·&nbsp; ESC to go to the next level
</div>

<hr>

<h2 id="zonecatch">Zone Catch — My Level (Level 3)</h2>

<p>Zone Catch is the level I designed and wrote from scratch. Every few seconds two coloured circles appear on screen, and a banner tells you which one is safe. You have to get into the right one before the timer hits zero — if you're standing outside it, or in the wrong one, you get eliminated. Survive 10 rounds, or find the golden gate that shows up from Round 6 and press E near it to escape early and win.</p>

<p>Under the hood it runs as a <code>ZoneCatchOverlay</code> class drawn on a separate fixed <code>canvas</code> stacked on top of the game engine's canvas using <code>z-index: 9999</code>. That way I didn't need to touch any engine code — just layered my logic right on top.</p>

<div class="annotation">
  Every property in the constructor is a different data type on purpose. <code>round</code> and <code>totalRounds</code> are Numbers compared each time a round ends. <code>roundActive</code>, <code>won</code>, and <code>gameOver</code> are Booleans that guard every update and draw method. <code>circles</code> is an Array of Objects where each object has a <code>safe</code> boolean telling the survival check which zone the player needs to be in.
</div>

<pre><code><span class="kw">class</span> <span class="cls">ZoneCatchOverlay</span> {
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

<hr>

<h2 id="control">Control Structures</h2>

<!-- ── Iteration ──────────────────────────────────────── -->
<h3>Iteration — <code>for</code>, <code>forEach</code>, <code>while</code> loops</h3>

<p>Loops drive the game's pixel sampling, object processing, and round scheduling. The for loop below is the same pattern used when iterating over <code>samplePoints</code> in the Zone Catch survival check — looping over every offset in an array and accumulating a result.</p>

<pre><code><span class="cm">// for...of — iterates pixel sample points in Zone Catch survival check</span>
<span class="kw">for</span> (<span class="kw">const</span> [dx, dy] <span class="kw">of</span> samplePoints) {
  <span class="kw">const</span> pixel = ctx.<span class="fn">getImageData</span>(cx+dx, cy+dy, <span class="num">1</span>, <span class="num">1</span>).data;
  <span class="kw">if</span> (pixel[<span class="num">3</span>] < <span class="num">30</span>) <span class="kw">continue</span>;
  <span class="kw">const</span> sd = Math.<span class="fn">sqrt</span>((pixel[<span class="num">0</span>]-safeRGB.r)**<span class="num">2</span> + (pixel[<span class="num">1</span>]-safeRGB.g)**<span class="num">2</span>);
  <span class="kw">if</span> (sd < bestSafeDist) bestSafeDist = sd;
}

<span class="cm">// forEach — processing each active cannonball in Level 1</span>
cannonballs.<span class="fn">forEach</span>(ball => {
  ball.x -= ball.speed;
  <span class="kw">if</span> (ball.x + ball.r < <span class="num">0</span>) <span class="fn">resetBall</span>(ball);
});</code></pre>

<h4>Iterations Homework</h4>
<pre><code><span class="cm">// for loop — accumulates sum, same structure as pixel colour accumulation</span>
<span class="kw">function</span> <span class="fn">sumNumbers</span>(n) {
  <span class="kw">let</span> sum = <span class="num">0</span>;
  <span class="kw">for</span> (<span class="kw">let</span> i = <span class="num">1</span>; i <= n; i++) {
    sum += i;
  }
  <span class="kw">return</span> sum;
}
console.<span class="fn">log</span>(<span class="str">"Sum 1 to 5:"</span>, <span class="fn">sumNumbers</span>(<span class="num">5</span>));  <span class="cm">// 15</span>

<span class="cm">// while loop — drains power until zero</span>
<span class="kw">let</span> power = <span class="num">35</span>;
<span class="kw">while</span> (power > <span class="num">0</span>) {
  power -= <span class="num">10</span>;
  <span class="kw">if</span> (power < <span class="num">0</span>) power = <span class="num">0</span>;
}
console.<span class="fn">log</span>(<span class="str">"Power:"</span>, power);  <span class="cm">// 0</span></code></pre>

<!-- ── Conditionals ────────────────────────────────────── -->
<h3>Conditionals — <code>if/else</code>, state transitions</h3>

<p>Every state transition in the game runs through an if/else check. The gate key handler below uses basic conditionals to guard two different requirements before triggering a win — if the key isn't E, return early; if the player is close enough, trigger the win, otherwise log the miss.</p>

<pre><code><span class="cm">// if/else — gate interaction in Zone Catch</span>
<span class="kw">this</span>._gateKeyHandler = (e) => {
  <span class="kw">if</span> (e.key !== <span class="str">'e'</span> && e.key !== <span class="str">'E'</span>) <span class="kw">return</span>;        <span class="cm">// wrong key → do nothing</span>
  <span class="kw">if</span> (!<span class="kw">this</span>.roundActive || !<span class="kw">this</span>.gateVisible) <span class="kw">return</span>; <span class="cm">// wrong state → do nothing</span>

  <span class="kw">const</span> p = <span class="kw">this</span>.<span class="fn">_getPlayerCenter</span>();
  <span class="kw">if</span> (p && <span class="kw">this</span>.<span class="fn">_dist</span>(p.x, p.y, g.x, g.y) < g.r * <span class="num">1.5</span>) {
    <span class="kw">this</span>.<span class="fn">_triggerWin</span>();                                 <span class="cm">// close enough → win</span>
  } <span class="kw">else</span> {
    console.<span class="fn">log</span>(<span class="str">'[ZoneCatch] Too far from gate'</span>);       <span class="cm">// else → miss</span>
  }
};

<span class="cm">// if/else — cannonball reset in Level 1</span>
<span class="kw">if</span> (ball.x + ball.r < <span class="num">0</span>) {
  ball.x     = canvas.width + ball.r;    <span class="cm">// off left → reset to right</span>
  ball.speed = <span class="num">2</span> + Math.<span class="fn">random</span>() * <span class="num">3</span>;
} <span class="kw">else</span> {
  ball.x -= ball.speed;                  <span class="cm">// still on screen → keep moving</span>
}</code></pre>

<h4>Conditionals Homework</h4>
<pre><code><span class="cm">// Grade classifier — if/else chain for state transitions</span>
<span class="kw">function</span> <span class="fn">getGrade</span>(score) {
  <span class="kw">if</span> (score >= <span class="num">90</span>) {
    <span class="kw">return</span> <span class="str">"A"</span>;
  } <span class="kw">else if</span> (score >= <span class="num">80</span>) {
    <span class="kw">return</span> <span class="str">"B"</span>;
  } <span class="kw">else if</span> (score >= <span class="num">70</span>) {
    <span class="kw">return</span> <span class="str">"C"</span>;
  } <span class="kw">else</span> {
    <span class="kw">return</span> <span class="str">"F"</span>;
  }
}
console.<span class="fn">log</span>(<span class="fn">getGrade</span>(<span class="num">85</span>));  <span class="cm">// B</span>
console.<span class="fn">log</span>(<span class="fn">getGrade</span>(<span class="num">72</span>));  <span class="cm">// C</span></code></pre>

<!-- ── Nested Conditions ───────────────────────────────── -->
<h3>Nested Conditions — Complex game logic</h3>

<p>The Zone Catch survival check uses multi-level conditionals — first checking if there are any opaque pixels under the player (are they in any zone?), then checking colour distance to the safe zone, then comparing against the danger zone. Any one of the three failing = eliminated.</p>

<div class="annotation">
  The final check chains three conditions with <code>||</code>: die if there are no coloured pixels under the player (outside both zones), die if the safe colour is too far away (wrong circle), or die if the danger colour is actually closer (still wrong). Three completely different failure modes handled in nested conditionals — power-up + collision + direction all at once.
</div>

<pre><code><span class="cm">// Nested conditions — Zone Catch survival check</span>
<span class="kw">if</span> (!hasOpaquePixel) {
  <span class="cm">// Level 1: not inside any zone at all</span>
  <span class="kw">this</span>.<span class="fn">_triggerDeath</span>();
} <span class="kw">else if</span> (bestSafeDist > <span class="num">80</span>) {
  <span class="cm">// Level 2: inside a zone but not the safe colour</span>
  <span class="kw">this</span>.<span class="fn">_triggerDeath</span>();
} <span class="kw">else if</span> (bestSafeDist >= bestDangerDist) {
  <span class="cm">// Level 3: safe colour is further away than danger colour</span>
  <span class="kw">this</span>.<span class="fn">_triggerDeath</span>();
} <span class="kw">else</span> {
  <span class="kw">this</span>.<span class="fn">_nextRound</span>();
}</code></pre>

<h4>Nested Conditionals Homework</h4>
<pre><code><span class="kw">const</span> factorsOf50 = [<span class="num">1</span>, <span class="num">2</span>, <span class="num">5</span>, <span class="num">10</span>, <span class="num">25</span>, <span class="num">50</span>];

<span class="kw">for</span> (<span class="kw">let</span> i = <span class="num">1</span>; i <= <span class="num">50</span>; i++) {
  <span class="kw">if</span> (i > <span class="num">25</span>) {
    <span class="kw">if</span> (factorsOf50.<span class="fn">includes</span>(i)) {
      console.<span class="fn">log</span>(<span class="str">`${i} is in the upper range and is a factor of 50.`</span>);
    } <span class="kw">else</span> {
      <span class="kw">if</span> (i % <span class="num">3</span> === <span class="num">0</span>) {
        console.<span class="fn">log</span>(<span class="str">`${i} is in the upper range and divisible by 3.`</span>);
      } <span class="kw">else</span> {
        console.<span class="fn">log</span>(<span class="str">`${i} is in the upper range (no match).`</span>);
      }
    }
  } <span class="kw">else</span> {
    <span class="kw">if</span> (factorsOf50.<span class="fn">includes</span>(i)) {
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

<hr>

<h2 id="datatypes">Data Types</h2>

<div class="table-wrap">
  <table>
    <tr><th>Type</th><th>Used For</th><th>Example from the Game</th></tr>
    <tr><td><span class="badge b-orange">Number</span></td><td>Position, velocity, score tracking — round counter, zone radius, timer durations, pixel colour distances.</td><td><code>this.round = 0</code> · <code>baseR = 95 - round * 3</code></td></tr>
    <tr><td><span class="badge b-blue">String</span></td><td>Character names, sprite paths, game states — zone colours as hex strings, HUD labels as template literals, key comparison.</td><td><code>color: '#e63946'</code> · <code>e.key !== 'e'</code></td></tr>
    <tr><td><span class="badge b-red">Boolean</span></td><td>Flags (isJumping, isPaused, isVulnerable) — <code>roundActive</code>, <code>won</code>, <code>gameOver</code> control which screen draws. Each circle has a <code>safe</code> boolean.</td><td><code>this.roundActive = false</code> · <code>safe: safeIdx === 0</code></td></tr>
    <tr><td><span class="badge b-green">Array</span></td><td>Game object collections, level data — <code>this.circles</code> holds zone objects, <code>colorPairs</code> stores colour options, <code>samplePoints</code> holds pixel offsets.</td><td><code>this.circles = []</code> · <code>colorPairs = [['#e63946','#457b9d'],...]</code></td></tr>
    <tr><td><span class="badge b-purple">Object (JSON)</span></td><td>Configuration objects, sprite data — each circle is an object with x, y, r, color, safe. Gate and player position are also objects.</td><td><code>{ x:400, y:300, r:80, color:'#e63946', safe:true }</code></td></tr>
  </table>
</div>

<h3>Numbers — Position, velocity, score tracking</h3>
<p>Numbers are everywhere there's math: zone radius shrinks by 3 each round, the distance formula uses exponentiation, <code>Math.max()</code> prevents zones getting impossibly small:</p>
<pre><code><span class="cm">// Arithmetic on Numbers — zone radius calculation</span>
<span class="kw">const</span> baseR = Math.<span class="fn">max</span>(<span class="num">50</span>, <span class="num">95</span> - <span class="kw">this</span>.round * <span class="num">3</span>);

<span class="cm">// Distance formula — numeric properties x, y used in math</span>
<span class="fn">_dist</span>(ax, ay, bx, by) {
  <span class="kw">return</span> Math.<span class="fn">sqrt</span>((ax - bx) ** <span class="num">2</span> + (ay - by) ** <span class="num">2</span>);
}

<span class="cm">// Round duration decreases 200ms each round, minimum 3800ms</span>
<span class="fn">_roundDuration</span>() {
  <span class="kw">return</span> Math.<span class="fn">max</span>(<span class="num">3800</span>, <span class="kw">this</span>.baseRoundDuration - (<span class="kw">this</span>.round - <span class="num">1</span>) * <span class="num">200</span>);
}</code></pre>

<h3>Strings — Character names, sprite paths, game states</h3>
<p>Zone colours are stored as hex strings and passed to canvas drawing calls. The gate key handler compares <code>e.key</code> to a string. All HUD labels are strings built with template literals:</p>
<pre><code><span class="cm">// String literals — hex colour stored as String</span>
<span class="kw">const</span> colorPairs = [[<span class="str">'#e63946'</span>, <span class="str">'#457b9d'</span>], [<span class="str">'#f4a261'</span>, <span class="str">'#2a9d8f'</span>]];

<span class="cm">// String comparison — gate key check</span>
<span class="kw">if</span> (e.key !== <span class="str">'e'</span> && e.key !== <span class="str">'E'</span>) <span class="kw">return</span>;

<span class="cm">// Template literal — HUD text built from Numbers + Strings</span>
ctx.fillText(<span class="str">`Round ${<span class="kw">this</span>.round} / ${<span class="kw">this</span>.totalRounds}`</span>, x, y);</code></pre>

<h4>Strings Homework</h4>
<pre><code><span class="kw">let</span> str1 = <span class="str">"Homework"</span>, str2 = <span class="str">"JavaScript is fun"</span>, str3 = <span class="str">"I like coding"</span>;
console.<span class="fn">log</span>(<span class="str">`Length of str1: ${str1.length}`</span>);
console.<span class="fn">log</span>(<span class="str">`str1 — first: ${str1[0]}, last: ${str1[str1.length - 1]}`</span>);
<span class="kw">let</span> sentence = <span class="str">`${str1}: ${str2}. ${str3}!`</span>;
console.<span class="fn">log</span>(sentence);</code></pre>

<h3>Booleans — Flags (isJumping, isPaused, isVulnerable)</h3>
<p>Every state flag in the game is a boolean. <code>roundActive</code> guards the update and draw loops — nothing runs if it's false. Each circle object carries a <code>safe</code> boolean set at spawn time using a strict equality check:</p>
<pre><code><span class="cm">// Boolean flag — guards entire game loop</span>
<span class="kw">if</span> (!<span class="kw">this</span>.roundActive || <span class="kw">this</span>.gameOver) <span class="kw">return</span>;

<span class="cm">// Boolean from expression — set at circle spawn</span>
<span class="kw">const</span> safeIdx = Math.<span class="fn">round</span>(Math.<span class="fn">random</span>());
<span class="kw">this</span>.circles = [
  { color: shuffled[<span class="num">0</span>], safe: safeIdx === <span class="num">0</span> },  <span class="cm">// evaluates to Boolean</span>
  { color: shuffled[<span class="num">1</span>], safe: safeIdx === <span class="num">1</span> },
];</code></pre>

<h3>Arrays — Game object collections, level data</h3>
<p><code>this.circles</code> holds the two zone objects each round. <code>colorPairs</code> stores the available colour combinations. <code>samplePoints</code> is an array of pixel offsets looped over in the survival check:</p>
<pre><code><span class="cm">// Array of Objects — the two zones spawned each round</span>
<span class="kw">this</span>.circles = [
  { x: x0, y: y0, r: baseR, color: shuffled[<span class="num">0</span>], safe: <span class="bool">true</span>  },
  { x: x1, y: y1, r: baseR, color: shuffled[<span class="num">1</span>], safe: <span class="bool">false</span> },
];

<span class="cm">// Array of offsets — iterated in pixel survival check</span>
<span class="kw">const</span> samplePoints = [[<span class="num">0</span>,<span class="num">0</span>],[<span class="num">-8</span>,<span class="num">0</span>],[<span class="num">8</span>,<span class="num">0</span>],[<span class="num">0</span>,<span class="num">-8</span>],[<span class="num">0</span>,<span class="num">8</span>]];</code></pre>

<h4>Arrays Homework</h4>
<pre><code><span class="kw">const</span> myGames = [<span class="str">"COD"</span>, <span class="str">"Minecraft"</span>, <span class="str">"Forza"</span>, <span class="str">"Clash"</span>, <span class="str">"Roblox"</span>];
console.<span class="fn">log</span>(<span class="str">"First:"</span>, myGames[<span class="num">0</span>]);
console.<span class="fn">log</span>(<span class="str">"Last:"</span>,  myGames[myGames.length - <span class="num">1</span>]);

<span class="kw">let</span> shoppingList = [<span class="str">"milk"</span>, <span class="str">"eggs"</span>, <span class="str">"bread"</span>, <span class="str">"cheese"</span>];
shoppingList[<span class="num">1</span>] = <span class="str">"butter"</span>;
shoppingList.<span class="fn">push</span>(<span class="str">"yogurt"</span>);
shoppingList.<span class="fn">splice</span>(<span class="num">2</span>, <span class="num">1</span>);

<span class="kw">const</span> numbers = [<span class="num">10</span>, <span class="num">25</span>, <span class="num">30</span>, <span class="num">15</span>, <span class="num">20</span>];
<span class="kw">let</span> sum = <span class="num">0</span>;
<span class="kw">for</span> (<span class="kw">let</span> i = <span class="num">0</span>; i < numbers.length; i++) { sum += numbers[i]; }
console.<span class="fn">log</span>(<span class="str">"Total:"</span>, sum);</code></pre>

<h3>Objects (JSON) — Configuration objects, sprite data</h3>
<p>Each zone circle is a configuration object. Sprite hitbox data comes in as a nested object from the engine's JSON config — read with optional chaining and a nullish fallback:</p>
<pre><code><span class="cm">// Object literal — zone configuration</span>
<span class="kw">const</span> gate = { x: gx, y: gy, r: <span class="num">30</span>, alpha: <span class="num">1.0</span>, visible: <span class="bool">true</span> };

<span class="cm">// Nested object access — sprite config from JSON</span>
<span class="kw">const</span> hbW = player.spriteData?.hitbox?.widthPercentage ?? <span class="num">0.4</span>;</code></pre>

<h4>JSON Homework</h4>
<pre><code><span class="kw">const</span> resume = {
  fullName:  <span class="str">"Kash Tubati"</span>,
  email:     <span class="str">"kash.tubati@gmail.com"</span>,
  education: <span class="str">"9th Grade"</span>,
  address:   { city: <span class="str">"San Diego"</span>, state: <span class="str">"California"</span>, country: <span class="str">"USA"</span> },
  skills:    [<span class="str">"JavaScript"</span>, <span class="str">"Python"</span>, <span class="str">"Problem Solving"</span>, <span class="str">"Debugging"</span>]
};
console.<span class="fn">log</span>(<span class="str">"City: "</span> + resume.address.city);
<span class="kw">let</span> jsonString   = JSON.<span class="fn">stringify</span>(resume);
<span class="kw">let</span> parsedResume = JSON.<span class="fn">parse</span>(jsonString);
console.<span class="fn">log</span>(parsedResume);</code></pre>

<hr>

<h2 id="operators">Operators</h2>

<div class="table-wrap">
  <table>
    <tr><th>Type</th><th>Operators Used</th><th>What They Do in the Game</th></tr>
    <tr><td>Mathematical</td><td><code>+</code> <code>-</code> <code>*</code> <code>/</code> <code>**</code> <code>%</code> <code>Math.sqrt()</code> <code>Math.max()</code></td><td>Physics: <code>95 - round * 3</code> shrinks zones. <code>(ax-bx)**2</code> is the distance formula. <code>Math.max(50, ...)</code> enforces a minimum radius.</td></tr>
    <tr><td>String Operations</td><td>Template literals <code>`${}`</code>, concatenation <code>+</code>, <code>.length</code>, indexing <code>[i]</code></td><td>Path concatenation for sprite images. <code>`Round ${round}`</code> builds HUD text. Hex string indexing in colour parsing.</td></tr>
    <tr><td>Boolean Expressions</td><td><code>&&</code> <code>||</code> <code>!</code> <code>===</code> <code>!==</code> <code>&lt;</code> <code>&gt;=</code></td><td>Compound conditions: <code>!roundActive || !gateVisible</code> short-circuits the gate check. <code>bestSafeDist >= bestDangerDist</code> catches the wrong zone.</td></tr>
  </table>
</div>

<h3>Mathematical — Physics calculations (gravity, velocity, collision)</h3>
<p>Every movement, collision, and sizing calculation runs on mathematical operators. Zone radius shrinks by 3px per round; the distance formula uses exponentiation and square root; <code>Math.random()</code> positions zones unpredictably each round:</p>
<pre><code><span class="cm">// Arithmetic — zone sizing with + - *</span>
<span class="kw">const</span> baseR  = Math.<span class="fn">max</span>(<span class="num">50</span>, <span class="num">95</span> - <span class="kw">this</span>.round * <span class="num">3</span>);
<span class="kw">const</span> margin = baseR + <span class="num">16</span>;

<span class="cm">// ** and / — distance formula (physics collision)</span>
<span class="fn">_dist</span>(ax, ay, bx, by) {
  <span class="kw">return</span> Math.<span class="fn">sqrt</span>((ax - bx) ** <span class="num">2</span> + (ay - by) ** <span class="num">2</span>);
}

<span class="cm">// % — modulo used for wrapping round index into colorPairs</span>
<span class="kw">const</span> pair = <span class="kw">this</span>.colorPairs[<span class="kw">this</span>.round % <span class="kw">this</span>.colorPairs.length];</code></pre>

<h4>Mathematical Expressions Homework</h4>
<pre><code><span class="cm">// Modulo — divisibility check</span>
<span class="kw">let</span> y = <span class="num">17</span>;
<span class="kw">let</span> remainder = y % <span class="num">5</span>;
<span class="kw">if</span> (remainder === <span class="num">0</span>) {
  console.<span class="fn">log</span>(y + <span class="str">" is divisible by 5."</span>);
} <span class="kw">else</span> {
  console.<span class="fn">log</span>(y + <span class="str">" is NOT divisible by 5. Remainder: "</span> + remainder);
}
<span class="kw">let</span> a = <span class="num">15</span>, b = <span class="num">25</span>;
console.<span class="fn">log</span>(<span class="str">"Total: "</span> + (a + b));</code></pre>

<h3>String Operations — Path concatenation, text display</h3>
<p>Template literals build every piece of HUD text. Sprite image paths are concatenated strings. The hex colour string is parsed character-by-character when converting to RGB for the pixel comparison:</p>
<pre><code><span class="cm">// Template literal — HUD display</span>
ctx.fillText(<span class="str">`Round ${<span class="kw">this</span>.round} / ${<span class="kw">this</span>.totalRounds}`</span>, x, y);
ctx.fillText(<span class="str">`Safe zone: ${safeColor}`</span>, x, y + <span class="num">30</span>);

<span class="cm">// Concatenation — sprite path building</span>
<span class="kw">const</span> spritePath = baseURL + <span class="str">'images/'</span> + spriteName + <span class="str">'.png'</span>;

<span class="cm">// String indexing — hex colour parsing for pixel comparison</span>
<span class="fn">_hexToRgb</span>(hex) {
  <span class="kw">const</span> m = <span class="str">/^#([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i</span>.<span class="fn">exec</span>(hex);
  <span class="kw">return</span> m ? { r: <span class="fn">parseInt</span>(m[<span class="num">1</span>],<span class="num">16</span>), g: <span class="fn">parseInt</span>(m[<span class="num">2</span>],<span class="num">16</span>), b: <span class="fn">parseInt</span>(m[<span class="num">3</span>],<span class="num">16</span>) } : <span class="bool">null</span>;
}</code></pre>

<h4>String Operations Homework</h4>
<pre><code><span class="kw">let</span> str1 = <span class="str">"Homework"</span>, str2 = <span class="str">"JavaScript is fun"</span>;

<span class="cm">// .length and indexing</span>
console.<span class="fn">log</span>(<span class="str">`Length: ${str1.length}`</span>);
console.<span class="fn">log</span>(<span class="str">`First: ${str1[0]}, Last: ${str1[str1.length - 1]}`</span>);

<span class="cm">// Template literal — same pattern as all game HUD text</span>
<span class="kw">let</span> display = <span class="str">`${str1}: ${str2}!`</span>;
console.<span class="fn">log</span>(display);

<span class="cm">// Concatenation — path building</span>
<span class="kw">let</span> path = <span class="str">"images/"</span> + <span class="str">"player"</span> + <span class="str">".png"</span>;
console.<span class="fn">log</span>(path);  <span class="cm">// images/player.png</span></code></pre>

<h3>Boolean Expressions — Compound conditions in game logic</h3>
<p>Boolean expressions with <code>&&</code>, <code>||</code>, and <code>!</code> guard every state transition. The gate check short-circuits with <code>||</code> so the distance calculation never runs unless both flags pass. The survival check uses <code>>=</code> to compare colour distances:</p>
<pre><code><span class="cm">// && — both conditions must be true</span>
<span class="kw">if</span> (<span class="kw">this</span>.roundActive && <span class="kw">this</span>.gateVisible) {
  <span class="kw">this</span>.<span class="fn">_drawGate</span>();
}

<span class="cm">// || — any one failing triggers early return</span>
<span class="kw">if</span> (!<span class="kw">this</span>.roundActive || !<span class="kw">this</span>.gateVisible) <span class="kw">return</span>;

<span class="cm">// Compound boolean expression — survival check</span>
<span class="kw">if</span> (!hasOpaquePixel || bestSafeDist > <span class="num">80</span> || bestSafeDist >= bestDangerDist) {
  <span class="kw">this</span>.<span class="fn">_triggerDeath</span>();
}</code></pre>

<h4>Boolean Expressions Homework</h4>
<pre><code><span class="cm">// && — both must be true</span>
<span class="kw">function</span> <span class="fn">isPositiveAndEven</span>(num) {
  <span class="kw">let</span> isPositive = num > <span class="num">0</span>;
  <span class="kw">let</span> isEven     = num % <span class="num">2</span> === <span class="num">0</span>;
  <span class="kw">return</span> isPositive && isEven;
}
console.<span class="fn">log</span>(<span class="fn">isPositiveAndEven</span>(<span class="num">8</span>));   <span class="cm">// true</span>
console.<span class="fn">log</span>(<span class="fn">isPositiveAndEven</span>(-<span class="num">4</span>));  <span class="cm">// false</span>

<span class="cm">// || and ! — at least one true, or negation</span>
<span class="kw">function</span> <span class="fn">canPass</span>(hasTicket, isMember) {
  <span class="kw">return</span> hasTicket || isMember;
}
console.<span class="fn">log</span>(<span class="fn">canPass</span>(<span class="bool">false</span>, <span class="bool">true</span>));    <span class="cm">// true</span>
console.<span class="fn">log</span>(!<span class="fn">canPass</span>(<span class="bool">false</span>, <span class="bool">false</span>));  <span class="cm">// true — negated</span></code></pre>

<hr>

<h2 id="other-games">Other Games My Team Built</h2>

<p>On top of the three levels I made, my teammates built some other games that hit the same CS111 concepts from different directions:</p>

<div class="callout callout-blue">
  <strong>How they connect:</strong> Pong demonstrates OOP classes (Paddle, Ball, Renderer), physics math operators for velocity and collision, boolean game-state flags, and iteration via <code>requestAnimationFrame</code>. Connect 4 uses timer-driven state transitions (booleans + iteration). Blackjack uses arrays for the deck, nested conditionals for hand evaluation, and mathematical expressions for card values and betting.
</div>

<h3>Blackjack</h3>
<p>Blackjack is embedded live below — it demonstrates arrays (deck shuffling and hand management), nested conditionals (ace value switching, win/loss/tie logic), mathematical expressions (hand totalling, betting), and strings (card suit and value display). Each round auto-bets $10:</p>

<div style="margin: 24px 0;">
  <div id="bj-menu" style="text-align:center; padding: 32px; background:#2a1a0c; border:1px solid #5a3920; border-radius:8px;">
    <h2 style="color:#faf4e8; font-family:'Playfair Display',serif; font-style:italic; margin-bottom:16px;">Blackjack</h2>
    <button onclick="bjStartGame()" style="padding:10px 22px; margin:8px; font-size:15px; background:#c8832a; color:#faf4e8; border:1px solid #5a3920; border-radius:4px; cursor:pointer; font-family:'Lora',serif;">Play Game</button>
    <button onclick="bjShowHowTo()" style="padding:10px 22px; margin:8px; font-size:15px; background:#3d2710; color:#e8d5b7; border:1px solid #5a3920; border-radius:4px; cursor:pointer; font-family:'Lora',serif;">How to Play</button>
  </div>

  <div id="bj-how-to" style="display:none; text-align:center; padding:32px; background:#2a1a0c; border:1px solid #5a3920; border-radius:8px; color:#e8d5b7; font-family:'Lora',serif;">
    <h2 style="color:#faf4e8; font-family:'Playfair Display',serif; font-style:italic; margin-bottom:12px;">How to Play</h2>
    <p style="margin-bottom:8px;">Get as close to 21 as possible without going over.</p>
    <p style="margin-bottom:8px;">Face cards = 10 &nbsp;·&nbsp; Aces = 1 or 11.</p>
    <p style="margin-bottom:16px;">Dealer hits on 16. Each round bets $10 automatically.</p>
    <button onclick="bjGoBack()" style="padding:10px 22px; font-size:15px; background:#c8832a; color:#faf4e8; border:1px solid #5a3920; border-radius:4px; cursor:pointer; font-family:'Lora',serif;">Back</button>
  </div>

  <div id="bj-game-container" style="display:none; background:#2a1a0c; border:1px solid #5a3920; border-radius:8px; padding:24px; font-family:'Lora',serif; color:#e8d5b7;">
    <h2 style="color:#faf4e8; font-family:'Playfair Display',serif; font-style:italic; text-align:center; margin-bottom:4px;">Blackjack</h2>
    <p style="text-align:center; color:#9c7450; font-size:13px; margin-bottom:20px;">Dealer hits on 16</p>

    <div style="margin-bottom:20px;">
      <h3 style="color:#c8832a; font-family:'Playfair Display',serif; font-style:italic;">Dealer's Hand: <span id="bj-dealer-score" style="color:#faf4e8;">0</span></h3>
      <div style="display:flex; flex-direction:column; align-items:center;">
        <div id="bj-dealer-cards" style="display:flex; justify-content:center; min-height:120px; flex-wrap:wrap;"></div>
        <div id="bj-dealer-points" style="font-size:14px; color:#9c7450; margin-top:4px;"></div>
      </div>
    </div>

    <div style="margin-bottom:20px;">
      <h3 style="color:#c8832a; font-family:'Playfair Display',serif; font-style:italic;">Your Hand: <span id="bj-player-score" style="color:#faf4e8;">0</span></h3>
      <div style="display:flex; flex-direction:column; align-items:center;">
        <div id="bj-player-cards" style="display:flex; justify-content:center; min-height:120px; flex-wrap:wrap;"></div>
        <div id="bj-player-points" style="font-size:14px; color:#9c7450; margin-top:4px;"></div>
      </div>
    </div>

    <div style="text-align:center; margin-bottom:12px;">
      <button id="bj-new-game-btn" style="padding:10px 20px; margin:6px; font-size:15px; background:#3d2710; color:#e8d5b7; border:1px solid #5a3920; border-radius:4px; cursor:pointer; font-family:'Lora',serif;">New Round</button>
      <button id="bj-hit-btn" style="padding:10px 20px; margin:6px; font-size:15px; background:#c8832a; color:#faf4e8; border:1px solid #5a3920; border-radius:4px; cursor:pointer; font-family:'Lora',serif;">Hit</button>
      <button id="bj-stand-btn" style="padding:10px 20px; margin:6px; font-size:15px; background:#c8832a; color:#faf4e8; border:1px solid #5a3920; border-radius:4px; cursor:pointer; font-family:'Lora',serif;">Stand</button>
    </div>

    <div style="text-align:center; margin-bottom:12px;">
      <span style="color:#d4a030; font-weight:bold; font-size:15px;">💰 Balance: $<span id="bj-money">100</span> &nbsp;·&nbsp; Bet: $<span id="bj-bet-display">0</span></span>
    </div>

    <p id="bj-message" style="text-align:center; font-weight:bold; color:#faf4e8; font-size:16px; min-height:24px;"></p>
  </div>
</div>

<style>
  .bj-card {
    width: 72px; height: 100px; border: 1px solid #5a3920; border-radius: 6px;
    margin: 5px; display: flex; justify-content: center; align-items: center;
    font-size: 22px; font-weight: bold; background: #faf4e8;
    box-shadow: 2px 2px 6px rgba(0,0,0,0.4);
  }
</style>

<script>
(function(){
  let bjDeck=[], bjPlayerHand=[], bjDealerHand=[], bjGameOver=false;
  let bjMoney=100, bjBet=0;

  function bjStartGame(){
    document.getElementById('bj-menu').style.display='none';
    document.getElementById('bj-game-container').style.display='block';
    bjNewGame();
  }
  function bjShowHowTo(){document.getElementById('bj-menu').style.display='none';document.getElementById('bj-how-to').style.display='block';}
  function bjGoBack(){document.getElementById('bj-how-to').style.display='none';document.getElementById('bj-menu').style.display='block';}
  window.bjStartGame=bjStartGame; window.bjShowHowTo=bjShowHowTo; window.bjGoBack=bjGoBack;

  function bjCreateDeck(){
    const suits=["♠","♥","♦","♣"], values=["A","2","3","4","5","6","7","8","9","10","J","Q","K"];
    let d=[];
    for(let s of suits) for(let v of values) d.push({value:v,suit:s});
    return bjShuffle(d);
  }
  function bjShuffle(d){
    for(let i=d.length-1;i>0;i--){let j=Math.floor(Math.random()*(i+1));[d[i],d[j]]=[d[j],d[i]];}
    return d;
  }
  function bjCardValue(c){if(["J","Q","K"].includes(c.value))return 10;if(c.value==="A")return 11;return parseInt(c.value);}
  function bjCalcHand(hand){let v=0,aces=0;for(let c of hand){v+=bjCardValue(c);if(c.value==="A")aces++;}while(v>21&&aces>0){v-=10;aces--;}return v;}

  function bjMakeCard(c,hidden=false){
    const el=document.createElement('div');el.className='bj-card';
    if(hidden){el.textContent='🂠';el.style.color='#2a1a0c';}
    else{el.textContent=c.value+c.suit;el.style.color=(c.suit==="♥"||c.suit==="♦")?"#b91c1c":"#120b05";}
    return el;
  }

  function bjRenderHand(hand,container,pointsEl){
    container.innerHTML='';
    for(let c of hand)container.appendChild(bjMakeCard(c));
    pointsEl.textContent='Total: '+bjCalcHand(hand);
  }

  function bjRenderDealerInitial(){
    const dc=document.getElementById('bj-dealer-cards');
    dc.innerHTML='';
    dc.appendChild(bjMakeCard(bjDealerHand[0]));
    dc.appendChild(bjMakeCard(null,true));
    document.getElementById('bj-dealer-points').textContent='Showing: '+bjCardValue(bjDealerHand[0]);
  }

  function bjUpdateMoney(){
    document.getElementById('bj-money').textContent=bjMoney;
    document.getElementById('bj-bet-display').textContent=bjBet;
  }

  function bjNewGame(){
    if(bjMoney<=0){document.getElementById('bj-message').textContent="You're out of money! Refresh the page to restart.";return;}
    bjBet=Math.min(10,bjMoney);
    bjDeck=bjCreateDeck();
    bjPlayerHand=[bjDeck.pop(),bjDeck.pop()];
    bjDealerHand=[bjDeck.pop(),bjDeck.pop()];
    bjGameOver=false;
    bjRenderHand(bjPlayerHand,document.getElementById('bj-player-cards'),document.getElementById('bj-player-points'));
    bjRenderDealerInitial();
    document.getElementById('bj-dealer-score').textContent=bjCardValue(bjDealerHand[0]);
    document.getElementById('bj-player-score').textContent=bjCalcHand(bjPlayerHand);
    document.getElementById('bj-message').textContent='Bet: $'+bjBet+' — Your move.';
    bjUpdateMoney();
  }

  function bjHit(){
    if(bjGameOver)return;
    bjPlayerHand.push(bjDeck.pop());
    bjRenderHand(bjPlayerHand,document.getElementById('bj-player-cards'),document.getElementById('bj-player-points'));
    document.getElementById('bj-player-score').textContent=bjCalcHand(bjPlayerHand);
    if(bjCalcHand(bjPlayerHand)>21)bjEndRound('lose');
  }

  function bjStand(){
    if(bjGameOver)return;
    bjRenderHand(bjDealerHand,document.getElementById('bj-dealer-cards'),document.getElementById('bj-dealer-points'));
    while(bjCalcHand(bjDealerHand)<17){bjDealerHand.push(bjDeck.pop());}
    bjRenderHand(bjDealerHand,document.getElementById('bj-dealer-cards'),document.getElementById('bj-dealer-points'));
    document.getElementById('bj-dealer-score').textContent=bjCalcHand(bjDealerHand);
    document.getElementById('bj-player-score').textContent=bjCalcHand(bjPlayerHand);
    const pv=bjCalcHand(bjPlayerHand),dv=bjCalcHand(bjDealerHand);
    if((pv>dv&&pv<=21)||dv>21)bjEndRound('win');
    else if(dv>pv&&dv<=21)bjEndRound('lose');
    else bjEndRound('tie');
  }

  function bjEndRound(result){
    bjGameOver=true;
    const msg=document.getElementById('bj-message');
    if(result==='win'){bjMoney+=bjBet;msg.textContent='You win! +$'+bjBet+' — Balance: $'+bjMoney;}
    else if(result==='lose'){bjMoney-=bjBet;msg.textContent='Dealer wins. -$'+bjBet+' — Balance: $'+bjMoney;}
    else{msg.textContent="Push — it's a tie. Balance: $"+bjMoney;}
    bjUpdateMoney();
  }

  document.getElementById('bj-new-game-btn').addEventListener('click',bjNewGame);
  document.getElementById('bj-hit-btn').addEventListener('click',bjHit);
  document.getElementById('bj-stand-btn').addEventListener('click',bjStand);
})();
</script>

<h3>Pong</h3>
<p>Pong is embedded live below — it demonstrates OOP (separate <code>Paddle</code>, <code>Ball</code>, <code>Renderer</code>, and <code>Game</code> classes), mathematical operators for physics (velocity, spin, collision), boolean flags for game state, and a <code>requestAnimationFrame</code> loop for smooth animation. Choose PvP or AI mode:</p>

<div style="margin: 24px 0; text-align: center;">
  <div style="margin-bottom:12px;">
    <button id="pongStartPvP" style="margin-right:8px; padding:8px 16px; font-size:15px; background:#c8832a; color:#faf4e8; border:1px solid #5a3920; border-radius:4px; cursor:pointer; font-family:'Lora',serif; letter-spacing:1px;">Start PvP</button>
    <button id="pongStartAI"  style="padding:8px 16px; font-size:15px; background:#c8832a; color:#faf4e8; border:1px solid #5a3920; border-radius:4px; cursor:pointer; font-family:'Lora',serif; letter-spacing:1px;">Start AI</button>
  </div>
  <canvas id="pongCanvas" width="800" height="500" style="border:2px solid #5a3920; background:#000; max-width:100%;"></canvas>
  <br>
  <button id="pongRestartBtn" style="display:none; margin-top:15px; padding:10px 20px; font-size:16px; border:none; border-radius:6px; background:#c8832a; color:#faf4e8; cursor:pointer; font-family:'Lora',serif;">Restart Game</button>
</div>

<script>
(function() {
const PongConfig = {
  canvas: { width: 800, height: 500 },
  paddle: { width: 10, height: 100, speed: 10.5 },
  ball: { radius: 10, baseSpeedX: 5, maxRandomY: 2, spinFactor: 0.3, maxSpeed: 15 },
  powerUp: { spawnMinSec: 6, spawnMaxSec: 14, width: 28, height: 14, durationSec: 6, colors: { bg: '#ffdd57', border: '#ffaa00' } },
  bumper: { enabledAtScore: 9, radius: 40, color: "#ed1111ff" },
  rules: { winningScore: 11 },
  keys: { p1Up: "w", p1Down: "s", p2Up: "ArrowUp", p2Down: "ArrowDown" },
  visuals: { bg: "#000", fg: "#fff", text: "#fff", gameOver: "red", win: "yellow" }
};

class PVector2 { constructor(x=0,y=0){this.x=x;this.y=y;} }

class PPaddle {
  constructor(x,y,w,h,speed,bh){this.position=new PVector2(x,y);this.width=w;this.height=h;this.speed=speed;this.boundsHeight=bh;}
  move(dy){this.position.y=Math.min(this.boundsHeight-this.height,Math.max(0,this.position.y+dy));}
  rect(){return{x:this.position.x,y:this.position.y,w:this.width,h:this.height};}
}

class PBall {
  constructor(radius,bw,bh){this.radius=radius;this.boundsWidth=bw;this.boundsHeight=bh;this.position=new PVector2();this.velocity=new PVector2();this.reset(true);}
  reset(rand=false){
    this.position.x=this.boundsWidth/2;this.position.y=this.boundsHeight/2;
    const dir=rand&&Math.random()>0.5?1:-1;
    this.velocity.x=dir*PongConfig.ball.baseSpeedX;
    this.velocity.y=(Math.random()*(2*PongConfig.ball.maxRandomY))-PongConfig.ball.maxRandomY;
  }
  update(){
    this.position.x+=this.velocity.x;this.position.y+=this.velocity.y;
    if(this.position.y+this.radius>this.boundsHeight||this.position.y-this.radius<0)this.velocity.y*=-1;
  }
}

class PInput {
  constructor(){this.keys={};
    document.addEventListener("keydown",e=>{if(["ArrowUp","ArrowDown"," ","Spacebar"].includes(e.key))e.preventDefault();this.keys[e.key]=true;});
    document.addEventListener("keyup",e=>{this.keys[e.key]=false;});
  }
  isDown(k){return!!this.keys[k];}
}

class PRenderer {
  constructor(ctx){this.ctx=ctx;}
  clear(w,h){this.ctx.fillStyle=PongConfig.visuals.bg;this.ctx.fillRect(0,0,w,h);}
  rect(r,color=PongConfig.visuals.fg){this.ctx.fillStyle=color;this.ctx.fillRect(r.x,r.y,r.w,r.h);}
  circle(ball,color=PongConfig.visuals.fg){this.ctx.fillStyle=color;this.ctx.beginPath();this.ctx.arc(ball.position.x,ball.position.y,ball.radius,0,Math.PI*2);this.ctx.closePath();this.ctx.fill();}
  text(t,x,y,color=PongConfig.visuals.text){this.ctx.fillStyle=color;this.ctx.font="30px Arial";this.ctx.fillText(t,x,y);}
}

class PongGame {
  constructor(canvasEl,restartBtn,opts={}){
    this.canvas=canvasEl;this.ctx=canvasEl.getContext('2d');this.renderer=new PRenderer(this.ctx);this.ai=!!opts.ai;
    this.input=new PInput();
    const{width,height,speed}=PongConfig.paddle;
    this.paddleLeft=new PPaddle(0,(PongConfig.canvas.height-height)/2,width,height,speed,PongConfig.canvas.height);
    this.paddleRight=new PPaddle(PongConfig.canvas.width-width,(PongConfig.canvas.height-height)/2,width,height,speed,PongConfig.canvas.height);
    this.balls=[new PBall(PongConfig.ball.radius,PongConfig.canvas.width,PongConfig.canvas.height)];
    this.multiTriggered={p1:0,p2:0};
    this.scores={p1:0,p2:0};
    this.gameOver=false;this.restartBtn=restartBtn;this.paused=false;this.audioCtx=null;
    this.powerUp=null;this.nextPowerUpAt=performance.now()+this.randRange(PongConfig.powerUp.spawnMinSec*1000,PongConfig.powerUp.spawnMaxSec*1000);
    this.activeEffects={left:null,right:null};this.replayCountdown=null;
    this.restartBtn.addEventListener("click",()=>this.restart());
    document.addEventListener('keydown',(e)=>{if(e.key===' '||e.key==='Spacebar'){e.preventDefault();this.togglePause();}});
    this.loop=this.loop.bind(this);
  }
  randRange(min,max){return Math.random()*(max-min)+min;}
  togglePause(){this.paused=!this.paused;if(!this.paused)this.loop();}
  handleInput(){
    if(this.gameOver)return;
    if(this.input.isDown(PongConfig.keys.p1Up))this.paddleLeft.move(-this.paddleLeft.speed);
    if(this.input.isDown(PongConfig.keys.p1Down))this.paddleLeft.move(this.paddleLeft.speed);
    if(this.ai){this.updateAI();}else{
      if(this.input.isDown(PongConfig.keys.p2Up))this.paddleRight.move(-this.paddleRight.speed);
      if(this.input.isDown(PongConfig.keys.p2Down))this.paddleRight.move(this.paddleRight.speed);
    }
  }
  updateAI(){
    if(!this.balls||!this.balls.length)return;
    const mid=PongConfig.canvas.width/2;
    const candidates=this.balls.filter(b=>b.position.x>=mid);
    if(!candidates.length)return;
    let target=candidates[0],bestDist=Math.abs(target.position.y-(this.paddleRight.position.y+this.paddleRight.height/2));
    for(let i=1;i<candidates.length;i++){const d=Math.abs(candidates[i].position.y-(this.paddleRight.position.y+this.paddleRight.height/2));if(d<bestDist){target=candidates[i];bestDist=d;}}
    const centerY=this.paddleRight.position.y+this.paddleRight.height/2;
    const diff=target.position.y-centerY;
    if(Math.abs(diff)<=6)return;
    this.paddleRight.move((diff>0?1:-1)*this.paddleRight.speed*0.9);
  }
  capBallSpeedFor(ball){
    if(!ball||!ball.velocity)return;
    const max=PongConfig.ball.maxSpeed,vx=ball.velocity.x||0,vy=ball.velocity.y||0;
    const speed=Math.sqrt(vx*vx+vy*vy);
    if(speed>max&&speed>0){const s=max/speed;ball.velocity.x=vx*s;ball.velocity.y=vy*s;}
  }
  _ballHitsRect(ball,rect){
    const bx=ball.position.x,by=ball.position.y;
    const left=rect.x-(rect.w/2),top=rect.y-(rect.h/2),right=rect.x+(rect.w/2),bottom=rect.y+(rect.h/2);
    const cx=Math.max(left,Math.min(bx,right)),cy=Math.max(top,Math.min(by,bottom));
    const dx=bx-cx,dy=by-cy;return(dx*dx+dy*dy)<=(ball.radius*ball.radius);
  }
  _applyPowerUp(type,side){
    const now=performance.now(),dur=PongConfig.powerUp.durationSec*1000;
    if(type===1){const p=side==='left'?this.paddleLeft:this.paddleRight;p.height=Math.min(PongConfig.canvas.height,PongConfig.paddle.height*1.6);this.activeEffects[side]={type:'big',until:now+dur};}
    else if(type===2){const factor=1.6;for(const b of this.balls){b.velocity.x*=factor;b.velocity.y*=factor;}this.activeEffects[side]={type:'ball_fast',until:now+dur,factor};}
    else if(type===3){const other=side==='left'?'right':'left';const p=other==='left'?this.paddleLeft:this.paddleRight;p.height=Math.min(PongConfig.canvas.height,PongConfig.paddle.height*1.6);this.activeEffects[other]={type:'big_opponent',until:now+dur};}
  }
  _ensureAudio(){if(this.audioCtx)return;const A=window.AudioContext||window.webkitAudioContext;if(!A)return;this.audioCtx=new A();}
  playScoreSound(player){
    this._ensureAudio();if(!this.audioCtx)return;
    try{const ctx=this.audioCtx,o=ctx.createOscillator(),g=ctx.createGain();o.type='sine';o.frequency.value=player==='p1'?880:440;g.gain.value=0.0001;o.connect(g);g.connect(ctx.destination);const now=ctx.currentTime;g.gain.setValueAtTime(0.0001,now);g.gain.linearRampToValueAtTime(0.18,now+0.01);o.start(now);g.gain.linearRampToValueAtTime(0.0001,now+0.18);o.stop(now+0.2);}catch(e){}
  }
  update(){
    if(this.gameOver)return;
    for(const b of this.balls)b.update();
    const now=performance.now();
    if(!this.powerUp&&now>=this.nextPowerUpAt){
      const margin=60;
      this.powerUp={x:this.randRange(margin,PongConfig.canvas.width-margin),y:this.randRange(margin,PongConfig.canvas.height-margin),w:PongConfig.powerUp.width,h:PongConfig.powerUp.height,type:Math.floor(Math.random()*3)+1,spawnedAt:now};
      this.nextPowerUpAt=now+this.randRange(PongConfig.powerUp.spawnMinSec*1000,PongConfig.powerUp.spawnMaxSec*1000);
    }
    if(this.powerUp){for(const b of this.balls){if(this._ballHitsRect(b,this.powerUp)){const hitter=b.lastHit||(b.velocity.x>0?'p1':'p2');this._applyPowerUp(this.powerUp.type,hitter==='p1'?'left':'right');this.powerUp=null;break;}}}
    for(const side of['left','right']){const eff=this.activeEffects[side];if(eff&&eff.until&&now>=eff.until){if(eff.type==='big'){(side==='left'?this.paddleLeft:this.paddleRight).height=PongConfig.paddle.height;}else if(eff.type==='big_opponent'){(side==='left'?this.paddleRight:this.paddleLeft).height=PongConfig.paddle.height;}else if(eff.type==='ball_fast'){const f=eff.factor||1.6;for(const bb of this.balls){bb.velocity.x/=f;bb.velocity.y/=f;}}this.activeEffects[side]=null;}}
    const bumperActive=(this.scores.p1+this.scores.p2)>=PongConfig.bumper.enabledAtScore;
    if(bumperActive){const cx=PongConfig.canvas.width/2,cy=PongConfig.canvas.height/2,br=PongConfig.bumper.radius;for(const b of this.balls){const dx=b.position.x-cx,dy=b.position.y-cy,dist=Math.sqrt(dx*dx+dy*dy),minDist=br+b.radius;if(dist<=minDist){const inv=dist===0?1:1/dist,nx=dx*inv,ny=dy*inv,vdotn=b.velocity.x*nx+b.velocity.y*ny;b.velocity.x-=2*vdotn*nx;b.velocity.y-=2*vdotn*ny;const ov=(minDist-dist)+0.5;b.position.x+=nx*ov;b.position.y+=ny*ov;this.capBallSpeedFor(b);}}}
    for(const b of this.balls){
      const hitLeft=b.position.x-b.radius<this.paddleLeft.width&&b.position.y>this.paddleLeft.position.y&&b.position.y<this.paddleLeft.position.y+this.paddleLeft.height;
      if(hitLeft){b.velocity.x*=-1;b.lastHit='p1';const delta=b.position.y-(this.paddleLeft.position.y+this.paddleLeft.height/2);b.velocity.y=delta*PongConfig.ball.spinFactor;b.velocity.x*=1.25;b.velocity.y*=1.25;this.capBallSpeedFor(b);}
      const hitRight=b.position.x+b.radius>(PongConfig.canvas.width-this.paddleRight.width)&&b.position.y>this.paddleRight.position.y&&b.position.y<this.paddleRight.position.y+this.paddleRight.height;
      if(hitRight){b.velocity.x*=-1;b.lastHit='p2';const delta=b.position.y-(this.paddleRight.position.y+this.paddleRight.height/2);b.velocity.y=delta*PongConfig.ball.spinFactor;b.velocity.x*=1.25;b.velocity.y*=1.25;this.capBallSpeedFor(b);}
      if(b.position.x-b.radius<0){this.scores.p2++;this.playScoreSound('p2');this.checkWin()||b.reset();}
      else if(b.position.x+b.radius>PongConfig.canvas.width){this.scores.p1++;this.playScoreSound('p1');this.checkWin()||b.reset();}
    }
    const p1m=this.scores.p1>0&&this.scores.p1%3===0,p2m=this.scores.p2>0&&this.scores.p2%3===0;
    if(((p1m&&this.multiTriggered.p1!==this.scores.p1)||(p2m&&this.multiTriggered.p2!==this.scores.p2))&&this.balls.length===1){
      if(p1m)this.multiTriggered.p1=this.scores.p1;if(p2m)this.multiTriggered.p2=this.scores.p2;
      const b1=this.balls[0];b1.position.x=PongConfig.canvas.width/2;b1.position.y=PongConfig.canvas.height/2;b1.velocity.x=-Math.abs(PongConfig.ball.baseSpeedX);b1.velocity.y=(Math.random()*(2*PongConfig.ball.maxRandomY))-PongConfig.ball.maxRandomY;
      const b2=new PBall(PongConfig.ball.radius,PongConfig.canvas.width,PongConfig.canvas.height);b2.position.x=PongConfig.canvas.width/2;b2.position.y=PongConfig.canvas.height/2;b2.velocity.x=Math.abs(PongConfig.ball.baseSpeedX);b2.velocity.y=-b1.velocity.y;this.balls.push(b2);
    }
    if(this.balls.length>1){const kp1=this.multiTriggered.p1===this.scores.p1,kp2=this.multiTriggered.p2===this.scores.p2;if(!kp1&&!kp2){const keep=this.balls[0];keep.position.x=PongConfig.canvas.width/2;keep.position.y=PongConfig.canvas.height/2;keep.velocity.x=Math.sign(keep.velocity.x||1)*PongConfig.ball.baseSpeedX;keep.velocity.y=0;this.balls=[keep];}}
  }
  checkWin(){
    if(this.scores.p1>=PongConfig.rules.winningScore||this.scores.p2>=PongConfig.rules.winningScore){
      this.gameOver=true;this.restartBtn.style.display="inline-block";
      this.replayCountdown={until:performance.now()+5000};
      setTimeout(()=>{if(this.gameOver)this.restart();},5000);return true;
    }return false;
  }
  draw(){
    this.renderer.clear(PongConfig.canvas.width,PongConfig.canvas.height);
    this.ctx.save();this.ctx.strokeStyle=PongConfig.visuals.fg;this.ctx.lineWidth=2;this.ctx.setLineDash([10,6]);
    this.ctx.beginPath();this.ctx.moveTo(PongConfig.canvas.width/2,0);this.ctx.lineTo(PongConfig.canvas.width/2,PongConfig.canvas.height);this.ctx.stroke();this.ctx.setLineDash([]);this.ctx.restore();
    this.renderer.rect(this.paddleLeft.rect());this.renderer.rect(this.paddleRight.rect());
    const bumperActive=(this.scores.p1+this.scores.p2)>=PongConfig.bumper.enabledAtScore;
    if(bumperActive)this.renderer.circle({position:{x:PongConfig.canvas.width/2,y:PongConfig.canvas.height/2},radius:PongConfig.bumper.radius},PongConfig.bumper.color);
    let maxSpeed=0;
    for(const b of this.balls){this.renderer.circle(b);const vx=b.velocity.x||0,vy=b.velocity.y||0,sp=Math.sqrt(vx*vx+vy*vy);if(sp>maxSpeed)maxSpeed=sp;}
    if(this.powerUp){const pu=this.powerUp;this.ctx.save();this.ctx.fillStyle=PongConfig.powerUp.colors.bg;this.ctx.strokeStyle=PongConfig.powerUp.colors.border;this.ctx.lineWidth=2;this.ctx.fillRect(pu.x-pu.w/2,pu.y-pu.h/2,pu.w,pu.h);this.ctx.strokeRect(pu.x-pu.w/2,pu.y-pu.h/2,pu.w,pu.h);this.ctx.restore();}
    this.renderer.text(this.scores.p1,PongConfig.canvas.width/4,50);
    this.renderer.text(this.scores.p2,3*PongConfig.canvas.width/4,50);
    this.renderer.text("Speed: "+maxSpeed.toFixed(2),PongConfig.canvas.width-200,30);
    if(this.gameOver){
      this.renderer.text("Game Over",PongConfig.canvas.width/2-80,PongConfig.canvas.height/2-20,PongConfig.visuals.gameOver);
      const msg=this.scores.p1>=PongConfig.rules.winningScore?"Player 1 Wins!":"Player 2 Wins!";
      this.renderer.text(msg,PongConfig.canvas.width/2-120,PongConfig.canvas.height/2+20,PongConfig.visuals.win);
      if(this.replayCountdown){const s=Math.ceil((this.replayCountdown.until-performance.now())/1000);this.renderer.text('Restarting in '+s+'...',PongConfig.canvas.width/2-140,PongConfig.canvas.height/2+70,PongConfig.visuals.text);}
    }
    if(this.paused){this.ctx.save();this.ctx.fillStyle='rgba(0,0,0,0.5)';this.ctx.fillRect(0,0,PongConfig.canvas.width,PongConfig.canvas.height);this.ctx.fillStyle='#fff';this.ctx.font='36px Arial';this.ctx.fillText('PAUSED',PongConfig.canvas.width/2-60,PongConfig.canvas.height/2);this.ctx.restore();}
  }
  restart(){
    this.scores.p1=0;this.scores.p2=0;
    this.paddleLeft.position.y=(PongConfig.canvas.height-this.paddleLeft.height)/2;
    this.paddleRight.position.y=(PongConfig.canvas.height-this.paddleRight.height)/2;
    this.balls=[new PBall(PongConfig.ball.radius,PongConfig.canvas.width,PongConfig.canvas.height)];
    this.gameOver=false;this.restartBtn.style.display="none";
    this.powerUp=null;this.activeEffects={left:null,right:null};this.replayCountdown=null;
  }
  loop(){
    if(this.paused){this.draw();return;}
    this.handleInput();this.update();this.draw();
    requestAnimationFrame(this.loop);
  }
}

const pongCanvas=document.getElementById('pongCanvas');
const pongRestartBtn=document.getElementById('pongRestartBtn');
const pongStartPvP=document.getElementById('pongStartPvP');
const pongStartAI=document.getElementById('pongStartAI');
pongCanvas.width=PongConfig.canvas.width;pongCanvas.height=PongConfig.canvas.height;
let pongGame=null;

function startPong(useAI){
  if(pongGame){pongGame.ai=!!useAI;pongGame.restart();return;}
  pongGame=new PongGame(pongCanvas,pongRestartBtn,{ai:!!useAI});
  pongStartPvP.style.display='none';pongStartAI.style.display='none';
  pongGame.loop();
}
pongStartPvP.addEventListener('click',function(e){e.preventDefault();startPong(false);pongCanvas.focus();});
pongStartAI.addEventListener('click',function(e){e.preventDefault();startPong(true);pongCanvas.focus();});
})();
</script>

<h3>Connect 4</h3>
<p>Connect 4 is embedded live below — it demonstrates timer-driven state transitions (booleans), iteration over the board array to check winners, and <code>requestAnimationFrame</code> for the animated disc drop and confetti.</p>

<div style="margin: 24px 0;">
  <script src="https://cdn.tailwindcss.com"></script>

  <div id="title-screen" class="flex flex-col items-center gap-6 p-6 bg-blue-100 rounded-xl shadow-xl border-8 border-double border-blue-800">
    <div class="text-5xl font-extrabold text-blue-900 drop-shadow-lg">🔴 Connect 4 🟡</div>
    <div class="flex gap-4">
      <button onclick="c4game.startGame(60)"  class="px-6 py-3 bg-red-500    hover:bg-red-600    text-white rounded-lg shadow font-semibold">1 Minute</button>
      <button onclick="c4game.startGame(180)" class="px-6 py-3 bg-yellow-500 hover:bg-yellow-600 text-white rounded-lg shadow font-semibold">3 Minutes</button>
      <button onclick="c4game.startGame(300)" class="px-6 py-3 bg-green-500  hover:bg-green-600  text-white rounded-lg shadow font-semibold">5 Minutes</button>
    </div>
  </div>

  <div id="game-screen" class="flex flex-col items-center gap-6 p-6 bg-blue-100 rounded-xl shadow-xl border-8 border-double border-blue-800 hidden">
    <div class="text-5xl font-extrabold text-blue-900 drop-shadow-lg">🔴 Connect 4 🟡</div>
    <div id="c4-status" class="text-xl font-semibold text-blue-900">Player Red's turn</div>
    <div class="flex gap-8">
      <div>Red Timer: <span id="red-timer">00:00</span></div>
      <div>Yellow Timer: <span id="yellow-timer">00:00</span></div>
    </div>
    <div id="board" class="grid grid-cols-7 gap-2 bg-blue-600 p-4 rounded-xl shadow-inner"></div>
    <button onclick="c4game.reset()" class="bg-red-500 hover:bg-red-600 text-white px-6 py-2 rounded-lg shadow font-semibold">Restart Game</button>
    <div id="winner-overlay" class="hidden fixed inset-0 bg-black/50 flex flex-col items-center justify-center z-50">
      <div class="bg-white p-10 rounded-xl shadow-lg text-center">
        <div id="winner-text" class="text-4xl font-bold mb-4">Player Red Wins!</div>
        <button onclick="c4game.reset()" class="bg-red-500 hover:bg-red-600 text-white px-6 py-2 rounded-lg shadow font-semibold">Play Again</button>
      </div>
      <canvas id="confetti-canvas" class="absolute inset-0 pointer-events-none"></canvas>
    </div>
  </div>
</div>

<script>
class Connect4 {
    constructor() {
        this.rows = 6; this.cols = 7;
        this.currentPlayer = "Red";
        this.selectedTime = 180;
        this.redTime = this.selectedTime;
        this.yellowTime = this.selectedTime;
        this.timerInterval = null;
        this.board = [];
        this.discSpeed = 10;
        this.confettiParticles = [];
        this.initBoard();
        this.renderBoard();
        this.setupCanvas();
    }
    initBoard() {
        this.board = [];
        for (let r = 0; r < this.rows; r++) {
            this.board[r] = [];
            for (let c = 0; c < this.cols; c++) this.board[r][c] = null;
        }
    }
    renderBoard() {
        const boardDiv = document.getElementById("board");
        boardDiv.innerHTML = "";
        for (let r = 0; r < this.rows; r++) {
            for (let c = 0; c < this.cols; c++) {
                const cell = document.createElement("div");
                cell.classList.add("w-14","h-14","rounded-full","bg-blue-300","flex","items-center","justify-center","shadow-md","cursor-pointer");
                cell.dataset.row = r; cell.dataset.col = c;
                cell.addEventListener("click", () => this.placePiece(c));
                if (this.board[r][c]) {
                    const disc = document.createElement("div");
                    disc.classList.add("w-12","h-12","rounded-full","shadow-inner");
                    disc.style.backgroundColor = this.board[r][c];
                    cell.appendChild(disc);
                }
                boardDiv.appendChild(cell);
            }
        }
    }
    placePiece(col) {
        for (let r = this.rows - 1; r >= 0; r--) {
            if (!this.board[r][col]) {
                this.animateDiscDrop(r, col, this.currentPlayer);
                this.board[r][col] = this.currentPlayer;
                if (this.checkWinner(r, col)) { this.showWinner(this.currentPlayer); this.stopTimers(); }
                else { this.switchPlayer(); }
                break;
            }
        }
    }
    animateDiscDrop(row, col, color) {
        const boardDiv = document.getElementById("board");
        boardDiv.style.position = "relative";
        const disc = document.createElement("div");
        disc.classList.add("w-12","h-12","rounded-full","shadow-inner","absolute");
        disc.style.backgroundColor = color;
        const cell = boardDiv.children[row * this.cols + col];
        const rect = cell.getBoundingClientRect();
        const boardRect = boardDiv.getBoundingClientRect();
        const discSize = 48;
        const cellCenterX = rect.left - boardRect.left + rect.width / 2;
        const cellCenterY = rect.top - boardRect.top + rect.height / 2;
        disc.style.left = (cellCenterX - discSize/2) + "px";
        disc.style.top = "-50px";
        boardDiv.appendChild(disc);
        const targetTop = cellCenterY - discSize/2;
        const animate = () => {
            let currentTop = parseFloat(disc.style.top);
            if (currentTop < targetTop) { disc.style.top = Math.min(currentTop + this.discSpeed, targetTop) + "px"; requestAnimationFrame(animate); }
            else { disc.remove(); this.renderBoard(); }
        };
        animate();
    }
    switchPlayer() {
        this.currentPlayer = this.currentPlayer === "Red" ? "Yellow" : "Red";
        document.getElementById("c4-status").innerText = `${this.currentPlayer}'s turn`;
    }
    checkWinner(row, col) {
        const color = this.board[row][col];
        return (
            this.checkDirection(row,col,0,1,color) + this.checkDirection(row,col,0,-1,color) > 2 ||
            this.checkDirection(row,col,1,0,color) > 2 ||
            this.checkDirection(row,col,1,1,color) + this.checkDirection(row,col,-1,-1,color) > 2 ||
            this.checkDirection(row,col,1,-1,color) + this.checkDirection(row,col,-1,1,color) > 2
        );
    }
    checkDirection(r, c, dr, dc, color) {
        let count = 0, i = r+dr, j = c+dc;
        while (i>=0 && i<this.rows && j>=0 && j<this.cols && this.board[i][j]===color) { count++; i+=dr; j+=dc; }
        return count;
    }
    showWinner(color) {
        document.getElementById("winner-text").innerText = `Player ${color} Wins!`;
        document.getElementById("winner-overlay").classList.remove("hidden");
        this.launchConfetti();
    }
    startTimers() {
        this.stopTimers();
        this.updateTimerDisplay();
        this.timerInterval = setInterval(() => {
            if (this.currentPlayer === "Red") { this.redTime--; if (this.redTime<=0) { this.showWinner("Yellow"); this.stopTimers(); } }
            else { this.yellowTime--; if (this.yellowTime<=0) { this.showWinner("Red"); this.stopTimers(); } }
            this.updateTimerDisplay();
        }, 1000);
    }
    stopTimers() { clearInterval(this.timerInterval); }
    updateTimerDisplay() {
        document.getElementById("red-timer").innerText    = this.formatTime(this.redTime);
        document.getElementById("yellow-timer").innerText = this.formatTime(this.yellowTime);
    }
    formatTime(sec) {
        const m = Math.floor(sec/60).toString().padStart(2,"0");
        const s = (sec%60).toString().padStart(2,"0");
        return `${m}:${s}`;
    }
    startGame(seconds) {
        this.selectedTime = seconds; this.redTime = seconds; this.yellowTime = seconds;
        document.getElementById("title-screen").classList.add("hidden");
        document.getElementById("game-screen").classList.remove("hidden");
        this.startTimers();
    }
    reset() {
        this.stopTimers(); this.initBoard(); this.renderBoard();
        this.currentPlayer = "Red";
        this.redTime = this.selectedTime; this.yellowTime = this.selectedTime;
        this.updateTimerDisplay();
        document.getElementById("winner-overlay").classList.add("hidden");
        document.getElementById("game-screen").classList.add("hidden");
        document.getElementById("title-screen").classList.remove("hidden");
    }
    setupCanvas() {
        this.canvas = document.getElementById("confetti-canvas");
        this.ctx = this.canvas.getContext("2d");
        this.canvas.width = window.innerWidth; this.canvas.height = window.innerHeight;
    }
    launchConfetti() {
        this.confettiParticles = [];
        for (let i = 0; i < 100; i++) {
            this.confettiParticles.push({ x: Math.random()*this.canvas.width, y: Math.random()*this.canvas.height, r: Math.random()*6+4, color: i%2===0?"red":"yellow", dx: Math.random()*4-2, dy: Math.random()*4+2 });
        }
        requestAnimationFrame(() => this.updateConfetti());
    }
    updateConfetti() {
        this.ctx.clearRect(0,0,this.canvas.width,this.canvas.height);
        for (let p of this.confettiParticles) {
            p.x+=p.dx; p.y+=p.dy;
            if (p.y>this.canvas.height) p.y=0;
            if (p.x>this.canvas.width) p.x=0;
            if (p.x<0) p.x=this.canvas.width;
            this.ctx.fillStyle=p.color; this.ctx.beginPath(); this.ctx.arc(p.x,p.y,p.r,0,Math.PI*2); this.ctx.fill();
        }
        requestAnimationFrame(() => this.updateConfetti());
    }
}
const c4game = new Connect4();
</script>

<hr>

<h2 id="homework-links">Homework</h2>

<p>Every homework below maps directly to a concept above:</p>

<ul>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/24/iterationshomework-redo.html" target="_blank">Iterations</a></strong> — for/forEach/while loops used in pixel sampling, object processing, and round scheduling</li>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/24/nestedconditionals-redo.html" target="_blank">Nested Conditionals</a></strong> — multi-level if/else is the backbone of the Zone Catch survival check</li>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/24/mathematicalexpressions-redo.html" target="_blank">Mathematical Expressions</a></strong> — modulo, arithmetic, and Math methods used in zone sizing and distance checks</li>
  <li><strong><a href="https://kash484.github.io/portfolio/js/strings-hw" target="_blank">Strings</a></strong> — template literals, string indexing, and hex colour strings throughout</li>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/24/booleans-redo.html" target="_blank">Boolean Expressions</a></strong> — every guard clause and state flag; compound conditions in the survival check</li>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/24/arrays-homework.html" target="_blank">Arrays</a></strong> — circles array, colorPairs, samplePoints all drive Zone Catch logic</li>
  <li><strong><a href="https://kash484.github.io/portfolio/2026/02/24/jsonhw-redo.html" target="_blank">Objects (JSON)</a></strong> — JSON.stringify and JSON.parse; nested object config for sprites and gates</li>
</ul>

<div class="callout callout-green">
  <strong>The point:</strong> Every single homework has a real equivalent somewhere in the game. It's not just practice — the concepts genuinely show up in the final project.
</div>

<div class="footer">
  Built with JavaScript &nbsp;·&nbsp; HTML5 Canvas &nbsp;·&nbsp; Game Engine v1 &nbsp;·&nbsp; requestAnimationFrame<br>
  CSSE Final Project — Sprint 6 &nbsp;·&nbsp; Kashyap Tubati &nbsp;·&nbsp; Mar 23, 2026
</div>

</div>