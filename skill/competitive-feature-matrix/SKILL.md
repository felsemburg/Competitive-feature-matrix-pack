---
name: competitive-feature-matrix
description: Conduct competitive feature research for a digital product (SaaS platform, app, or system) and produce a prioritized feature matrix. Use this whenever a Product Manager wants to map, compare, group, score, and rank features across competing products to decide what to build, where they have gaps, and where the market whitespace is. Triggers include "compare features across competitors", "what features should we prioritize", "feature gap analysis", "competitive teardown", "survey the major players", "feature matrix", "where are we behind the market", or any request to evaluate a product segment's feature landscape and turn it into a build-prioritization decision. Use it even when the PM only says "research competitors for [product]" without naming the matrix explicitly, as long as the intent is feature-level comparison rather than pricing or positioning alone.
---

# Competitive Feature Matrix

Turn a fuzzy "what should we build / where do we stand" question into a scored, decision-ready feature matrix for a digital product. The output is a ranked table where every feature is scored on how essential it is to the segment, how widely competitors have it, how much it differentiates, and how well it solves the real customer problem — plus a clear "build / fix / ignore" recommendation per feature.

You are doing this FOR a Product Manager. They don't need feature definitions explained back to them. They need a defensible ranking they can act on this week. Be opinionated. A matrix that says "everything is medium priority" is a failed matrix.

## Workflow

Run these phases in order. Don't skip the scoping questions even if you think you can infer the answers — a wrong segment definition poisons the whole matrix.

### Phase 1 — Scope (ask, don't assume)

You need three things locked before researching. If any is unclear from the conversation, ask. Bundle the questions into one turn; don't interrogate one at a time.

1. **The product** — what is the PM's own product, and its URL if they have one. You score the market relative to *their* product, so you need to know what it is.
2. **The segment** — the specific category and customer. "Returns management for Shopify merchants" is a usable segment. "E-commerce tools" is not — too broad to produce a sharp matrix. Narrow it until features are comparable across players.
3. **Known competitors** — ask which competitors they already track. This does NOT replace your own market discovery; you will still find players they didn't name. It ensures you don't miss the ones they care about. Frame it as: "Which competitors should I be sure to include? I'll research the market independently and add others I find."

Also confirm the **customer's core problem** in one sentence. Every feature later gets scored partly on how well it solves *this*. If the PM hasn't stated it, infer a draft and have them confirm.

**Ask about forced-include features.** Before researching, ask the PM: "Is there a specific feature you want me to force into the matrix — something you're considering building, or already have, and want validated against the market?" This turns the matrix into a validation tool: even if no competitor ships the feature (adoption 0%), it still gets its own row so the PM can see exactly who has it, who doesn't, and whether it's whitespace or a solved problem. A forced feature is never dropped during the "don't pad the matrix" pruning in Phase 3 — it always appears, even at 0% adoption, because its absence across competitors is itself the answer the PM wanted. Mark forced rows clearly (e.g. a ★ before the feature name) so they're easy to find.

If the PM already gave you all of this in their message, skip straight to Phase 2 and just state your understanding in one line before proceeding.

### Phase 2 — Discover competitors

Default depth: **8–12 competitors** (web search + their docs/feature pages). Combine the PM's named list with your own discovery. Find players via: segment search ("best [segment] software"), review aggregators (G2, Capterra, app-store category pages for the relevant platform), and "alternatives to [known competitor]" searches.

For each competitor capture: name, URL, rough tier/positioning (budget / mid / enterprise), and where you'll read features from (pricing page, feature page, docs, app listing).

**Mandatory approval gate — stop here.** Before extracting a single feature, present the full mapped competitor list back to the PM and explicitly ask them to approve, add, or remove. Discovery is never complete — your search will miss players the PM cares about, and a missing competitor silently distorts every adoption percentage and verdict in the final matrix. So do not proceed past this point on your own. Show the list as: name — tier — one-line positioning, fold in the competitors the PM named in Phase 1, and ask a direct question like "Here's who I'll analyze. Anyone to add or drop before I dig into features?" Wait for their answer. Only after they confirm do you move to Phase 3.

When the PM names a competitor you hadn't found, add it and research it like any other — their domain knowledge is a feature of the process, not an interruption to it. Don't burn 30 searches before reaching this gate.

### Phase 3 — Extract features

For each competitor, pull the actual feature list from their site/docs/app listing. Normalize names — different vendors call the same thing different things ("RMA portal" vs "self-service returns page" → one canonical feature). Group features into capability clusters (e.g. for returns: Customer-facing flow, Automation/rules, Logistics/labels, Analytics, Integrations, Exchange/retention). Read `references/feature-extraction.md` for normalization rules and the canonical-naming method.

