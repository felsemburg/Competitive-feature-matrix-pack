# Output Templates

Read before Phase 5. Two deliverables: the full matrix table and the decision view. Both are mandatory.

## 1. The feature matrix table

ALWAYS precede the table with this "How to read this matrix" block, adjusted to the actual competitor count and segment. The point is that a brand-new PM and a veteran both understand every column and symbol at a glance, with no outside context:

```markdown
### How to read this matrix

Each row is one feature. Read left to right:
- **Cluster** — the capability group the feature belongs to (e.g. Exchanges, Logistics).
- **What it does** — one line, in plain terms.
- **Competitor columns** — one per researched competitor, plus your own product. Symbols:
  - ✓ has it (confirmed)   ◐ partial / weak / gated to a top tier   ✗ doesn't have it   ? couldn't verify
  - ● = YOUR product. ◐● = you have it but it's weak. ✗ in your column = a gap.
  - ★ before a feature name = a feature you asked me to force into the matrix for validation.
- **The five scores (0–5, higher = more of that thing unless noted):**
  - **E — Essential:** how much buyers in this segment expect it by default. High E = table stakes.
  - **A% — Adoption:** the share of competitors that ship it. This is counted, not guessed.
  - **D — Differentiation:** how much having it (or doing it well) sets a product apart. High adoption usually means low D.
  - **P — Problem-fit:** how directly it solves the core customer problem we defined.
  - **X — Effort:** rough build/fix cost for your team. NOTE: this is the one score where LOWER is better.
- **Score** — the overall priority, combining the above and weighting features you're missing. Higher = act sooner. (Full formula in the methodology section at the bottom.)
- **Verdict** — the recommended action:
  - **Build** = essential or high-fit feature you're missing → build it.
  - **Fix** = you have it but it's weak → improve it.
  - **Differentiator** = few rivals have it and it fits the problem → whitespace worth owning.
  - **Maintain** = you have it and it's fine → keep it, don't over-invest.
  - **Skip** = low-value / futile → don't chase it, even if competitors have it.

Rows are sorted by Score, highest first. Start at the top.
```

One row per feature, sorted by Priority Score descending. Use this exact column order:

| Feature | Cluster | What it does | [Comp1] | [Comp2] | … | [PM Product] | E | A% | D | P | X | Score | Verdict |

Rules:
- **What it does**: one line, ≤12 words, customer-benefit framed.
- One column per researched competitor, plus a clearly-labeled column for the PM's own product (use ● marks there).
- Cell marks: ✓ / ◐ / ✗ / ? as defined in feature-extraction.md.
- E, D, P, X are 0–5. A% is the raw percentage (show the number, e.g. "73%").
- Score is the composite Priority Score from the rubric.
- Verdict ∈ {Build, Fix, Differentiator, Maintain, Skip}.
- **Forced features** (the PM asked to validate a specific one): prefix the name with ★, always include the row even at 0% adoption, and never prune it. If no competitor has it, that's a finding, not a reason to drop it — note in the description whether it's genuine whitespace or simply unproven in the market.

If there are many competitors (8+), the table gets wide. Keep it as a real table anyway — the PM asked for every competitor marked. In the HTML decision view you can make competitor columns compact (icons only) so it stays readable.

After the table, add three short ranked lists pulled from it (these are the PM's actual action items):
- **Build next** — top Build-verdict rows by Score.
- **Behind the market** — rows where PM is ✗/◐ but adoption is ≥60%.
- **Whitespace** — Differentiator-verdict rows (low adoption, high problem-fit).

## 2. The decision view (visual)

The point is speed: a PM should look at it and know what to do without reading the whole table. Use the `visualize` tool. If unavailable, produce a single self-contained HTML artifact.

**Primary visual — opportunity quadrant** (scatter):
- X axis: Adoption % (how saturated the market is).
- Y axis: Differentiation score.
- Bubble size: Problem-fit (bigger = solves the core problem better).
- Bubble color: Verdict (Build / Fix / Differentiator / Maintain / Skip — distinct colors).
- Quadrant reading:
  - High-D / Low-A (top-left) = **whitespace** — own this.
  - High-D / High-A (top-right) = competitive battlegrounds — quality matters.
  - Low-D / High-A (bottom-right) = **table stakes** — must-have, won't differentiate.
  - Low-D / Low-A (bottom-left) = mostly **Skip** — futile zone.
- Label the PM's missing-but-essential features prominently (these are the urgent builds).

**Supporting elements in the same view:**
- A compact sorted bar/list of the top 8 features by Priority Score, colored by verdict.
- A small "you vs. market" readout: count of features where PM is ahead / at parity / behind.

Keep the visual self-explanatory: title, axis labels, a legend for colors and bubble size, and a one-line "how to read this". Make it interactive if using a tool that supports it (hover for feature name + scores), but it must still communicate at a glance when static.

### Rendering rules (avoid the blank-canvas failure)

A bubble/scatter chart that renders as a blank white square is the most common failure here. It happens when the drawing code runs before the chart library has loaded or before the canvas has a measured height. Always guard against both:

- **Load the chart library with a callback, don't assume it's present.** If injecting a CDN script (e.g. Chart.js), attach the draw logic to the script's `onload`; if the library is already on `window`, draw immediately. Never call the library at top level and hope it exists.
- **Draw after layout.** Wrap the draw call in `requestAnimationFrame` (or equivalent) so the canvas has real width/height before rendering. A canvas with zero measured height paints nothing.
- **Give the canvas a sized wrapper.** Put each canvas in a container with an explicit pixel height (e.g. `height:380px`) and `position:relative`, and use `responsive:true, maintainAspectRatio:false` so it fills that box.
- **Draw via `getContext('2d')`** on the canvas element, not a stale selector.
- **Fail loud, not white.** If the library can't load, insert a visible text fallback near the canvas instead of leaving a blank square — and always print the same data as a plain table so the chart is never the only copy of the information.
- **Prefer the platform's native visualization tool** when one is available (it handles loading/layout for you); only hand-roll a CDN-injected chart when no native tool exists.

## Written summary structure

Lead with decisions, not method:

```
## Bottom line
[2–3 sentences: the single most important takeaway and the top action.]

## Top moves
1. [Build X] — why, in one line.
2. [Fix Y] — why.
3. [Own Z whitespace] — why.

## Where you stand
[Ahead / parity / behind summary, 2–3 sentences.]

[matrix table]

[decision view]

<details>
## How this was scored
[methodology, competitor list, sources — collapsed/at the bottom]
</details>
```
