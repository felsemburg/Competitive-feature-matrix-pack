# HTML Report

Read before Phase 5. Every run of this skill ends with one saved, self-contained HTML page that the PM can keep, open offline, and forward to stakeholders. It is the durable artifact; the chat output is the conversation, this file is the deliverable.

## Non-negotiables

- **Self-contained.** One `.html` file. Inline the chart library (e.g. paste Chart.js into a `<script>` tag) rather than linking a CDN, so the report renders offline and still works years later. No external JS/CSS dependencies. Web fonts via a stylesheet link are acceptable (they degrade gracefully to serif/mono fallbacks); everything load-bearing must be inline.
- **Minimalistic and professional.** Editorial, calm, print-like. Generous whitespace, a clear type hierarchy, restrained color (use the verdict colors as the only strong accents). No dashboard chrome, no gradients-on-white AI look. It should read like a research brief, not a SaaS landing page.
- **Informative date and sources.** A preparation date appears in the header metadata AND the footer. The footer lists every competitor analyzed as a named link, plus a one-line provenance note stating how feature presence was verified and as of when.
- **Renders without a code bug.** Apply the same chart-rendering rules from `output-templates.md` (draw after layout, fail to a visible message + the table rather than a blank canvas). Because the library is inlined, it's present by definition — but still guard the draw call.

## Page structure (top to bottom)

1. **Header** — an eyebrow label ("Competitive Feature Matrix"), the segment as the H1 title, and a metadata bar with: subject product, number of competitors analyzed, number of features mapped, and the preparation date.
2. **Bottom line** — the 2–3 sentence summary, then the top 3–5 moves as a numbered list.
3. **Opportunity map** — a "how to read" line, the verdict legend, and the adoption-vs-differentiation bubble chart (bubble size = problem-fit, color = verdict).
4. **Priority ranking** — the horizontal bar chart of top features by priority score, colored by verdict.
5. **Full matrix** — a symbols/scores "how to read" block, then the complete table: one row per feature, every competitor marked plus the PM's own product column accented, the five scores, the composite score, and the verdict badge. Sorted by score descending. Allow horizontal scroll for wide competitor sets; rotate competitor column headers to keep it compact.
6. **Footer** — a short "note on visibility" disclaimer, sources (named links to each competitor), the dated provenance note, and a generation line crediting the skill and the date.

### The visibility disclaimer (required)

The footer must include a brief, clearly-set-apart disclaimer (e.g. an accent-bordered callout titled "A note on visibility"), spanning the full page width like the rest of the content (no narrower max-width cap), making this point: the results reflect what an AI could find about each competitor online, which is shaped by how well each company surfaces its features for language models (its GEO / generative-engine-optimization footprint). A feature marked absent or partial may simply be poorly documented or hard for an LLM to discover rather than truly missing. Frame the flip side as an opportunity: if the PM's own platform has capabilities that appear thin in the report, that is a signal to improve how those features are promoted — clearer docs, feature pages, structured descriptions — so they grow more visible to LLMs over time. This protects the PM from over-reading a thin row as a real gap, and turns the report into a prompt to improve their own GEO.

### Attribution link

In the generation line, link the phrase "Competitive Feature Matrix skill" to the author's repository: `https://github.com/felsemburg`. Keep the author credit (Rafael Felsemburg) and the date alongside it.

## Build method

Generate the HTML programmatically from the scored feature data (e.g. a short script that takes the rows + metadata and emits the file) so the table, charts, and footer all draw from one source of truth and stay consistent. Don't hand-write 40 table rows. Save to the outputs directory and present the file for download. If a forced feature (★) is present, keep its row and prefix it in the report too.

## Styling guidance

- Type: a distinctive serif for headings/body (e.g. Fraunces / Newsreader) and a mono for labels, scores, and metadata (e.g. IBM Plex Mono). Avoid Inter/Roboto/Arial. Provide system fallbacks.
- Color: a warm paper background, near-black ink, a single muted accent for the eyebrow/links/own-product column, and the five verdict colors for badges, legend, and chart series. Keep badges as soft tinted pills (color at ~10% alpha background, full-strength text).
- Marks: color the cells — green ✓, amber ◐, red ✗, accent ● for the PM's product — so presence/absence reads at a glance.
- Layout: a centered column that uses most of the page width (max ~1600px) with responsive side padding (e.g. `clamp(16px,4vw,56px)`), so wide screens are well used and narrow ones stay comfortable. The summary and the rest of the content use the full column width. Let the matrix table scroll horizontally inside a bordered card.
- How-to blocks: present each "how to read" explainer as a titled card with its points on separate lines (a heading plus a bulleted list), not a single run-on sentence. Use a block-level container (`<div>`, not `<p>`) for these — a `<ul>` inside a `<p>` is invalid HTML and browsers will eject the list from the styled box, so it must be a div.
- Legend: stack the verdict legend items vertically, one per line, rather than wrapping them inline — it's easier to scan.
- Rotated table headers: give the rotated competitor-name headers generous height and bottom padding (e.g. height ~128px with ~16px bottom padding) so the titles never overlap the first row of cells.
- A subtle drop cap on the summary and numbered move markers add polish without clutter; use sparingly.
