# Roaring Twenties Jeopardy — Live Multiplayer

Live, buzzer-based version of the Roaring Twenties Jeopardy review game.
You run the board on the projector (`index.html`), students join on their
own phones/Chromebooks (`player.html`) and buzz in for real.

## How it works

1. Open `index.html` on the projector/teacher computer. Pick a question set,
   set up your teams, click **Create Game & Get Room Code**.
2. A 4-character room code shows up big on screen. Students go to
   `player.html` on their own device, enter that code, type their name, and
   pick their team.
3. Once everyone's in, click **Start the Game**. The board appears.
4. Click any tile to open a clue. Click **Open Buzzers** is automatic —
   students' buzz buttons light up the moment the clue is shown. First
   student to tap wins the buzz for their team (ties are resolved
   automatically — whoever's tap reaches the server first).
5. Mark **Correct** or **Wrong**. Wrong locks that team out of this clue
   only — buzzers immediately reopen for the remaining teams.
6. Daily Doubles work the classic way: whoever's team picked the tile
   wagers (you enter the wager on your screen after asking them out loud),
   then you judge correct/wrong yourself — no buzzing involved.

## Setup (one-time)

This repo already has a Firebase config wired in (`firebase-config.js`),
pointed at the `roaring-twenties-live` Firebase project's Realtime
Database. Nothing to change there.

**Turn on GitHub Pages** so students can reach `player.html` from their own
devices:
1. On this repo, go to **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to **Deploy from a
   branch**, branch **main**, folder **/ (root)**, then **Save**.
3. After a minute or two you'll get a live URL like
   `https://jimmaoscott-lang.github.io/roaringtwentiesjeopardylive/`.
   Bookmark `index.html` for yourself and give students the
   `player.html` link (or just tell them to go to that base URL and tap
   "player.html" — easiest is to post the exact link on the board).

**Firebase Realtime Database rules:** when you created the database you
chose "test mode," which allows open read/write for 30 days and then locks
everything down. Before it expires, go to Firebase Console → your project
→ Realtime Database → **Rules**, and set:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

then click **Publish**. (This keeps it open — fine for a classroom tool
with no sensitive data. If you ever want it locked down further, that's a
separate conversation.)

## Notes

- Each game gets a fresh random room code, so old sessions from a previous
  class period don't collide with a new one — just click **New Game**
  between periods.
- The original single-screen version (`roaringtwentiesjeporady` repo)
  is untouched — this is a separate, standalone game.
- If a student's device loses connection mid-game, reopening
  `player.html` on the same device automatically rejoins them to the same
  room and team.
