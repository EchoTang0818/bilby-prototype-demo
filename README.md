# Bilby — clickable prototype

**▶ Open it: https://echotang0818.github.io/bilby-prototype-demo/**

Real-world routines feed a virtual animal the child chooses and names.
Parent assigns tasks and sets the coin value → child completes → parent approves → coins → care & grow.

A neurodiversity-friendly routine app for kids aged 5–10.

---

## 🎬 Demo script (5 min)

Both apps on the page are **live and connected** — do something on the right, watch the left update.

1. **Child onboarding** — pick one of 6 animals → **name it yourself** → Home.
2. **Parent builds a task** — Tasks tab → `＋ New task` → title, icon, **coin value 1–20 (the parent decides)**, 1–6 visual steps → Save. It appears in the child's app instantly.
3. **Parent re-prices** — the `±` controls next to any task change its coin value live.
4. **Child does the task** — tap it → step through → tap `🙋 I need help` → `All done`. Task = *waiting*. **Zero coins awarded yet.**
5. **Parent approves** — full / partly (half, rounded up) / **`Not today`** (awards nothing, **removes nothing**).
6. **Reward loop** — Shop → buy food → Care → feed → XP → the animal grows a stage.
7. Toggle **Low-stimulation mode** (top of page) to see the reduced-motion, reduced-colour variant.

Runs locally too — it's one file, no build step, no dependencies:

```bash
open index.html
```

---

## ⚠️ Non-negotiable design rules

These are product constraints, not preferences. Please read before writing any code.

| # | Rule | Why |
|---|---|---|
| **R1** | **No loss mechanics.** The animal never gets sick, decays, dies, or loses items. | Loss-based pet mechanics drive avoidance in ADHD/ASD children. There must be **no code path** that reduces XP, reduces coins, or degrades the pet's state. |
| **R2** | **The parent is the only source of truth.** The child app can never self-award coins. | Coins, XP and stage are mutated **server-side only**. The client never computes a balance it then writes back. |
| **R3** | **"Not today" awards nothing and removes nothing.** | No streak breaks, no deductions. Non-punitive. |
| **R4** | Partial completion is a first-class outcome, not a failure. | Executive-function reality. |
| **R5** | No leaderboards, no social, no chat, no comparison to other children. | Child safety. |
| **R6** | No loot boxes, no surprise mechanics. Every price is visible and readable. | Child-privacy code compliance + parent trust. |
| **R7** | **Every task attempt writes the full analytics/OT data model from day one.** | Retro-fitting it later means rebuilding. Spec is in the private repo. |
| **R8** | Parent setup ≤ 10 min/week; creating a routine ≤ 2 min. | If it takes longer, we have failed. |

---

## 🎨 Note on the art — important for estimation

All 6 animals are **one function plus a palette lookup** — a shared chibi rig where only **ears, tail, muzzle and colour** swap. See `petSVG()` in `index.html`.

**Production art must be built the same way.** 6 species × 4 growth stages = 24 base states, each needing wearable anchor points. Six independently drawn characters means **every new shop item needs six bespoke fits**, and the content pipeline dies.

If art cost forces a cut: ship **Cat + Dog + Bilby** first, but keep the `species` field and the picker screen from day one.

---

## 🙋 Open questions for engineering

- Offline-first? Kids will use this on a bathroom-floor iPad with no wifi. Queue attempts locally and sync?
- Multi-parent households: does either parent approve, or the assigning one?
- Art asset format — sprite sheets, Rive/Lottie, or SVG? (Prototype uses SVG.)
- Data residency — Australian region required from day one.
- Pet name: profanity filter must fail *gently* ("try another name"), never shame the child.

---

*Prototype only. Not production code. Not a clinical tool — no diagnosis, no therapeutic claim.*
*Full PRD, data model and acceptance criteria live in the private repo — ask Echo for access.*
