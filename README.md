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

## Deploying with GitHub Pages

This is a static site — `index.html` is the entry point.

1. In the repository, go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Pick the branch you want served (e.g. `main`) and folder `/ (root)`.
4. Save. GitHub will publish the site at
   `https://<owner>.github.io/<repo>/`.

No build step or dependencies are required — everything runs client-side in
plain HTML, CSS, and JavaScript.
