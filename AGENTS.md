# AGENTS.md

## Setup and verification

- Static HTML5 Canvas game with no package manifest, dependencies, build, tests, lint, or typecheck. `index.html` loads `game.js` as a classic script (not a module).
- Verify by running it in a browser: open `index.html` directly, or `npx serve .` and visit `http://localhost:3000`. There are no automated verification commands.

## Gotchas

- `README.md` is UTF-16LE with a BOM: normal readers/tools report it as binary; decode as UTF-16LE to read or edit it.
- `README.md` is partly aspirational: it advertises power-ups and an "estrella fugaz" that `game.js` does not implement. Treat `game.js` as the source of truth for current behavior.
- Canvas size is duplicated in the `width`/`height` attributes of `index.html` and the `W`/`H` constants in `game.js`; change both together.
- Input uses `e.code` and one-shot presses go through `pressed(code)`, which consumes the `justPressed` flag. Calling `pressed()` twice for the same key in one frame drops the second check. Space and arrows are `preventDefault()`ed.
- `game.js` holds all mutable state in top-level variables driven by a single `requestAnimationFrame` loop (`update(dt)` then `draw()`); `dt` is capped at 0.05s.
- User-facing strings, comments, and the README are in Spanish; keep that convention for new text.
