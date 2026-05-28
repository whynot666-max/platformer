# Platformer Game — Design Doc

**Date:** 2026-05-27
**Tool:** Plain HTML + JavaScript (single file, runs in any browser)
**Working title:** TBD

---

## Concept

A 2D side-scrolling platformer where you can't kill enemies — you **dash through them** to stun them, and **stunned enemies become temporary platforms** you must use to reach the next area. Walking into an un-stunned enemy hurts you. Levels are designed so the player has to dash, stun, and jump on enemies to make progress.

The tension: stunned enemies un-freeze after a few seconds. If you're standing on one when it wakes up, you fall (or get hurt). Every jump is a timing puzzle.

---

## Controls

| Action | Keys |
|---|---|
| Walk left / right | A / D **or** ← / → |
| Jump | W **or** Space **or** ↑ |
| Dash forward | J **or** Shift |

The dash works **in the air** as well as on the ground. After dashing, there is a short cooldown (~0.5 seconds) so it cannot be spammed.

---

## Core Mechanic: Dash → Stun → Auto-Mount → Platform

1. Player presses dash. Character moves quickly forward for a short distance.
2. If the dash hits an enemy:
   - The dash ends immediately on contact.
   - The player **auto-mounts** — snaps to the top of the enemy, standing on it. No extra jump input needed.
   - The enemy freezes in place and visibly changes color (e.g., glows blue).
   - The enemy stays frozen for **4 seconds**.
3. While frozen, the enemy acts as a solid platform. The player can stand on it and jump off it like any other platform.
4. When the 4 seconds end:
   - If the player is still on top of the enemy: the player falls.
   - If the player is touching the enemy from any side: the player takes damage.
5. Each enemy can be re-stunned by dashing into it again.

**Why this is fun:** every encounter is a tiny puzzle. You have to plan: dash this enemy, jump off it before it wakes, dash the next one, etc. The auto-mount makes the chain feel like one fluid motion — dash, dash, dash, you're surfing across stunned bots.

---

## Player Health

- Player has **3 hearts**.
- Touching an un-stunned enemy: lose 1 heart, brief invincibility (1 second).
- Falling off the bottom of the screen: lose 1 heart, respawn at start of level.
- 0 hearts → "You died" screen → restart level.

---

## Enemies

### Sprout-bot (Zone 1)
- Small robot covered in grass / leaves (it's been sitting in the field a long time).
- Walks back and forth on a fixed platform. Turns around at edges.
- Slow. Mostly a tutorial enemy — easy to dash through.
- When stunned: becomes a normal-sized platform.

### Floater-bot (Zone 2)
- Hovers in place at a fixed height. Does not patrol.
- Used as a **mid-air stepping stone**: the player dashes through one in mid-air, then jumps off it to reach a high ledge.
- When stunned: stays floating in place, acts as platform.

### Mini-boss (end of Zone 2)
- A bigger robot. Specific behavior TBD during implementation.
- Defeated by dashing through it 3 times, with timing puzzles in between.

---

## World & Levels

Played in order, no level select for v1.

### Zone 1 — The Field (Levels 1–3)
- Setting: grassy field, trees, blue sky, a factory visible in the distance.
- Loose story: robots have been escaping from a factory and getting stuck in the field. The player notices and goes to investigate.
- **Level 1:** Pure intro. Walk + jump only. One sprout-bot near the end teaches dash.
- **Level 2:** A pit you can only cross by dashing through a sprout-bot mid-air.
- **Level 3:** Multiple sprout-bots, timing-based jumps. Ends at the factory door.

### Zone 2 — The Factory (Levels 4–6)
- Setting: industrial. Conveyor belts, sparks, metal platforms, warning lights.
- New hazards: pits with electric floors, conveyor belts that push the player.
- **Level 4:** Introduces floater-bots. Mostly aerial dashes.
- **Level 5:** Combines sprout-bots, floater-bots, and conveyor hazards.
- **Level 6:** Mini-boss fight. Win = "You win!" screen.

---

## What's NOT in v1 (YAGNI)

Explicitly out of scope. Can be added later as v2:

- Sound effects and music
- Multiple playable characters
- Coins / score / collectibles
- Save system / level select
- More than 2 enemy types (plus boss)
- Cutscenes or dialogue
- Difficulty options
- Mobile / touch controls

**Reason:** the goal is a finished, playable 6-level game. Every feature added is a risk that the project never ships.

---

## Build Order (rough)

The order we'll build things in once we plan the implementation:

1. Player character: walk + jump (no enemies yet)
2. Add dash
3. Add a single sprout-bot, walking back and forth
4. Add hurt-on-touch + 3 hearts + respawn
5. Add stun-on-dash logic (dash + enemy collision → stun + auto-mount player on top)
6. Add stand-on-stunned-enemy as platform (player can jump off, falls when stun expires)
7. Build Level 1
8. Build Levels 2 and 3 (Zone 1 done)
9. Add floater-bot
10. Add factory hazards (conveyor, electric floor)
11. Build Levels 4–5
12. Mini-boss + Level 6
13. Title screen + win screen

---

## Success Criteria

The game is "done" when:

- All 6 levels are playable start to finish.
- The mini-boss can be defeated.
- The win screen appears after beating Level 6.
- A friend can play the whole game in one sitting (~10–20 minutes) without bugs blocking progress.
