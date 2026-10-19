# 🏰 Pixel Tower Defense (像素塔防)

> A browser-based real-time strategy tower defense game — **single HTML file, zero dependencies, fully offline, Chinese UI**. Double-click and play.

**[🎮 Play Now](https://studyguy.github.io/pixel-tower-defense/)** · **[📦 Source Code](https://github.com/studyguy/pixel-tower-defense)**

---

## 🕹️ What Is This

Enemies stream down a winding S-shaped road in wave after wave. You build, upgrade, and sell defense towers on the grass beside the path to stop them from reaching your base. The game features **20 waves**, **5 enemy types** (including a Boss that heals and summons minions), and **7 tower types** (each with a 3-level upgrade tree, unlocked progressively as waves advance).

The whole game lives in **a single `index.html`**: Canvas rendering + DOM overlay UI + Web Audio-synthesized sound, with zero external dependencies — nothing to download, nothing to install, no programming knowledge needed. Open it in a browser and play, even fully offline.

This project was built independently by [studyguy](https://github.com/studyguy) via **Vibe Coding**, for learning and entertainment purposes only.

## ✨ Features

- **7 towers × 3 upgrade levels**: Arrow (fast single-target, anti-air) / Cannon (area splash) / Frost (stackable slow) / Laser (damage scales with distance — 2.0× at max range) / Poison (stackable DoT, unlocks wave 6) / Chain Lightning (3–5 targets, wave 10) / Sniper (400 range one-shots, wave 13)
- **5 enemy types**: Normal / Fast / Armored (50% slow resist) / Flying (ignores terrain; only Arrow and Laser can hit it) / Boss (waves 5, 10, 15, 20 — alternates healing and summoning every 8s; double Boss at wave 20)
- **20 escalating waves**: compositions scale linearly, enemy HP grows up to ~9×; **early-start** the next wave for bonus gold
- **Strategic depth**: three target-priority modes on the fly (first / nearest / highest HP), stackable slows (capped 85%), distance-scaled laser damage
- **Economy**: kill rewards + wave bonuses + **passive income** (scales with waves) + 60% refund on sell
- **Presentation**: flat cartoon + pixel accents, day-night color cycling, damage numbers, screen shake, Web Audio SFX + chiptune-style looping BGM (no audio files)

## 🎯 Gameplay Reference

### Controls

| Key | Action |
|---|---|
| `1`–`7` | Select a tower to enter placement mode (press again to cancel); towers unlock by wave |
| LMB / RMB·`ESC` | Place / select tower · cancel placement |
| `U` / `S` | Upgrade selected tower / sell (60% refund) |
| `Space` | Start the next wave early (bonus gold) |
| `T` | Cycle target priority: first → nearest → highest HP |
| `P` / `M` / `Enter` | Pause / mute / start-restart |

### Tower Overview

| Tower | Role | Unlocks | Lv.1 cost |
|---|---|---|---|
| 🏹 Arrow | Fast single-target, anti-air | Wave 1 | 60 |
| 💣 Cannon | Area splash, ground only | Wave 3 | 110 |
| ❄️ Frost | Slow control, stackable | Wave 5 | 90 |
| 🧪 Poison | DoT, stacks up to 3× | Wave 6 | 120 |
| ⚡ Laser | Sustained beam, distance-scaled, anti-air | Wave 8 | 160 |
| ⚡ Chain Lightning | 3–5 target chain, anti-air | Wave 10 | 190 |
| 🎯 Sniper | Extreme range, high single-target, anti-air | Wave 13 | 230 |

### Enemy Quick Reference

| Enemy | HP | Speed | Trait |
|---|---|---|---|
| Normal 🔴 | 40 | 60 | Basic enemy |
| Fast 🟡 | 25 | 105 | High speed, hard to intercept |
| Armored 🔵 | 150 | 38 | Tanky and slow; 50% slow resist |
| Flying 🟣 | 32 | 95 | Flies straight at base, slow-immune, only Arrow/Laser can hit |
| Boss 👹 | 1550 | 30 | Slow-immune, scales with waves (×1.03→×1.7), heals + summons |

> General rules: enemies walk the 5-lane S path; leaks damage your base (20 HP total); kills drop gold with floating numbers; enemy HP scales ×(1+0.42×(wave−1)).

## 🚀 Quick Start

| Method | How |
|---|---|
| 🌐 Play online (recommended) | [studyguy.github.io/pixel-tower-defense](https://studyguy.github.io/pixel-tower-defense/) — no files to download |
| 💻 Play locally | Clone the repo and double-click `index.html` (`file://` works) |
| Compatibility | Chrome / Edge / Firefox / Safari (last ~2 years), desktop and mobile; auto-scales to any window size |

> Sound takes effect after the first click on "Start Game" (standard browser autoplay policy — expected behavior).

## 🛠️ Technical Notes

**Single-file architecture** (`index.html`, ~1,540 lines, 14 logical sections):

```
<style>   Layout / HUD / panels / menu animations
<body>    Canvas + HUD + build bar + selection panel + overlay menus
<script>  Config → audio engine → global state → entities (Enemy/Tower/Projectile)
          → effects → wave manager → game flow → main update → draw → input → UI → loop
```

- **Rendering**: single 2D Canvas with devicePixelRatio scaling; `requestAnimationFrame` main loop, `dt` clamped to 50ms (no frame skips after tab-switch)
- **Audio**: all SFX and the chiptune BGM synthesized in real time via Web Audio — zero audio files
- **Deterministic decoration**: grass and path speckles use hash-based randomness — the map looks identical after refresh
- **Testing**: static checks (`node --check` + tag/reference validation) plus **53 headless smoke tests** (a stub environment driving the real game logic, ~1,700 simulated seconds covering placement validation, upgrade edge cases, Boss skills, and a full 20-wave clear; the tests caught and fixed 2 real bugs)

## 📁 Project Structure

```
pixel-tower-defense/
├── index.html   # The entire game (HTML + CSS + JS in one file)
└── README.md    # This file
```

## 📜 Disclaimer

- This project was built independently by [studyguy](https://github.com/studyguy) via **Vibe Coding**, for learning and entertainment only. Any resemblance to other projects is purely coincidental.
