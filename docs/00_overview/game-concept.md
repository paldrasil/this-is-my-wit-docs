---
Status: Draft
Owner: Game Design
Last Updated: 2026-05-08
Version: 0.3
Changelog:
  - Added metadata frontmatter.
  - Synced buffalo whistle/lead behavior notes.
---

# This is my wit!

# 🌿 Story

You are a buffalo herder in the forest.

A tiger appears and starts hunting.

You cannot fight it directly - you must **outsmart and mislead it**,

open a safe route, and guide the buffalo to safety.

---

# 🎮 Gameplay Core

```
Observe → Distract → Lead → Escape
```

---

# 🧑‍🌾 Player Actions

- 🪨 **Throw Stone** → create noise → tiger Investigates
- 🍖 **Drop Bait** → tiger transitions to Consume
- 📣 **Whistle** → call the buffalo from a distance (up to 3 tiles), signaling it to move toward the player
- 🪢 **Lead Buffalo (rope/lead action)** → only available when the player is near the buffalo; toggles follow mode

---

# 🐯 Tiger Behavior

## Perception

- Vision Far: forward-facing long vision cone
- Vision Near: close-range all-around awareness
- Hearing: medium-range sound detection

---

## States

```
Patrol A ↔ B
→ Investigate (sound)
→ Consume (bait)
→ Chase (detect target)
```

---

## Key Behavior

- **Investigate**: move to the sound source
- **Consume**:
    - stays in place for a period of time
    - loses long-range vision
    - responds weakly to surroundings -> creates a "safe window"
- **Chase**: triggered when the tiger detects the buffalo or player

---

# 🐃 Buffalo Behavior

- 📣 **Whistle**: buffalo responds to distance calls and prioritizes moving closer to the player
- 🪢 **Lead when near**: buffalo enters **FollowPlayer**
- ✋ **Release lead**: buffalo **stays in place** (`HoldPosition`) and does not auto-follow
- Moves slower than the player
- Cannot pass through:
    - Deep Water
    - Cliff
- Can pass through:
    - Mud -> slower movement / can get stuck
    - Shallow Water -> creates loud noise

---

# 🌿 Level Objects

## Hide / Cover

- **Tall Grass** -> concealment, lower detection risk
- **Rock** -> blocks line of sight

## Risk

- **Mud** -> slows movement, may trap units
- **Shallow Water** -> creates loud noise

## Control

- **Deep Water / Cliff** -> blocks buffalo routing

## Interaction

- **Meat Bait** -> strong lure
- **Stone Pile** -> noise source

---

# 🗺️ Sample Map (1 level)
  0 1 2 3 4 
0 R G T G R 
1 . . . . . 
2 . . . . . 
3 B P . . . 
4 C C C C S 
Tiger patrols from (0,1) to (0,3). Example route: player moves to (3,2) -> (3,3), drops bait at (2,3), returns to (3,0), whistles to call buffalo upward to (0,0) -> (0,4), waits for tiger consume/patrol timing near (0,1), then leads buffalo to (4,4).
---

# 🧩 Intended Solution

1. Use stone or bait to pull the tiger off patrol.
2. Use distance whistle (<= 3 tiles) to call the buffalo closer.
3. When near the buffalo, trigger lead action so it follows.
4. Avoid water noise zones where possible.
5. Time movement during tiger lure windows.
6. Deliver the buffalo to `S`.