Keep a running master feature list. A feature enters the matrix once at least one competitor has it OR the PM's product has it.

### Phase 4 — Score

Score every feature on the dimensions below. The scoring rubric, the exact 0–5 anchors for each dimension, and the composite-score formula live in `references/scoring-rubric.md` — read it before scoring so the numbers are consistent and defensible. Summary of dimensions:

- **Essential (E)** — table stakes for the segment. Is this a feature a buyer expects by default?
- **Adoption (A)** — what share of researched competitors ship it. Computed, not guessed.
- **Differentiation (D)** — how much having it (or doing it well) sets a product apart. High adoption usually means low differentiation.
- **Problem-fit (P)** — how directly it solves the customer's stated core problem.
- **Effort (X)** — rough build/fix cost for the PM's team (ask the PM for their team size/constraints; default to a small team unless told otherwise). This is the only dimension where lower is better for prioritization.

The composite **Priority Score** combines these (formula in the rubric). Each feature also gets a **verdict**: `Build` (essential gap), `Fix` (have it but weak), `Differentiator` (whitespace worth owning), `Maintain` (have it, fine), or `Skip` (futile/low-value — and yes, the matrix must explicitly flag futile features; PMs need to know what NOT to do as much as what to do).

### Phase 5 — Visualize and deliver

Produce TWO things:

1. **The full feature matrix** — a table with one row per feature. Columns: Feature | Cluster | one-line description | a marked cell per competitor (✓ has it / ◐ partial / ✗ no / ● the PM's own product) | E | A% | D | P | X | Priority Score | Verdict. The per-competitor marks and the brief description are mandatory — the PM asked for both explicitly. Sort by Priority Score descending. The matrix MUST be preceded by a plain-language "How to read this matrix" block so a PM at any experience level can use it without prior context — see `references/output-templates.md` for the exact wording. Don't assume the reader knows what E/A/D/P/X mean.

2. **A decision view** — a compact visual that lets the PM decide in seconds, not minutes. Use the `visualize` tool to render an interactive matrix/quadrant (differentiation vs. adoption, sized by problem-fit, colored by verdict). If `visualize` isn't available, build a self-contained HTML artifact. The decision view must surface the three things the PM cares about equally: what to build next (high-priority gaps), where they're behind (competitors have it, they don't), and the whitespace (low adoption + high problem-fit = nobody's nailed this yet). Read `references/output-templates.md` for the exact table format and the decision-view spec.

3. **A saved HTML report** — always produce a single, self-contained, professional HTML page that bundles the head explanation, the charts, and the full matrix into one shareable, archivable document. This is the artifact the PM keeps and sends to stakeholders. Read `references/html-report.md` for the full spec; the essentials are: a header block with the segment title plus an informative metadata bar (subject product, competitor count, feature count, and the preparation date), the bottom-line summary and top moves, the opportunity-quadrant and priority-ranking charts, the complete marked matrix with its how-to-read block, and a footer listing all sources (with links) and a dated provenance note. The page must be minimalistic, elegant, and self-contained — inline the chart library rather than linking a CDN so the report still works offline and years later. Save it to the outputs location and present it as a downloadable file.

Lead the written summary with the top 3–5 actions, not methodology. Methodology goes at the bottom or in a collapsed section.

## Hard rules

- **Be decisive.** Force a spread in scores. If your matrix is all 3s and 4s, your anchors are wrong — recalibrate against the rubric.
- **Mark every competitor in every row.** A blank cell is ambiguous; use ✗ for confirmed-absent and `?` only when you genuinely couldn't verify.
- **Flag futile features explicitly.** The "Skip" verdict is a first-class output, not an afterthought.
- **Cite where features came from** when claims are non-obvious, so the PM can verify.
- **Adoption is computed**, never estimated by vibe — it's (competitors with feature / total researched).
- **Don't pad the matrix.** 20–40 well-chosen features beat 80 noisy ones. Merge near-duplicates ruthlessly.

## Reference files

- `references/scoring-rubric.md` — 0–5 anchors per dimension, composite formula, verdict logic. Read before Phase 4.
- `references/feature-extraction.md` — normalization, canonical naming, clustering. Read before Phase 3.
- `references/output-templates.md` — exact matrix table format and decision-view spec. Read before Phase 5.
- `references/html-report.md` — spec and structure for the saved, self-contained HTML report. Read before Phase 5.
