# RiskVault iGaming — demo

Two self-contained pages. No build step, no server, no dependencies beyond a web font.

- `casino.html` — the player-facing site (lobby + a playable 3x3 slot).
- `admin-mvp.html` — the risk console, MVP scope.

## Deploying on GitHub Pages

1. Put these files in the repository root (or in `/docs`).
2. Settings -> Pages -> Deploy from a branch, pick the branch and that folder.
3. Open `casino.html`, play a few rounds, then open `admin-mvp.html` in a second tab.

`index.html` redirects to the game client so the Pages root works too.

## How the link between the two pages works

The client writes canonical events (bet placed, deposit completed) into browser
storage and announces them on a broadcast channel; the console reads the same
store and re-scores the player in place. Nothing needs configuring and nothing
is sent anywhere.

Two consequences:

- Both pages must be served from the **same origin** — the same Pages site.
- Both must be open in the **same browser**. Traffic does not cross devices or
  browsers; that needs the real backend described in the technical specification.

Sessions arriving from the real client are tagged `game client` in the console,
so they stay distinguishable from the built-in emulator that keeps the screens
alive on their own.

## Demo path

1. `casino.html` -> pick a profile in the DEMO panel, bottom left -> open a game -> spin 8-10 times, deposit once after a losing run.
2. `admin-mvp.html` -> Live Monitoring -> Players online: the row carries the `game client` tag, the current game and the live score.
3. Queue -> open the alert -> case workspace: decision code, rationale, actions.
4. Journal -> Evidence exports: the whole chain as a printable extract.

Player data is a stratified sample of an anonymised public aggregate export;
aliases are pseudonymous and no personal data is present.
