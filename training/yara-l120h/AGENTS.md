# AGENTS.md — Yara Training Deck v2

This file is auto-loaded by Claude Code, Cursor, and similar AI coding tools. It tells the agent everything it needs to know to safely edit this deck.

## What this is

An 18-slide HTML presentation for Phase 1 of the Yara remote-operator training program (fjernstyrt L120H). Self-contained: one `index.html` plus a folder of images and one video.

- **Audience:** Yara wheel-loader operators in Porsgrunn / Herøya
- **Language:** Norwegian (with English technical terms preserved: HMI, geofence, light barrier, E-stop, retrofit, lidar)
- **Format:** Hosted as static site at https://presentations.hiveautonomy.no/training/yara-l120h/
- **Built by:** Ronny Liverød + Claude Code (May 2026)

## How the deck is structured

Each slide is a `<section class="slide">` element. The active slide gets `.active` added; CSS handles fade transitions and entrance animations. Navigation is keyboard + click + touch (see `<script>` at end of `index.html`).

Slide order:

| # | Slide | Class hints |
|---|---|---|
| 1 | Forsiden | `hero dark` |
| 2 | Visjonen | `photo-bg side-right` |
| 3 | Læringsmål | `pattern-grid` |
| 4 | Tre regelverk | `pattern-dots` |
| 5 | System 1: maskin og sensorer | (default light) |
| 6 | System 2: nettverk | `pattern-grid` |
| 7 | System 3: operatør-stasjon | (default light) |
| 8 | Dokumentasjon | `pattern-dots` |
| 9 | Light barriers / 3rd party stops | (default light) |
| 10 | Oppstart-prosedyre | `pattern-grid` |
| 11 | E-stop og safety reset | (default light) |
| 12 | HMI walkthrough | `pattern-dots` |
| 13 | Topp-5 feil | (default light) |
| 14 | Dry run video | `dark` |
| 15 | Veien videre (Fase 2/3) | `pattern-grid` |
| 16 | Yara HSE-kontakter | `pattern-dots` |
| 17 | Din installasjon | (default light) |
| 18 | Tusen takk | `hero dark close-slide` |

## Design system

CSS variables defined in `:root` of `index.html`:

```css
--navy:       oklch(30% 0.06 245);  /* primary brand */
--navy-deep:  oklch(15% 0.04 245);  /* dark backgrounds */
--cyan:       oklch(68% 0.12 245);  /* accent (used for cyan rules, eyebrow text on light) */
--yellow:     oklch(86% 0.16 95);   /* highlight, callouts, emphasis */
--paper:      oklch(98% 0.004 245); /* light slide background */
--ink:        oklch(18% 0.01 245);  /* body text */
```

Fonts (loaded from Google Fonts):
- **Fraunces** — serif display + headlines (titles, headlines, card-title, pillar-title)
- **Inter** — sans body
- **JetBrains Mono** — eyebrows, meta-labels, numbered annotations

Reusable component classes:
- `.eyebrow` — small uppercase mono label
- `.headline` — serif h2
- `.subhead` — secondary intro line
- `.card`, `.pillar`, `.col`, `.doc-card` — content boxes with entrance animation
- `.procedure` — numbered step list
- `.fault-table` — grid table for failure scenarios
- `.timeline` — phase progression
- `.video-slot` — lazy-loaded video frame (use `preload="none"` always)
- `.callout` — yellow-background highlight box

## Hard rules — do not break these

1. **Never use em dashes (`—`) in Norwegian copy.** They're an AI tell. Use periods, commas, or restructure. Single rule violation = fix immediately.
2. **Don't translate technical terms** that are industry-standard English: HMI, geofence, light barrier, E-stop, retrofit, lidar, 3rd party stop, autonomy, manual mode.
3. **Don't add `autoplay` or `loop` to videos.** They lazy-load via JS when their slide becomes active. The current `video` element has `preload="none"` and the JS controller in `<script>` handles `play()`/`pause()` based on `current` slide.
4. **Don't fabricate content.** Every contact name, phone number, date, statistic, or procedural detail must come from the user (Ravi or Ronny) or be marked with the `.tbc` class as a placeholder.
5. **Asset compression:** Keep images under 600 KB each. Keep videos under 25 MB. Compress with:
   ```
   ffmpeg -y -i INPUT.png -vf "scale='min(1920,iw)':'-2'" -q:v 4 OUTPUT.jpg
   ffmpeg -y -i INPUT.mp4 -vf "scale='min(1600,iw)':'-2'" -c:v libx264 -preset medium -crf 28 -an -movflags +faststart OUTPUT.mp4
   ```
