# Royal Bloom — QA Checklist

Balance-scale learning game (Tutorial + Levels 1–4). Use this to verify a build before release.
Tick every box. Anything unchecked is a blocker.

---

## 0. Automated gates (run first)

| Command | Expected |
|---|---|
| `node scripts/check-all.mjs` | `ALL STATIC CHECKS PASSED` |
| `node qa/smoke-test.mjs` | `SMOKE PASSED` (765 pass / 0 fail) |
| `node --check js/*.js` | no syntax errors |

- [ ] Static checks pass
- [ ] Smoke (viewport matrix) passes 765 / 0
- [ ] Open `index.html`, **hard-reload (Ctrl+Shift+R)**, open DevTools console → **no errors, no warnings**
- [ ] `file://` note: always hard-reload after a code change (browser caches old JS)

---

## 1. Global / cross-cutting (check on every screen)

- [ ] **Input**: mouse click, touch tap, pen/pointer, and keyboard all work
- [ ] **Responsive**: resize window / rotate — stage scales to fit, no horizontal scroll, nothing clipped or off-screen
- [ ] **Reduced motion** (OS "reduce motion" on): animations calm, confetti hidden, glow does not pulse
- [ ] **No console errors/warnings** at any point
- [ ] **Genie**: exactly one genie, one set of hands — no doubled/blurry duplicate (all screens)
- [ ] **Instruction bar**: left-aligned, full opacity, brown (#95491E), not clipped, updates every phase
- [ ] **Audio**: BGM loops after Let's Go; narration per phase; box/drop SFX; no overlap/stacking
- [ ] No duplicate listeners/timers after repeated play (drag, blur, revisit)

---

## 2. Intro

- [ ] "Let's Go" button animates and starts background music
- [ ] Rapid multi-click does **not** activate the Tutorial twice

---

## 3. Per-screen flow — repeat for **Tutorial, Level 1, Level 2, Level 3, Level 4**

### Part 1 — the box
- [ ] Instruction: "Tap the box."
- [ ] Tap the box → the **front box AND its lid wobble together** as one rigid unit
- [ ] The wobble does **not** shake the back box, glow, hidden items, or the whole scene; box does not go transparent or slide
- [ ] Box opens with golden sparkles rising **from inside**; lid lifts; items pop out

### Part 2 — item names
- [ ] Two name scrolls unfurl smoothly (parchment + rollers + centered name)
- [ ] **Each name matches its picture** (e.g. Tutorial shows Lantern + Feather; L1 Ribbon + Bell)
- [ ] Rollers stay attached to the parchment; both scrolls have identical layout; nothing detached

### Part 3 — weigh & answer
- [ ] Drag each item onto a pan — **drops when released near the pan** (not only on exact overlap)
- [ ] Placed item **nestles inside the pan** (bowl rim laps over its lower edge), full size
- [ ] Scale tilts so the **heavier side goes down** — matching where you placed the items
- [ ] Instruction "Tap the heavier item" / "Tap the lighter item" matches the level
- [ ] **You can tap the item on the pan** to answer (not blocked by the dish)
- [ ] **Correct** tap → vivid **green** pulsing glow on that item
- [ ] **Wrong** tap → vivid **red** pulsing glow → "Oops! Try again" → retry works
- [ ] Choosing one item does **not** fade or resize the other item
- [ ] **Heavier↓ / Lighter↑ arrows** sit over the correct pans — verify with the bell on the **left** AND on the **right**
- [ ] Correct answer → arrows appear, Next button shows

### Part 4 — sort into basket & wagon
- [ ] Drag lighter item → basket, heavier item → wagon (**drops when near**)
- [ ] Wrong container → feedback shown, item returns to start
- [ ] Correct drop → item **nestles inside** the basket/wagon (behind the front art), at a sensible size, never floating on the front or vanishing behind
- [ ] The "ghost" hint item hides once the real item covers it
- [ ] Both placed → golden sparkle bursts from the basket & wagon
- [ ] Next button advances (or final screen on Level 4)

### Transitions
- [ ] Next buttons advance exactly one step; rapid clicks don't skip/double

---

## 4. Final screen (Level 4 only)

- [ ] Final picture shows
- [ ] Golden stars burst **across the scene** (not stuck in the bottom-left corner)
- [ ] Final narration plays

---

## 5. Layout / placement

- [ ] Part 3 item cards are fully on-screen and do **not** overlap
- [ ] Each card's item image is **centered** in its card
- [ ] Balance-scale pan dishes render at the intended size (226×64) on every level
- [ ] Name-scroll rollers use the same layout on all 10 scrolls

---

## 6. Regression watch (previously-fixed bugs — confirm they stay fixed)

- [ ] Instruction text not frozen / updates per phase
- [ ] No duplicate genie body or hands (tutorial + all levels)
- [ ] Box tap shakes only the front box + lid (not all boxes, not the whole scene)
- [ ] Answer tap: no size change, evident glow, other item untouched, **item is tappable**
- [ ] Dragging is forgiving — releasing near a pan / basket / wagon drops the item
- [ ] Part 3 & Part 4 items sit *inside* their pan / basket / wagon
- [ ] Hint arrows match the actual placement on both sides
- [ ] Final stars burst over the scene
- [ ] Answer glow sprites never shrink/stretch the item

---

## 7. God Mode (dev/QA overlay — must be absent from the learner build)

- [ ] Shift+G toggles the God Mode overlay
- [ ] God Mode edits (move/scale/delete) reset when it is turned off — the learner build is untouched
- [ ] The shipped/learner build shows **no** God Mode UI

---

### Sign-off

| | Name | Date | Build |
|---|---|---|---|
| QA | | | |
| Approver | | | |
