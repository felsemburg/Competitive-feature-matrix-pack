# CLAUDE.md

> Author: Rafael Felsemburg · Skill: Competitive Feature Matrix v1.0

@AGENTS.md

## Competitive Feature Matrix skill

This project bundles the Competitive Feature Matrix skill at
`skill/competitive-feature-matrix/SKILL.md`.

In Claude Code, this is a native skill — if the folder is in your skills path
(project `.claude/skills/` or `~/.claude/skills/`), it triggers automatically on
competitive-feature-analysis requests. Otherwise, read `SKILL.md` and follow it
when the user wants to map, compare, score, and rank features across competitors.

Key behaviors that must not be skipped: the scoping questions, the mandatory
competitor-list approval gate before any feature analysis, the plain-language
"how to read this" block above the matrix, and forced-feature rows (a feature the
user asks to validate always appears, even at 0% adoption).
