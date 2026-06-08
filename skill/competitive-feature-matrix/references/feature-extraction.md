# Feature Extraction & Normalization

Read before Phase 3. The job here is turning a dozen marketing pages full of inconsistent jargon into one clean, comparable feature list. Garbage normalization produces a matrix where the same capability appears three times under different names and adoption numbers are meaningless.

## Where to read features from (in priority order)

1. **Docs / help center** — most accurate, least marketing spin. What's documented usually exists.
2. **Feature/product pages** — good coverage, but watch for vaporware and "coming soon".
3. **Pricing pages** — reveal which features are gated to which tier (useful signal for the PM's own packaging later).
4. **App-store / marketplace listings** (Shopify App Store, etc.) — good for the relevant platform, plus reviews reveal what users actually use vs. what's advertised.
5. **Review sites (G2/Capterra)** — the "most/least liked" and "feature request" sections are gold for problem-fit and futility signals.

Prefer documented capabilities over marketing claims. If only the marketing page asserts something and docs don't mention it, mark it partial (◐) and note the uncertainty.

## Canonical naming

Different vendors name the same thing differently. Collapse them to ONE canonical feature name. Method:

- Name the feature by **what it does for the customer**, not the vendor's brand term. "Smart Exchange Engine™" → "Variant/product exchanges".
- Keep names short and concrete. "Automated return rules" not "Powerful no-code automation workflow builder".
- When two features overlap ~80%, merge them and note the variation in the description.
- When a "feature" is really a bundle (e.g. "Analytics" covering 6 distinct reports), decide: split only if competitors differ meaningfully on the sub-parts. Otherwise keep it as one row.

Keep a synonym log as you go so the same canonical name is applied consistently:

```
Canonical: Self-service return portal
  aka: RMA portal, returns center, branded return page, customer return portal
```

## Clustering

Group features into 5–8 capability clusters so the matrix is scannable. Clusters are segment-specific — derive them from the features you find, don't force a generic taxonomy. For a returns-management product, clusters tend to be: Customer-facing flow, Automation & rules, Logistics & labels, Exchanges & retention, Analytics & reporting, Integrations, Admin & branding. For a different segment they'll differ. Aim for clusters of roughly 3–8 features each; a cluster with one feature probably belongs inside another.

## Marking presence per competitor

For each (feature, competitor) cell:
- **✓** — confirmed present (seen in docs/feature page/listing).
- **◐** — partial: exists but limited, gated to top tier only, or marketing-only with no doc confirmation.
- **✗** — confirmed absent (you looked and it's not there).
- **?** — couldn't verify either way. Use sparingly; too many `?` weakens the adoption math. Try one more targeted search before settling on `?`.
- **●** — reserved for the PM's OWN product, so it stands out in the row. Use ●/◐●/✗ logic the same way for them.

## Futility signals (feeds the "Skip" verdict)

Watch for features that are common but low-value, so you can flag them honestly:
- Mentioned in marketing but absent from "most liked features" and never in user reviews.
- Present across many competitors yet correlated with no buying decision (checkbox features).
- Solve a problem the segment's customers don't actually have (over-engineering).
- Heavy config burden for marginal benefit.

Note these as you extract — don't reconstruct them from memory at scoring time.
