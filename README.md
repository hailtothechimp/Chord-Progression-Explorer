# Chord Progression Explorer

A single-page web app for exploring, building, and previewing chord progressions on a virtual piano. Built for songwriters, students, and anyone who's ever wanted to *hear* the difference between Drop-2 and Open Spread voicings on the same progression.

Everything runs in the browser — no install, no build step, no backend. Just open the HTML file and play.

## What it does

Pick a key, a mode, a famous chord progression, and a voicing — and hear the whole thing played on a real-sampled grand piano with a live keyboard diagram lighting up under each chord. Then start tweaking:

- **Layer color** onto any chord (maj7, add9, 9, sus4, …) or change its quality entirely
- **Insert passing chords** between any two chords, with theory-aware suggestions (secondary dominants, tritone subs, common-tone diminished, sus anticipations, backdoor dominants, modal interchange)
- **Compare voicings** while the progression is looping — A/B between Smooth, Drop-2, Stride Bass, "So What," Hancock Spread, and 16 others
- **Build your own progression** from scratch with a chip-based palette
- **Save** your work, **export** to MIDI for Logic Pro / Ableton / GarageBand, or **print** a PDF chord sheet for the keyboard

## Features

### Core
- 12 keys × 2 modes (major / natural minor with harmonic V available)
- 100+ canned progressions organized by category (Classic Pop, Jazz, Classical, Modal/Rock, Modal Interchange, Country, Blues, Cinematic, etc.)
- Real Salamander Grand Piano samples via Tone.js
- 5-octave keyboard visualization (C2–C7) with shaded keys for the current chord
- Note-name readout with octave subscripts
- Voice-led playback — common tones are held, other voices move by the smallest possible step

### Voicings (19 of them)
- **Voice-Led** — Smooth
- **Triadic** — Close Root, First Inversion, Second Inversion
- **Open / Pianistic** — Open Spread, Wide Open, Octave Doubled, Stride Bass, Choir (SATB), Cluster (Add2)
- **Jazz** — Drop-2, Drop-3, Shell (1-3-7), Rootless (Bill Evans 3-5-7-9), Hancock Spread (1-5-9-3-7), "So What" (Modal Quartal + 3rd)
- **Rock / Folk** — Power, Power Wide, Quartal Stack (4ths)

Each comes with a built-in cheat-sheet (ⓘ next to the Voicing dropdown) explaining what it sounds like and where it's used, plus a one-click C-major preview.

### Chord color & quality
Click the **+** badge under any chord to:
- **Add color** — pick from explained options (6, 7, maj7, add9, 9, sus4, sus2) with descriptions and previews
- **Pick any chord type** — chip palette of 23 chord types in 5 groups (Triads, 6ths, 7ths, 9ths & Extensions, Suspended 7ths). Hover any chip to preview it in context; click to apply. Half-diminished chords are correctly notated as **ø7**.

### Passing chords
Click the **+** between any two chords to see the top 7 theory-informed suggestions, ranked:
- Secondary dominants (V7/X or V9/X depending on context)
- Sus anticipations (sus4 / sus2, or 7sus4 / 9sus4 in rich contexts)
- Common-tone diminished (vii°7/X)
- Tritone substitutions
- Backdoor dominants (♭VII7/X)
- Chromatic approaches above & below
- Modal interchange

Suggestions are context-aware — when surrounding chords carry 7ths or 9ths, the passing-chord options match that richness (e.g., V7 becomes V9, plain sus4 becomes 7sus4).

### Custom progression builder
Select **"✎ Build Custom…"** from the Progression dropdown to access:
- Chip palette of all diatonic chords for the current mode
- Common borrowed chords (♭III, ♭VI, ♭VII, iv, ♭II)
- Click to add, drag to reorder (works on touch with finger-drag), × to remove
- Extensions and quality changes per chord, just like presets

### Library
- Save current progression with a name
- Browse, load, and delete saved progressions
- **Export library JSON** for backup or sharing
- **Import library JSON** to merge another library into yours
- **Export current progression as MIDI** — drag the resulting `.mid` into any DAW
- **Print / PDF** — open a styled chord sheet showing each chord with a keyboard diagram and note names, ready to print or save as PDF and bring to the keyboard

### Playback
- Tempo slider (60–160 BPM)
- One full beat per chord, including passing chords
- Voicing changes while playing apply on the next chord — A/B in real time
- Final chord of any progression always voice-leads smoothly to resolve cleanly, regardless of selected voicing
- Click any chord to play just that one
- Hover any chord to see its keyboard / note chips without playing

### Touch / iPad support
- Tap palette chips, drag chords horizontally to reorder
- Bigger tap targets and always-visible action buttons on touch devices
- Vertical scroll still scrolls — only horizontal drag triggers reorder

## Getting started

### Easiest: open in a browser
Just double-click `chord-progression-explorer.html`. It runs from `file://` in most modern desktop browsers (Chrome, Edge, Firefox, Safari).

### On iPad / iOS
iOS doesn't run local `.html` files as live web pages. Host the file somewhere first:

- **GitHub Pages** — push to a repo, enable Pages, get a permanent URL
- **Netlify Drop** — drag the file onto [app.netlify.com/drop](https://app.netlify.com/drop), get an instant public URL
- **Local network** — run `python -m http.server 7890` in the file's directory, then visit `http://<your-computer's-LAN-IP>:7890/chord-progression-explorer.html` from your iPad while on the same Wi-Fi

Once it loads in Safari, use **Add to Home Screen** for an app-icon experience.

## Tech stack

- Plain HTML + CSS + JavaScript — no framework, no build step
- [Tone.js](https://tonejs.github.io/) for sample playback and synth fallback
- [Salamander Grand Piano](https://archive.org/details/SalamanderGrandPianoV3) samples (loaded over HTTPS from the Tone.js CDN)

The entire app is a single self-contained `.html` file. Copy it anywhere and it works — just needs an internet connection on first load to pull Tone.js and the piano samples.

## File structure

```
chord-progression-explorer.html   # The whole app
README.md                          # This file
```

That's it.

## Music-theory notes

A few opinionated choices worth knowing about:

- **The first chord's inversion in Smooth voicing** is anchored to a fixed reference around middle C (C4–E4–G4), so chord-tones land at whichever octaves bring them closest to that anchor. This keeps progressions in a sensible register regardless of key, but means the first chord's inversion can vary by key (e.g., E minor's first chord lands in second inversion: B3–E4–G4).

- **Half-diminished chords** are notated **ø7** (not °7, which means fully-diminished bb7).

- **Borrowed chords** with flat-prefixed numerals (♭VII, ♭VI, etc.) automatically use flat spelling in chord names, regardless of the key's natural preference for sharps or flats.

- **Custom progressions** are stored as Nashville numerals plus per-chord quality and extension overrides — so changing key transposes the whole progression instantly.

## Browser support

Tested on recent Chrome, Edge, Firefox, and Safari (desktop + iPad). Requires:
- HTML5 audio + Web Audio API
- ES6+ JavaScript
- CSS Grid + Flexbox
- HTML5 drag-and-drop (desktop) or touch events (iPad) for the custom builder

## License

MIT — do whatever you like with this.

## Credits

- Piano samples: Salamander Grand Piano (Alexander Holm)
- Audio engine: [Tone.js](https://tonejs.github.io/) by Yotam Mann
- Built with a lot of help from [Claude](https://claude.ai/)