6. **Total folder size cap:** 50 MB. Currently ~20 MB. Don't push past 50.
7. **Don't break the slide-counter pattern.** Each slide has `<div class="slide-counter">NN / 18</div>` matching its position. If you add a slide, update *every* counter.
8. **Don't change the JS navigation logic** unless asked. Keyboard, click, touch/swipe, hash deep-links, lazy video, and reduced-motion handling are all wired together.
9. **Accessibility:** Maintain `aria-hidden`, `role="progressbar"`, `:focus-visible` styles, and `prefers-reduced-motion` support. Test with keyboard nav after changes.
10. **Don't push to GitHub directly.** Make changes locally, send updated files back to Ronny who pushes to `ronron24ever2/hive-decks` repo.

## Common edits and how to handle them

### Add a new contact name
Find the slide (usually 16, 18) → look for `[navn — TBC]` or `.tbc` class → replace with real value → remove the `.tbc` styling.

### Replace an image
1. Place new image in `yara-training-assets/`
2. Compress with the ffmpeg command above (target 1920px wide, q:v 4)
3. Find the `background-image: url('yara-training-assets/X.jpg')` reference and update path
4. Test locally: `open index.html`

### Replace a video
1. Compress per ffmpeg command above (target 1600px, crf 28, no audio)
2. Generate a poster: `ffmpeg -ss 00:00:05 -i video.mp4 -frames:v 1 -q:v 2 video-still.jpg`
3. Replace both `<source src="...">` and `poster="..."` and `<img class="poster" src="...">`

### Add a new slide
1. Pick a position; copy the closest existing slide's structure as template
2. Add `data-slide="N"` matching its position
3. Add `<div class="slide-counter">NN / 19</div>` (note: also update the total)
4. Update *every* other slide-counter to use new total
5. The CSS animation delays are tied to `.slide.active .X:nth-child(N)` selectors — add new delays if needed

### Change typography globally
Edit the CSS variables in `:root`. Don't override per-slide unless absolutely necessary.

### Export to PDF
```bash
# from the deck folder
python3 ~/Code/ronny-os/scripts/deck-to-pdf.py index.html yara-training-v2.pdf
```
This produces a pixel-perfect PDF (Chrome headless screenshots + img2pdf). Required: `pip3 install img2pdf pillow` and Chrome installed. The script is in Ronny's local repo — if the recipient doesn't have it, ask Ronny.

## Files explained

| File | Purpose |
|---|---|
| `index.html` | The deck — single self-contained HTML file with inline CSS and JS |
| `README.md` | Human-friendly intro for Ravi |
| `AGENTS.md` | This file — instructions for any AI agent editing the deck |
| `yara-training-assets/` | All images + videos used by the deck |

## What's still flagged as TBC (needs Ronny / Yara input)

| Slide | Item |
|---|---|
| 12 | HMI mockup is a wireframe — replace with real screenshot when UI is locked |
| 14 | Tutorial video (full dry run) needs recording — Daniel as operator, Nicole filming |
| 16 | Yara HSE-leder name + phone |
| 16 | Yara koordinator (Hive-leveranse) name + phone |
| 16 | Skift-vakt phone number |
| 17 | Bilde of actual Yara installation (currently using marketing photo) |
| 17 | Operasjonsområde-spesifikk informasjon |
| 18 | Yara koordinator contact |
| 10, 11, 13 | Tutorial videos for procedures (Dmitri must green-light tech-locked-in first) |

## Source materials (for context)

- **Meeting note** (decisions): output of meeting 2026-05-05 10:00, Ravi+Ronny+Daniel+Kenneth+Michael+Nicole
- **Original training deck** (v1): `HA Operator Training WL1002 NO.pptx` (15 slides, deprecated)
- **Hive design system reference:** `vision-deck-v3.html` at `presentations.hiveautonomy.no/vision/`
- **Hive deck best-practices:** internal playbook at Ronny's working directory

## Versioning

Current file is v2.0 final (2026-05-05). When making major changes, save the previous as `index-v2.0-archive.html` before overwriting. Don't lose history.

## Contact

Ronny Liverød — `liverod@gmail.com`
Hive support 24/7 — `+47 38 13 46 00` · `support@hiveautonomy.no`
