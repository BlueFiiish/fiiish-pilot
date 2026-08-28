# Fiiish Pilot

A ban-safe on-screen minimap and navigation overlay for **Escape from Tarkov** — live position, extract/quest arrows, and optional squad mode (see your friends' positions).

**Why it's ban-safe:** this app never reads game memory, never injects anything, and never sends input to the game. It only watches the Screenshots folder Tarkov itself writes to (your position/heading are encoded in the screenshot filename) and tails Tarkov's own log files for the current map and quest events. The same passive technique TarkovMonitor / Tarkov Market Pilot / TarkovQuestie have used for years. Your position only updates when **you** press your screenshot key — there is no continuous tracking.

## Install

1. Download the latest release from the [Releases page](../../releases/latest). You want one of:
   - **`Fiiish Pilot-Setup-<version>.exe`** — a normal one-click installer (installs for your user only, adds a Start Menu shortcut, no admin needed). **Recommended** if you just want it set up and forget about it.
   - **`Fiiish Pilot-Portable-<version>.exe`** — a single exe, no install, just run it from wherever you put it. Good if you want to keep it on a USB stick or don't want anything written to Program Files.
2. Run the exe. **Windows will show a SmartScreen warning** ("Windows protected your PC") because this isn't signed with a paid code-signing certificate. That's expected for a small free tool, not a sign of malware:
   - Click **More info**
   - Click **Run anyway**
3. The app starts with a tray icon (bottom-right of your taskbar) and a **first-run setup wizard** that walks you through everything below automatically — it autodetects your Screenshots and Tarkov Logs folders and tells you if something's wrong. You can mostly just click through it.

## In-game setup (2 settings)

Both are one-time:

1. **Escape from Tarkov → Settings → Game → Screen mode: Borderless.** The overlay can't draw on top of exclusive fullscreen, and borderless has no real performance cost on a modern PC.
2. **Escape from Tarkov → Settings → Controls → Screenshot:** bind it to a key you don't already use for anything else. **F10** is the default the app expects — if you use that key already, pick a different one and change it in the setup wizard (or the tray menu later) so the two stay in sync.

That's it. In a raid, tap your screenshot key whenever you want your dot on the map to move. The app never presses this key for you — it just watches for the file Tarkov creates when you do.

## Playing with the overlay

- **F8** — interact mode: click the map to drop a nav ping, click an extract/quest marker to navigate to it, drag the purple bar to move the panel, drag the corner to resize it. Press F8 again (or click "done") to hand control back to the game.
- **F7** — show/hide the whole overlay.
- **F6** — extract arrows (direction + distance to every PMC extract on the current map).
- **F9** — quest arrows (direction + distance to your active quest objectives — no TarkovTracker account needed, it reads the log Tarkov already writes).
- **Ctrl+F8** — cycle minimap size. **Ctrl+F9** — cycle opacity. **Ctrl+F6** — toggle the minimap panel.

**Don't like those keys?** The setup wizard has a **Your keys** step where you click a key and press whatever you want instead — it warns you if two actions clash, if a key is already taken by another app, or if you pick something Tarkov itself needs. Reopen it any time from the tray icon. New keys apply immediately, no restart.

Everything else is configurable from interact mode's filter panel (appearance, what's shown per-map) or the tray icon.

## Playing with friends (squad mode)

Squad mode shows your squad's positions on your own map, same freshness rules as your own dot (a dot older than 45 seconds shows its age; a teammate who left or changed maps disappears rather than showing a stale ghost).

1. Open interact mode (**F8**) → the **squad** section. (The setup wizard also offers this on its **Squad** step.)
2. Type a display name.
3. One of you clicks **create squad** — a 6-character code appears. Share it (voice, Discord, whatever).
4. Everyone else types that code into **join**.

The server this uses is already set up and filled in for you — there's nothing to configure. Codes use `A-H J-N P-Z 2-9` only (no `I`, `O`, `0` or `1`), so reading one aloud can't send two people to different squads.

**Privacy:** your position is only ever sent to your own squad's room (identified by the code, nothing is browsable). Nothing is logged or stored anywhere — the relay only ever holds your *last* position, attached to your open connection, and that's gone the instant you disconnect.

## Problems?

- **Wrong folder detected for screenshots/logs** — tray icon → **Setup wizard**, or Browse to the right one by hand. Common if OneDrive redirects your Documents folder.
- **Position not updating** — make sure the key you press in-game is the same one shown as your screenshot key in the setup wizard. The wizard's **Live test** step confirms it end-to-end: it goes green the moment it reads a screenshot you just took.
- **A key does nothing (F8, F6, ...)** — something else on your PC has grabbed it globally. Discord, GeForce Experience, the Steam overlay and other map tools all do this. **The app tells you:** a red banner appears top-left naming the key and the action it broke, the tray tooltip says how many keys are blocked, and the wizard's **Your keys** step marks it `TAKEN` in red. Either close whatever owns it, or record a different key right there.
- **Maps look blank / no extract or quest markers** — the app refreshes its map data from tarkov.dev on its own when it's more than two weeks old. Give it a minute on a working internet connection, then restart it.
- Anything else — ask whoever gave you this app.
