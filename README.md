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

## Bulk paste (a whole season at once)

Paste more than one match — each separated by a blank line — and the app
detects it automatically. The **Confirm & Build Graphic** button relabels
itself to show how many matches it found (e.g. "Confirm & Build 6 Graphics"),
and building adds every one of them to the gallery, player stats, and match
log in a single step.

```
Matchday 1
Great Colne 6-5 Opponent
Mckeown 14’ 25’ 69’ 94’ ⚽️🅰️🅰️🅰️
Maximus 74’ 87’ 94’ 🅰️⚽️⚽️
Opponent 22’ 28’ 37’ 60’ 76’

Matchday 2
Great Colne 5-6 Opponent
Maximus 7’ 11’ 41’ 59’ 84’ ⚽️⚽️⚽️⚽️🅰️
Mckeown 11’ 41’ 59’ 🅰️🅰️🅰️
Opponent 18’ 34’ 45’ 77’ 90’+2 102’
```

If any one match in the paste can't be read, nothing is added — you get an
alert naming which match (by its `Matchday X` label, or its position) needs
fixing, and the rest of the batch is left untouched until you fix it and
build again.

After a bulk build, a **Save all to Camera Roll** button appears: on iPhone
it opens the Share Sheet with every graphic at once (choose **Save Images**);
on desktop your browser may ask permission to allow multiple downloads.

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

The **Graphic gallery** panel is a single **View graphic gallery** button —
tap it to open the first match full-size, then use the ‹ › arrows (or swipe,
or the left/right arrow keys) to flip through every match you've built,
oldest to newest. Tapping a row in the match log opens that specific match
the same way. Nothing is pre-rendered for this — each image is drawn on the
fly, on demand, from the same match text already saved in the log, so the
gallery can't drift out of sync with it and doesn't add to your browser's
storage usage.

## Player stats

The **Player stats** panel is a season leaderboard, aggregated automatically
across every match in your log: appearances, goals, assists, and combined
G+A, ranked highest first. It updates the moment you build, rebuild, or
delete a match — there's nothing to save separately.

Note: a player is aggregated by the exact name you typed, so keep spelling
consistent across weeks (e.g. always "Mckeown", not "McKeown" one week and
"Mckeown" the next) for their stats to combine correctly.

## Exporting a stats image

Both the **Player stats** and **Match log** panels have an **📤 Export
image** button. Each renders its own shareable 1080 × 1920 graphic — in the
same visual style as a match graphic — built from everything currently in
your log:

- **Player stats export**: a "Top Scorer" / "Top Assister" spotlight plus
  the full season leaderboard.
- **Match log export**: your win/draw/loss record, goals scored/conceded and
  goal difference, a recent-form strip (last 5 results), and every match
  played.

Tapping either saves it the same way as a match graphic — the iOS Share
Sheet where available, otherwise a direct download.

## Does my data survive closing the browser?

Yes. Every match you build — and everything derived from it (the gallery,
player stats, match log) — is saved to your browser's local storage the
moment you build it, and reloading or reopening the page brings it all back
exactly as it was.

The one thing that *doesn't* persist is unbuilt draft text sitting in the
paste box — if you type or paste something and reload before tapping
**Confirm & Build Graphic**, that draft is lost (only built matches are
saved). This storage is local to the specific browser and device you're
using — it isn't synced anywhere, so it won't follow you to a different
phone or browser, and clearing your browser's site data clears it.

## Deploying with GitHub Pages

This is a static site — `index.html` is the entry point.

1. In the repository, go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Pick the branch you want served (e.g. `main`) and folder `/ (root)`.
4. Save. GitHub will publish the site at
   `https://<owner>.github.io/<repo>/`.

No build step or dependencies are required — everything runs client-side in
plain HTML, CSS, and JavaScript.
