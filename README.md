# GanitGuru — Maths Working Book

A bilingual (ગુજરાતી / English) web app that teaches students the **standard written methods** of arithmetic through step-by-step animation. A teacher types any sum — the website writes out the full working digit by digit, exactly the way it's done in an exercise book, with a plain-language explanation and optional voice narration for every step.

**Live demo:** https://ganit-guru.vercel.app/

## ✨ Features

- **Four operations, real school methods**
  - ➗ Long division — straight bracket lines, bring-downs, remainders
  - ➕ Column addition with carries (વદ્દી) written small in red
  - ➖ Column subtraction with borrowing — crossed-out digits, cascading borrows across zeros
  - ✖️ Long multiplication — starts from the highest digit, places the 0 placeholder first, and gives **each round of carries its own line** above the number
- **Bilingual** — ગુજરાતી by default, English one tap away; switching mid-sum re-narrates the current step without losing your place. Place values use the Indian system (એકમ, દશક, સો, હજાર, લાખ, કરોડ…)
- **Classroom-friendly controls** — Play/Pause with 3 speeds, step forward/back, restart, ⏭ skip to answer, keyboard shortcuts (arrow keys, spacebar)
- **🔊 Voice narration** — reads each step aloud in Gujarati or English using the device's text-to-speech (best on Android + Chrome)
- **Large numbers** — up to 12 digits (15 digits combined for multiplication), with cells that auto-shrink so wide sums fit any screen
- **Exercise-book design** — graph-paper grid, red margin line, handwriting-style digits, animated pen strokes

## 🚀 Run it

No build, no dependencies, no server — it's one HTML file.

```bash
# locally: just open it
open index.html

# or deploy to Vercel
npx vercel --prod
```

## 🎓 How to use in class

1. Type a sum: `156 ÷ 12`, `478 + 356`, `703 − 458`, `123 × 456` (also accepts `*`, `/`, `x`, `%`)
2. The setup appears — nothing moves yet
3. Press **▶ ચલાવો / Play** to animate automatically, or **આગળ / Next** to control the pace yourself
4. Use **⏭ જવાબ / Answer** to jump to the finished working, **⟲** to start over
5. Toggle **🔊** to have each step read aloud

## 🔧 Customisation cheat-sheet

Everything lives in `index.html`. The most useful knobs:

| What | Where | Change |
|---|---|---|
| Default language | `let LANG='gu';` (~line 216) | `'gu'` or `'en'` |
| Digit cell size | `Math.min(48, ...)` in `render()` | `48` = max px per digit |
| Gap between divisor and bracket | `widths[c.c]=Math.round(u*0.35)` | lower `0.35` = tighter |
| Horizontal line position | `el.style.left=xs[l.c0]+'px'` / `...*u+2` | shift left/right, up/down in px |
| Colours | CSS variables in `:root` | ink, red pen, green, paper, grid |
| All narration text | `S={en:{...},gu:{...}}` language packs | edit any sentence |
| Number limits | `la>12`, `la+lb>15` in `start()` | raise/lower digit caps |

## 🧠 How it works

Each operation has a *step builder* (`buildAdd`, `buildSub`, `buildMul`, `buildDiv`) that converts a sum into a list of steps — each step says which digits appear in which grid cells, which lines to draw, and what to narrate. A single renderer plays the steps back on an absolutely-positioned grid with variable column widths. Narration comes from per-language string functions, so the same step list renders identically in both languages.

## 📱 Notes

- Gujarati voice requires a Gujarati TTS voice on the device (built into most Android phones; on desktop, install one in OS language settings). The app detects this and shows install instructions if missing.
- Whole numbers only — by design, matching how the written methods are first taught.

## 📄 License

MIT — free to use in your school or classroom.

---

Built to help students *see* the method, not just the answer. 🇮🇳
