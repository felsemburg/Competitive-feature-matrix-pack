# AGENTS.md

> Author: Rafael Felsemburg · Skill: Competitive Feature Matrix v1.0

This repository includes a portable skill for competitive feature analysis of digital products.

## Competitive Feature Matrix skill

When the user asks to compare competitor features, run a feature gap analysis, decide what to build next, survey the major players in a product segment, or otherwise map and rank features across competing products into a decision-ready matrix — load and follow the instructions in:

`skill/competitive-feature-matrix/SKILL.md`

and its reference files in `skill/competitive-feature-matrix/references/`.

Follow that skill's workflow exactly, including:

- Asking the scoping questions first (product, segment, core customer problem, competitors to include, and any feature to force-validate).
- Presenting the discovered competitor list and **waiting for the user's approval or edits before analyzing any features**. This gate is mandatory — do not proceed to feature extraction on a competitor set the user hasn't confirmed.
- Producing both the full marked matrix (every competitor marked per feature, with a one-line description and a plain-language "how to read this" block) and the decision view.
- Forcing any user-requested feature into the matrix as its own row even at 0% adoption.

Do not summarize or paraphrase the skill from memory — read the file and follow it, because the scoring rubric and output format are precise.
