# Lemming Ball Z — Reborn 3D

A browser fighting game inspired by Lemmingball Z, built with Bun, React, TypeScript, and native WebGL. Fly around a destructible arena, fire energy blasts, and battle a CPU opponent or a friend locally. Player 1 supports keyboard and mouse or a standard USB / wireless controller; local Player 2 uses the keyboard.

This is an independent fan homage with original code and procedural artwork. It is not affiliated with the original game and does not bundle its assets.

## Features

- Over-the-shoulder 3D flight and energy combat, melee, charging, and slow motion.
- Thirteen battlegrounds with destructible terrain, buildings, and rooftop cover.
- Six fighters with editable names and roster choices saved on your device.
- CPU ranged combat and local duels using a shared camera.
- Fullscreen setup and pause menus, captured mouse aiming, and Gamepad API input.

## Getting started

Install [Bun](https://bun.sh/), then run:

```sh
bun install
bun dev
```

Open the local URL printed in the terminal, usually `http://localhost:3000`.

Use a desktop browser with WebGL, fullscreen, and pointer lock support. For controller access, serve the game over HTTPS or localhost. Starting or resuming a match requires fullscreen and mouse capture. If the browser blocks either request, the game stays paused and shows a retry message. Embedded previews may need to be opened in a separate browser tab.

## Starting a match

1. Click **Enter the arena** to open the fullscreen battleground selection menu.
2. Choose the battleground, game mode, fighters, and optional custom names. The mouse stays free while you choose.
3. Click **Start battle** to capture the mouse and begin the match.
4. Knock out the opponent or finish the three-minute round with more health.

### Keyboard and mouse controls

The over-the-shoulder camera keeps your fighter visible. Move the captured mouse to aim and steer. Hold either mouse button to fire repeatedly while energy is available. Blasts carve terrain and damage buildings, which provide cover and rooftop landing spots until destroyed.

| Action | Player 1 | Player 2 in local duel |
| --- | --- | --- |
| Fly forward / backward | W / S, along your aim | Up / Down arrows, vertically |
| Strafe / move sideways | A / D | Left / Right arrows |
| Aim | Mouse movement | Automatically toward Player 1 |
| Rise / descend | Space / Ctrl | Up / Down arrows |
| Move in depth | Mouse-directed flight | [ / ] |
| Melee | J | Delete |
| Quick energy shot | Left mouse button | Enter |
| Strong energy attack | Right mouse button | Page Down |
| Charge energy | E | End |
| Slow motion | Hold Shift | Shared effect |
| Pause and release mouse | Escape | Escape |

Leaving fullscreen, releasing mouse capture, or switching windows also pauses play and clears held inputs. Click **Resume fullscreen** to continue, or **Return to page** to leave fullscreen. **New Match** returns to setup. Sound can be muted in the arena toolbar.

The CPU favors ranged combat: it retreats when approached, maintains a firing-distance band, and closes the gap when the player moves too far away.

### Settings while fullscreen

Press **Escape** to release the mouse and open the fullscreen pause menu. You can edit both character names, select either fighter, choose a battleground, and switch between CPU and local duel without leaving fullscreen. Names and fighter choices continue to save automatically.

Changing a battleground, fighter, or mode is staged until you click **Apply & restart round**, which loads the new setup, restores health and terrain, and requests mouse capture again. If you only edit names, **Resume fullscreen** continues the existing round. The pause menu scrolls on smaller displays.

**New Match** and **Fight again** also open the setup menu before starting a fresh round. If fullscreen is blocked, the setup remains visible with an explanation and the battle stays stopped.

## USB and wireless controllers

The game polls the browser's [Gamepad API](https://developer.mozilla.org/en-US/docs/Web/API/Gamepad_API/Using_the_Gamepad_API) each frame. Plug in a controller, focus the page, and press a controller button so the browser exposes it. Use HTTPS or localhost; browser or embedding policies can block gamepad access.

Controllers reported with the browser's **standard** mapping are supported, including compatible Xbox and PlayStation controllers. Unmapped devices show an explanatory message instead of using guessed controls. The first standard controller controls Player 1; local Player 2 continues to use the keyboard. Additional controllers are not assigned to Player 2.

| Controller action | Binding |
| --- | --- |
| Fly and strafe | Left stick |
| Aim | Right stick |
| Quick shot | RT / R2 |
| Strong attack | LT / L2 |
| Melee | RB / R1 |
| Charge energy | LB / L1 |
| Rise | A / Cross |
| Descend | B / Circle |
| Slow motion | X / Square |
| Pause | Start / Options |
| Focus a setup control | D-pad up / down |
| Change a focused selection | D-pad left / right |
| Select / activate a menu control | A / Cross |

Sticks have a dead zone to reduce drift and retain analog movement strength. Disconnecting the assigned controller during play pauses the match and clears controller input. Keyboard and mouse remain available. A controller pause never automatically resumes the game.

**Click Start battle or Resume once with the mouse** to grant browser fullscreen and pointer-lock activation; controller polling cannot reliably supply that browser gesture. Names can be typed using the keyboard. The interface shows controller detection and support status. Physical USB hardware has not been tested in this development environment; automated tests cover mapping, analog input, button edges, disconnects, and gameplay integration.

## Characters and saved names

Choose from **Sprout, Rook, Nova, Glacier, Ember, and Volt**. Each has a distinct palette, build, and hairstyle; all have equal combat stats.

Custom names appear in the roster, HUD, and match results. Names are shared per character, including when that character is selected as an opponent. Names and both roster choices save automatically in localStorage under `lbz.profile.v1` and return on your next visit in the same browser and origin.

Clearing browser site data resets the saved profile. If storage is blocked or full, changes remain available for the current session and the roster reports that saving is unavailable.

## Battlegrounds

All thirteen battlegrounds share a 7,200 × 3,600-unit fighting area, a high flight ceiling, destructible terrain, and destructible buildings. Each has its own terrain, colors, and cover layout.

| Battleground | Terrain and cover | Buildings |
| --- | --- | ---: |
| Verdant Valley | Rolling hills and concrete outposts | 32 |
| Crimson Wastes | Red dunes and scattered strongholds | 20 |
| Midnight Peaks | Mountain ridges and isolated towers | 16 |
| Neon District | Flat streets and dense high-rise blocks | 60 |
| Frostbite Basin | Frozen bowl with perimeter structures | 12 |
| Ashfall Caldera | Volcanic crater ringed with bunkers | 18 |
| Sunscar Canyon | Winding corridor with buildings along its sides | 24 |
| Emerald Ruins | Green terraces and broad strongholds | 28 |
| Stormglass Flats | Open plains and relay stations along a spiral | 22 |
| Ironrail Depot | Warehouse rows around long freight lanes | 36 |
| Violet Sinkholes | Sunken bowls and clustered research stations | 25 |
| Obsidian Citadel | Raised plateau with perimeter fortifications | 40 |
| Copperstep Mesa | Sandstone terraces and alternating outposts | 30 |

Changing the selector before a match updates the preview; changes made during a paused match wait until you apply and restart. Each new round restores the selected map's terrain and buildings.

## Troubleshooting

- **Fullscreen or mouse capture is blocked:** open the game directly in a browser tab and click **Start battle** or **Resume fullscreen**. The game remains paused until both succeed.
- **Controller is not detected:** focus the page and press a controller button. Check the on-page controller status, use HTTPS or localhost, and verify your browser exposes a standard mapping.
- **Controller disconnects:** reconnect it, press a button, and click **Resume fullscreen**. Held controller inputs are cleared when it disconnects.
- **Saved names disappear:** profiles are stored per browser and origin. Clearing site data or changing the host or port creates a different storage context.
- **3D graphics are unavailable:** use a WebGL-capable browser and enable hardware acceleration.

## Development

```sh
bun test                # Gameplay, AI, maps, storage, settings, fullscreen, and controller tests
bun run typecheck       # TypeScript checks
bun run build           # Static production bundle in dist/
bun start               # Bun server with development features disabled
```

The production bundle can be served from `dist/` using a static web host. `bun start` runs the Bun server from source; it does not serve the `dist/` directory.

| File | Purpose |
| --- | --- |
| `src/App.tsx` | React UI, player input, fullscreen and pointer lock |
| `src/game.ts` | Combat, movement, collisions, terrain and building destruction |
| `src/renderer3d.ts` | Native WebGL renderer and procedural models |
| `src/arena.ts` | Arena dimensions and terrain resolution |
| `src/battlegrounds.ts` | Map definitions, terrain functions, and building layouts |
| `src/characters.ts` | Fighter roster and localStorage profiles |
| `src/opponent-ai.ts` | CPU distance and movement decisions |
| `src/fullscreen.ts` | Safe fullscreen cleanup |
| `src/match-settings.ts` | Staged settings and round resets |
| `src/gamepad.ts` | Controller mapping, polling, button edges, and menu navigation |
| `tests/` | Automated regression tests |

Rendering uses faceted meshes, directional lighting, distance fog, and a deformable terrain mesh. Terrain is uploaded after resets and ground impacts. Device pixel ratio is capped at 1.5, and GPU buffers are released when the game unmounts. Optional Google Fonts have system font fallbacks.

Local duel shares Player 1's camera. Online multiplayer, the original engine, its character roster, and mod support are not implemented. Automated checks cover game logic; fullscreen, pointer lock, and visual rendering also require testing in a real browser.

## Inspiration and license

Inspired by the flying combat, destructible terrain, and slow motion of [Lemmingball Z](https://www.lemmingballz.eu/), with reference to its [documentation](https://www.lemmingballz.eu/documentation/).

This project's original code and artwork are available under the [MIT License](LICENSE). Third-party dependencies and fonts retain their respective licenses. The license does not grant rights to the original game's name, trademarks, or assets.
