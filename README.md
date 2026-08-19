# Bellringers

Start class strong. Fill the weird five minutes. Save your sanity.

A projector-first activity launcher for teachers. No downloads, no prep, no login —
open it, say what kind of five minutes you're dealing with, and put something on the board.

Live locally at **http://localhost:4213** (LaunchAgent `com.kennady.bellringers`).

---

## The idea

The homepage is not a subject taxonomy. It's a **situation launcher** — nine tiles that
name the teacher's actual problem ("They have way too much energy", "We finished early",
"Surprise me"). Filters for time / grade band / subject sit under it.

Everything is built on **formats**, not one-off activities. A format is a repeatable
mechanic; a deck is a themed bank of prompts inside it. That's why 24 decks produce
essentially endless Bellringers — `Next` never runs out.

## Structure

```
index.html          shell: header, view mount, projector player overlay
css/styles.css      the whole design system
js/formats.js       12 formats, the 9 situations, filter vocabulary
js/decks.js         24 decks / 195 prompts — the library
js/app.js           router, filters, stage renderers, player, Bellringer Mode
```

No build step, no dependencies, no framework. Open `index.html` and it works.

## The 12 formats

| Format | Render | What it does |
|---|---|---|
| Pick a Side | `duel` | Two options, commit before discussing |
| Wrong Answers Only | `statement` | Confidently wrong answers, then the real one |
| Odd One Out | `quad` | Four items, every one defensible |
| One Has to Go | `quad` | Eliminate one, forever, for everyone |
| Defend the Ridiculous | `statement` | Argue a position you don't hold |
| Estimate It | `reveal` | Impossible number question, reasoning over memory |
| Micro Mystery | `clues` | Three clues, revealed one at a time |
| 60-Second Story | `objects` | Three random objects, one minute |
| Caption This | `caption` | One line, anonymous, class votes |
| Would You Survive? | `quad` | Scenario, four decisions, real outcome |
| Beat the Teacher | `rapid` | Five rapid questions, class vs. you |
| Mystery Zoom | `zoom` | Zoomed way in, zoom out until someone shouts it |

## Adding content

Add a deck to `js/decks.js`. The prompt shape is determined by the format's `render`
type — the header comment in `js/formats.js` documents all nine shapes. Schema is strict:
a prompt missing a required key renders blank rather than erroring.

Validate before shipping:

```bash
node --check js/decks.js
```

## Bellringer Mode

`buildSequence(minutes, {grade, energy, subject})` picks activities that fit the time,
then expands each into timed facilitation beats using the per-format templates in
`BEATS`. Odd numbers work — "I have 7 minutes" returns exactly 7:00. Running a sequence
puts the player in sequence mode: a beat rail across the bottom, auto-started timer per
beat, `Next` advances the beat.

## Player controls

`→` / `space` next · `←` previous · `R` reveal · `T` timer (+1 min per press) ·
`F` full screen · `N` teacher notes · `Esc` close.

## Deliberate decisions

- **No accounts.** Favorites live in `localStorage` under `bellringers.favorites.v1`.
  The mockup had a "Sign In" button; the brief said no login. The brief won — the header
  says "No login. Ever." instead.
- **K-2 / 3-5 / 6-8 only.** No 9-12 chip, because there is no 9-12 content.
- **Emoji, not illustration.** Placeholder art that scales to any size and ships today.
  Mystery Zoom in particular works better than expected because of it.

## Not built yet

- Make Your Own (teacher-authored decks + shareable collections)
- 9-12 content
- K-2 social studies is thin (one deck)
- Deploy to GitHub Pages
