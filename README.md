# Competitive Feature Matrix — AI Skill for Product Managers (Multi-LLM)

**Competitive feature analysis and feature prioritization, automated.** A portable AI agent skill that researches your competitors, maps their features, scores them, and produces a prioritized, decision-ready **feature comparison matrix** — so Product Managers know what to build next, where they are behind the market, and where the untapped whitespace is.

**Author:** Rafael Felsemburg ([github.com/felsemburg](https://github.com/felsemburg))
**Version:** 1.0
**Works with:** Claude, Claude Code, Perplexity, Manus.ai, Gemini CLI, Cursor, GitHub Copilot, Codex, Amp, Kilo Code, Antigravity, OpenClaw
**License:** use freely within your organization.

> **What is the Competitive Feature Matrix skill?** It is a reusable AI skill (built on the Agent Skills open standard) that runs an end-to-end **competitive analysis** for any digital product — SaaS platform, mobile app, or system. It performs automated competitor research, **feature gap analysis**, and **competitor benchmarking**, then scores every feature on five dimensions and ranks them into a clear *build / fix / differentiate / maintain / skip* table, plus charts and a shareable HTML report. It turns a vague "what should we build and where do we stand?" question into a defensible product prioritization decision.

## Who it is for

Product Managers, product leaders, founders, and product marketers who need a fast, structured answer to **competitive product research** and **product roadmap prioritization** without spending days in spreadsheets. It is written for any experience level: every matrix ships with a plain-language "how to read this" guide, so it is just as usable on your first **feature audit** as your fiftieth.

## What problems it solves

- "What features should we prioritize next?" — turns competitor data into a ranked build list.
- "Where are we behind the market?" — surfaces table-stakes features you are missing.
- "Where is the market whitespace?" — finds high-value features few competitors have built.
- "Which features are futile?" — flags low-value features so you don't waste roadmap on them.
- "Does anyone actually offer this feature?" — validate a specific feature idea against the whole market.
- "Survey the major players in our segment" — automated competitor discovery and **competitive teardown**.

## What it does (workflow)

Given a product and its market segment, the skill:

1. **Scopes** the work — confirms your product, the segment, the core customer problem, the competitors you care about, and any specific feature you want force-validated against the market.
2. **Discovers competitors** across the segment (web + docs + app listings), then **stops and asks you to approve or edit the list** before any analysis — so the most important players for your business are never missed.
3. **Extracts and normalizes** features into comparable, de-duplicated capabilities grouped into clusters.
4. **Scores** every feature on Essential, Adoption, Differentiation, Problem-fit, and Effort, then computes a composite Priority Score and assigns a verdict.
5. **Delivers** a full marked **feature matrix** (every competitor marked per feature, with a one-line description) and a decision view that surfaces what to build, where you're behind, and where the whitespace is.
6. **Saves a self-contained HTML report** — a minimalistic, professional page bundling the summary, the charts, and the full matrix, with an informative date and linked sources. It opens offline (the chart library is inlined), so it's safe to archive and forward to stakeholders. See `examples/returns-management-report-example.html` for a finished sample.

## Key features

- **Prioritized feature scoring** — a transparent five-dimension rubric (Essential, Adoption, Differentiation, Problem-fit, Effort) with a composite Priority Score, so rankings are objective and repeatable.
- **Competitor approval gate** — never analyzes a competitor set you haven't signed off on. Competitor discovery is always incomplete; an unverified list silently distorts every adoption number and verdict.
- **Forced-feature validation** — name a feature you're considering (or already have), and it always gets a row, even at 0% adoption, so you can see exactly who in the market has built it and whether it's genuine whitespace or simply unproven.
- **Decision-ready visuals** — an opportunity quadrant (adoption vs. differentiation) and a priority ranking chart, designed so a PM can decide at a glance.
- **Shareable HTML report** — professional, self-contained, dated, and sourced; ready to send to stakeholders.
- **Portable across LLMs** — one canonical skill, install everywhere (see the table below).

## Common search terms this skill answers

competitive feature matrix · feature gap analysis · competitor feature comparison · product feature prioritization · competitive analysis for product managers · what features to build next · feature comparison table · competitive benchmarking · market whitespace analysis · SaaS competitor research · product roadmap prioritization · competitive teardown · feature audit

## Best-fit warning — read before you pick a tool

This is a **research-and-analysis** skill, not a code-generation skill. Its core work is web research, feature extraction from competitor sites/docs, scoring, and synthesis into a matrix. That means tool fit varies a lot:

**Best fit (native web research + synthesis):**
- **Claude / Claude Code** — strong research, native Skills, renders the decision visual well.
- **Perplexity Computer** — purpose-built for research and multi-model synthesis; arguably the most natural home for this skill.
- **Manus.ai** — autonomous agent with native browser, code execution, and file tools; runs the full research-to-report workflow end to end, including generating the saved HTML report.
- **Gemini CLI** — solid web research and long-context synthesis.

**Works, with caveats (coding-first agents):**
- **Codex, Cursor, GitHub Copilot, Amp, Kilo Code** — these read the skill file fine and will follow the workflow, but they are optimized for working inside a code repository. Their web-research and live-discovery capabilities are typically weaker or depend on configured tools/MCP, so the competitor-discovery phase may be thinner. If you run the skill here, expect to lean more on the "competitors to include" question and to feed in sources yourself.

**Depends on the tool's research tooling:**
- **Antigravity, OpenClaw** — directory-based skill support is native (see below), but research quality depends on what tools/integrations each has enabled. Fit is as good as the agent's ability to browse and read competitor pages.

In short: if the agent can browse the web well, this skill shines. If it's a pure coding agent with no research tooling, it will still produce a structured matrix but the market-discovery half will only be as good as the inputs you give it.

## What's in this pack

```
cfm-pack/
├── README.md                         ← you are here
├── skill/
│   ├── competitive-feature-matrix.skill   ← packaged for Claude's native installer
│   └── competitive-feature-matrix/
│       ├── SKILL.md                  ← the canonical skill (single source of truth)
│       └── references/
│           ├── scoring-rubric.md     ← 0–5 anchors per dimension, composite formula, verdict logic
│           ├── feature-extraction.md ← normalization, canonical naming, clustering
│           ├── output-templates.md   ← matrix format, how-to-read block, decision-view spec
│           └── html-report.md        ← spec for the saved self-contained HTML report
├── examples/
│   └── returns-management-report-example.html  ← finished sample report (opens offline)
└── adapters/                         ← per-tool entry files (see install table below)
    ├── AGENTS.md
    ├── CLAUDE.md
    ├── GEMINI.md
    ├── .cursor/rules/competitive-feature-matrix.mdc
    └── .github/copilot-instructions.md
```

The skill lives in **one** place (`skill/competitive-feature-matrix/`). Tools that use the directory-based `SKILL.md` convention read that folder directly; the rest get a thin adapter in `adapters/` that points back to it. Single source of truth, no duplication.

## Install per tool

| Tool | Reads the skill via | What to do | Fit |
|---|---|---|---|
| **Claude** (claude.ai / app) | Native Skills | Install `skill/competitive-feature-matrix.skill` via Settings → Capabilities → Skills. | Best |
| **Claude Code** | `SKILL.md` (native dir) + `CLAUDE.md` | Drop the `skill/competitive-feature-matrix/` folder into `.claude/skills/` (or `~/.claude/skills/`). Optionally add `adapters/CLAUDE.md` to your project. | Best |
| **Perplexity Computer** | Native Skills (`.md` / `.zip`) | Go to Computer → Skills → **+ Create skill** → upload `SKILL.md` (or zip the skill folder and upload). | Best |
| **Gemini CLI** | `GEMINI.md` | Copy `adapters/GEMINI.md` to repo root and the `skill/` folder alongside it. | Best |
| **Manus.ai** | Native Skills (directory + `SKILL.md`, Agent Skills standard) | In Manus, go to Skills → **+ Add**, then upload `skill/competitive-feature-matrix.skill` (or the folder / a zip of it), or import from GitHub. Trigger with `/competitive-feature-matrix`. No adapter needed — Manus adopted the Agent Skills open standard on 2026-01-27. | Best |
| **Antigravity** | Native Skills (directory + `SKILL.md`) | Place the `skill/competitive-feature-matrix/` directory in Antigravity's skills location. No adapter needed — it loads the `SKILL.md` package directly. | Good (research-tool dependent) |
| **OpenClaw** | Native Skills (directory + `SKILL.md` w/ YAML frontmatter) | Place the `skill/competitive-feature-matrix/` directory as a local skill. OpenClaw loads the `SKILL.md` and filters at load time by environment/config. No adapter needed. | Good (research-tool dependent) |
| **Codex** (OpenAI CLI) | `AGENTS.md` + `SKILL.md` | Copy `adapters/AGENTS.md` to repo root and the `skill/` folder alongside it. | Works (coding-first) |
| **Cursor** | `.cursor/rules/*.mdc` | Copy `adapters/.cursor/rules/competitive-feature-matrix.mdc` into `.cursor/rules/` and the `skill/` folder into the repo. | Works (coding-first) |
| **GitHub Copilot** | `.github/copilot-instructions.md` | Copy `adapters/.github/copilot-instructions.md` into your repo's `.github/`. | Works (coding-first) |
| **Amp** | `AGENTS.md` | Copy `adapters/AGENTS.md` to repo root. | Works (coding-first) |
| **Kilo Code** | `AGENTS.md` | Copy `adapters/AGENTS.md` to repo root. | Works (coding-first) |
| **Any other agent** | `AGENTS.md` fallback | Place `adapters/AGENTS.md` and the `skill/` folder at repo root. AGENTS.md is the cross-tool standard most agents read. | Varies |

All of Antigravity, OpenClaw, Perplexity, and Manus.ai use the same directory-based `SKILL.md` format (the Agent Skills open standard) as Claude Code, so the canonical skill folder installs into them directly with no adapter.

## Frequently asked questions

**What is a competitive feature matrix?**
A competitive feature matrix is a structured table that compares the features of competing products side by side, showing which competitor has which capability and how important each feature is. This skill generates one automatically, then scores and ranks the features so the result is a prioritization decision, not just a comparison.

**How is this different from a manual competitor spreadsheet?**
A manual spreadsheet tells you who has what. This skill goes further: it discovers competitors for you, normalizes feature names so comparisons are fair, scores each feature on five dimensions, computes a Priority Score, assigns a build/fix/differentiate/maintain/skip verdict, and produces charts and a shareable report — in one pass.

**Which AI tools and LLMs does it support?**
Claude, Claude Code, Perplexity, Manus.ai, Gemini CLI, Cursor, GitHub Copilot, Codex, Amp, Kilo Code, Antigravity, and OpenClaw. Tools with native web research (Claude, Perplexity, Manus.ai, Gemini CLI) are the best fit; see the tool table for details.

**Does it work for non-SaaS products?**
Yes. It works for any digital product — SaaS platforms, mobile apps, or internal systems — wherever feature-level comparison drives a build decision.

**Can I make sure my own known competitors are included?**
Yes. The skill asks which competitors you track and always includes them, while still discovering others on its own. It then shows you the full list for approval before any analysis runs.

## How to use it (any tool)

Just ask, in plain language. The skill triggers on requests like:

- "Compare features across competitors for [product] and tell me what to prioritize."
- "Run a feature gap analysis on [segment]."
- "Survey the major players in [market] and rank features into a matrix."
- "Where are we behind the market on [product]?"

It will ask you a few scoping questions (product, segment, competitors to include, any feature to force-validate), show you the competitor list for approval, then produce the matrix and decision view.

## Maintenance

To update the skill, edit only `skill/competitive-feature-matrix/SKILL.md` and its `references/`. The adapters are thin pointers and rarely need changing. If you add a reference file, mention it in `SKILL.md` so every tool picks it up.
