# Match Graphic Builder

A mobile-first, fully client-side football match graphic generator. Paste a
compact match summary and it builds a shareable 1080 × 1920 (9:16) graphic —
ready for TikTok/Instagram — with a live event timeline, running score, and
player stats. No backend, no AI API, no build step.

Open `index.html` directly, or deploy it with GitHub Pages (see below).

## Input format

```
Matchday 1
Great Colne 6-5 Opponent🟩
Mckeown 14’ 25’ 69’ 94’ ⚽️🅰️🅰️🅰️
Maximus 74’ 87’ 94’ 🅰️⚽️⚽️
Opponent 22’ 28’ 37’ 60’ 76’
```

- **Matchday line** (optional): `Matchday X`
- **Score line**: `Home Team H-A Opponent Name`, with an optional 🟩/🟥
  result marker after the opponent name.
- **Player lines**: minutes and symbols (⚽️ goal / 🅰️ assist) are matched
  in order. A player can also be listed with no minutes at all (e.g. just
  `Maximus`) and will still appear in Player Stats with 0 goals / 0 assists.
- **Opponent lines**: `Opponent 22’ 28’ …` — each minute is an opponent goal.
- **Red cards**: `Player 55’ 🟥` on its own line, for either team.
- Stoppage time (`90’+2`) and extra time (minute ≥ 91) are both supported.
- If a home goal has no explicit assist, an "AI" assist/goal is inferred
  internally for the timeline math — "AI" never appears in Player Stats.

## Using the app

1. Paste match data into the compact box.
2. Tap **Confirm & Build Graphic**.
3. Tap the **📦 Generated graphic** card to preview it (tap again to hide).
4. Tap **Save 9:16 Graphic** to save/download the PNG — on iPhone this opens
   the Share Sheet so you can save straight to Photos. After a successful
   save, the form resets automatically for the next match.

## Match log

Every match you build is saved to a log in the browser, below the builder.
The log shows a running record — played, won, drawn, lost, scored, conceded —
and one row per match. Each row can be rebuilt (↻) to regenerate its graphic,
or deleted (✕), or tapped to open it in the gallery.

Rebuilding a match that already has a `Matchday X` label updates that entry
rather than adding a duplicate, so correcting a typo and rebuilding keeps the
log clean.

The log lives in the browser's local storage on the device you used. It is not
uploaded anywhere, and it will not follow you to another phone or browser.
Clearing your browser data clears the log.

## Graphic gallery

Every match in the log gets a thumbnail in the **Graphic gallery**. Tap any
thumbnail to open it full-size, then use the ‹ › arrows (or swipe, or the
left/right arrow keys) to flip through every match you've built, oldest to
newest. Nothing extra is stored for this — thumbnails and the full-size view
are both regenerated on the fly from the same match text already saved in the
log, so the gallery can't drift out of sync with it and doesn't add to your
browser's storage usage.

## Player stats

The **Player stats** panel is a season leaderboard, aggregated automatically
across every match in your log: appearances, goals, assists, and combined
G+A, ranked highest first. It updates the moment you build, rebuild, or
delete a match — there's nothing to save separately.

Note: a player is aggregated by the exact name you typed, so keep spelling
consistent across weeks (e.g. always "Mckeown", not "McKeown" one week and
"Mckeown" the next) for their stats to combine correctly.

## Deploying with GitHub Pages

This is a static site — `index.html` is the entry point.

1. In the repository, go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Pick the branch you want served (e.g. `main`) and folder `/ (root)`.
4. Save. GitHub will publish the site at
   `https://<owner>.github.io/<repo>/`.

No build step or dependencies are required — everything runs client-side in
plain HTML, CSS, and JavaScript.
