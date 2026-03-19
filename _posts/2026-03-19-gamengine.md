---
layout: post
codemirror: true
title: Gamify Formatives
description: My three custom game levels built with the GameEngine framework.
permalink: /gamengine/formatives
---

## Level 1: Slime on Alien Planet

My first custom level features a slime character exploring an alien planet. I added Chill Guy as an NPC who greets you when you walk up to him, plus an invisible barrier to block off part of the map.

**Controls:** WASD to move. Walk up to Chill Guy to trigger a dialogue!

{% capture challenge1 %}
Explore the alien planet as a slime! Walk up to Chill Guy and interact with him. Try moving in all directions to see the slime's different animations.
{% endcapture %}

{% capture code1 %}
import GameControl from '/assets/js/GameEnginev1/essentials/GameControl.js';
import GameLevelKashslime from '/assets/js/adventureGame/GameLevelKashslime.js';

export const gameLevelClasses = [GameLevelKashslime];
export { GameControl };
{% endcapture %}

{% include game-runner.html
   runner_id="game1"
   challenge=challenge1
   code=code1
%}

---

## Level 2: Nonchalance Meter

My second level has a custom UI element — a **Nonchalance meter** that increases by 10 every time you interact with Chill Guy. This was my first time adding custom JavaScript UI on top of the game canvas.

**Controls:** WASD to move. Walk up to Chill Guy and interact to raise your Nonchalance!

{% capture challenge2 %}
Talk to Chill Guy and watch the Nonchalance meter at the bottom of the screen go up every time you interact with him. How high can you get it?
{% endcapture %}

{% capture code2 %}
import GameControl from '/assets/js/GameEnginev1/essentials/GameControl.js';
import GameLevelKashcustom from '/assets/js/adventureGame/GameLevelKashcustom.js';

export const gameLevelClasses = [GameLevelKashcustom];
export { GameControl };
{% endcapture %}

{% include game-runner.html
   runner_id="game2"
   challenge=challenge2
   code=code2
%}

---

## Level 3: Kirby Meets Donkey Kong

My third level switches it up — you play as **Kirby** on the alien planet, and the NPC is **Donkey Kong** who has something to say about your hair.

**Controls:** WASD to move. Walk up to Donkey Kong to hear what he has to say!

{% capture challenge3 %}
Play as Kirby and go talk to Donkey Kong. What does he say? See if you can find the invisible barrier hidden in the level too.
{% endcapture %}

{% capture code3 %}
import GameControl from '/assets/js/GameEnginev1/essentials/GameControl.js';
import GameLevelGameleveltwo from '/assets/js/adventureGame/GameLevelGameleveltwo.js';

export const gameLevelClasses = [GameLevelGameleveltwo];
export { GameControl };
{% endcapture %}

{% include game-runner.html
   runner_id="game3"
   challenge=challenge3
   code=code3
%}