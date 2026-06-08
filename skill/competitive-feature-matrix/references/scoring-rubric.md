# Scoring Rubric

Read this before Phase 4. The point of fixed anchors is consistency: two different runs of this skill on the same market should produce roughly the same scores. Score each feature on five dimensions, 0–5, then compute the composite Priority Score.

## The five dimensions

### Essential (E) — is this table stakes?
How much a buyer in this segment expects the feature by default. A product missing a high-E feature looks broken or incomplete during evaluation.

- 5 — Deal-breaker. Buyers reject products without it. (e.g. for returns: a self-service return portal)
- 4 — Strongly expected; absence is noticed and counts against you.
- 3 — Common and helpful, but absence is forgivable.
- 2 — Nice to have; few buyers ask.
- 1 — Rarely expected.
- 0 — Nobody expects it; irrelevant to the segment.

### Adoption (A) — computed, not judged
Share of researched competitors that ship the feature. Store as a percentage AND map to a 0–5 band for the composite.

`A% = competitors_with_feature / total_competitors_researched`

Partial implementations (◐) count as 0.5. Bands:
- 5 — 80–100%
- 4 — 60–79%
- 3 — 40–59%
- 2 — 20–39%
- 1 — 1–19%
- 0 — 0% (only the PM's product has it, or nobody does)

### Differentiation (D) — does it set you apart?
How much shipping this (or doing it notably better) distinguishes a product. Usually inversely related to adoption: if everyone has it, having it differentiates little — though *doing it well* can still differentiate.

- 5 — Rare and a major reason buyers switch. Defensible moat.
- 4 — Uncommon, clear selling point.
- 3 — Some differentiation, especially via quality of execution.
- 2 — Minor; everyone roughly at parity.
- 1 — Commodity.
- 0 — No differentiation possible.

### Problem-fit (P) — does it solve the core problem?
How directly the feature addresses the customer's stated core problem (locked in Phase 1). This is the dimension that keeps the matrix honest — a flashy feature that doesn't move the core problem scores low here.

- 5 — Directly solves the core problem; central to the value prop.
- 4 — Strongly supports solving it.
- 3 — Helps somewhat / indirectly.
- 2 — Tangential.
- 1 — Barely related.
- 0 — Unrelated to the core problem.

### Effort (X) — build/fix cost (lower is better)
Rough cost for the PM's team to build it well or fix it to parity. Ask the PM for team size/constraints; default to a small team (≈1 dev) if unknown, which pushes large efforts higher.

- 5 — Massive (quarters of work, new infra). 
- 4 — Large (multi-sprint).
- 3 — Moderate (a sprint or two).
- 2 — Small (days).
- 1 — Trivial (hours / config).
- 0 — Already built (for "Fix"/"Maintain" rows where it just needs polish, use 1–2).

## Composite Priority Score

Goal: surface features that are essential or high-fit, that the PM is *missing or weak on*, and that aren't prohibitively expensive. Differentiation gets a bonus so whitespace plays don't get buried.

```
GapFactor   = 2 if PM lacks the feature (✗)
            = 1 if PM has it but partial/weak (◐)
            = 0.4 if PM already has it well (●)   # de-prioritize maintenance

Value       = (1.4 * E) + (1.5 * P) + (1.1 * D) + (0.6 * A_band)
EffortPenalty = 0.7 * X

PriorityScore = round( (Value * GapFactor) - EffortPenalty , 1 )
```

Why these weights: Problem-fit (1.5) and Essential (1.4) dominate because building things customers expect and that solve their problem is the safest bet. Differentiation (1.1) is rewarded but not over-weighted (whitespace is risky). Adoption (0.6) is a weak positive — it confirms a feature is real, but high adoption also means low differentiation, so it shouldn't dominate. GapFactor is the multiplier that turns "good feature" into "good feature *we don't have*", which is what prioritization is actually about. Effort is subtracted, not multiplied, so a cheap win can outrank an expensive essential.

Sort the matrix by PriorityScore descending.

## Verdict logic

Assign each feature one verdict. Resolve in this order:

1. **Skip** — futile/low-value. Assign if `E ≤ 1 AND P ≤ 1 AND D ≤ 1`, regardless of adoption. These are features that exist in the market but don't earn their keep — call them out explicitly so the PM knows not to chase them. (A feature can have decent adoption and still be Skip if it's a checkbox nobody benefits from.)
2. **Differentiator** — whitespace worth owning. Assign if `D ≥ 4 AND A_band ≤ 2 AND P ≥ 3` (rare, high-fit, underexploited).
3. **Build** — essential gap. Assign if PM lacks it (✗) AND `(E ≥ 4 OR P ≥ 4)`.
4. **Fix** — have it but weak. Assign if PM has it partially (◐) AND `(E ≥ 3 OR P ≥ 3)`.
5. **Maintain** — PM has it well (●) and it's still worth keeping. Default for ● rows not caught above.
6. If none apply, fall back to **Build** if PriorityScore is in the top third, else **Skip**.

## Calibration check

Before finalizing: your verdicts should spread across at least 4 of the 5 categories. If everything is "Build", you've scored too generously on E/P — re-anchor. If nothing is "Skip", you're being too polite; almost every mature market has futile features (re-read the futile ones critically).
