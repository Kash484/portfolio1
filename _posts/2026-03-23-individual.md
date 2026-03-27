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

<div style="text-align:center; margin: 28px 0;">
  <a class="play-button" href="https://rashig-1804.github.io/csse_teamrepo/hacks/TicTacToe/" target="_blank" rel="noopener noreferrer">▶ Tic-Tac-Toe</a>
  <a class="play-button" href="https://rashig-1804.github.io/csse_teamrepo/connect4/" target="_blank" rel="noopener noreferrer">▶ Connect 4</a>
  <a class="play-button" href="https://aadis12.github.io/student/hacks/whackamole" target="_blank" rel="noopener noreferrer">▶ Whack-a-Mole</a>
</div>

<div class="callout callout-blue">
  <strong>How they connect:</strong> Tic-Tac-Toe shows 2D array win checking (arrays + nested conditionals). Connect 4 uses timer-driven state transitions (booleans + iteration). Whack-a-Mole uses <code>Math.random()</code> for spawning and template literals for the score display — mathematical and string operators directly in the game loop.
</div>

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