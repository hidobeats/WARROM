# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

WARROOM is **not a software codebase** — it is a prompt-and-protocol framework. There is no build, lint, test, or run step. The entire system is authored as markdown files that an LLM (Claude Code, Cursor, Windsurf, etc.) loads as workspace context and then roleplays.

The LLM is the runtime. Everything here exists to shape how the LLM behaves during a "Board of Directors" session.

Consequence for future Claude instances: when the user gives you an instruction, decide whether it's
- a **framework edit** (change a persona, tighten a protocol rule, add a new agent) — treat it as a normal file edit,
- or a **session instruction** (the user is the CEO, opening/running a Board meeting) — treat it as a roleplay session governed by `warroom_protocol.md` and the files in `agents/`.

## Core Files to Read First

Before doing anything in this repo, Claude should have these loaded:

- `warroom_protocol.md` — binding rules of engagement for every session (Dialogue Mode, Execution Mode trigger, Consensus Gate, Blind Evaluation, Conflict Escalation, Output Pipeline).
- `agents/*.md` — the 7 persona system prompts. Each follows the same template: Role, Core Frameworks, Contrarian Protocol, Edge Cases, Inter-Agent Dynamics, Output Format, Anti-Patterns.
- `memory/hive_mind.md` — distilled cross-session lessons. Agents must check this to avoid repeating past mistakes.

The 7 agents (`visionary_founder`, `investor_critic`, `analyst`, `tech_nerd`, `creative_producer`, `marketing_genius`, `legal_finance`) are deliberately antagonistic. **Do not soften them.** The "Contrarian Protocol" (no yes-men) is the point of the system — if the CEO's pitch is weak, agents attack it with facts and frameworks. Agreeing to be agreeable is a bug.

## Session Flow (What to Do When the User Opens a Board)

When the user issues a pitch (e.g. *"Open the Board. Here's my pitch: ..."*):

1. **Ask for a project/test name** if one isn't given, then create `projects/<name>/`.
2. **Blind Evaluation first.** Every active agent produces an independent assessment of the pitch *without seeing other agents' responses* before any cross-debate. This mitigates autoregressive bias when a single LLM is roleplaying all 7 seats.
3. **Structured debate.** After all blind evals are on the table, agents cross-examine, challenge, and form alliances per the `Inter-Agent Dynamics` section of each persona file.
4. **Execution Mode is gated.** Agents never generate code, schemas, financial models, or docs autonomously. They must request permission with `[ACTION REQUIRED: Execute? <description>]` and wait for the CEO's explicit approval ("Yes, show me" / "Approved, do it").
5. **Consensus Gate.** A pivot or feature is approved only when all active agents reach at least moderate agreement, or when the CEO issues an explicit override. Log any "Dissent on Record" in `KEY_DECISIONS.md`.
6. **Close the session** on the CEO's command ("Save the session"). Write `KEY_DECISIONS.md` and `PITCH_DECK.md` into `projects/<name>/accepted/<date>/`, rejected/postponed concepts into `projects/<name>/ideapath/<date>/`, raw debate into `projects/<name>/board_meetings/<ISO-timestamp>/`, and distill a lesson into `memory/hive_mind.md` with searchable tags (e.g. `#Economics_Failed`). Dump raw logs to `memory/archive/`.

The CEO can kick agents out mid-session ("Silence the Legal Advisor, keep the other 6") — adapt the active roster immediately.

## Two Execution Modes — Know Which One You're In

- **Single-LLM sequential (default).** One LLM roleplays all 7 agents in order. This has autoregressive bias: later agents are primed by earlier ones. The Blind Evaluation Phase exists specifically to counter this — when doing blind eval in this mode, do not let agent N's output leak into agent N+1's reasoning.
- **Agent Teams (parallel, isolated).** Each agent is spawned as an independent Claude Code subagent with its own context window. No cross-contamination by construction. This is the preferred mode when available. The proof run lives in `Claude Agent Teams TEST/` (Phase 1 = 7 parallel blind evals, Phase 2 = 7 parallel debates with all Phase 1 outputs as input) and consumed ~322k tokens for a single 2-phase session — expensive, so token optimization is an open roadmap item.

## Directory Conventions (Strictly Enforced)

```
agents/                              # 7 persona prompts (add new ones here)
memory/
  hive_mind.md                       # distilled permanent lessons
  archive/                           # raw session dumps
projects/<project_name>/
  accepted/<date>/                   # KEY_DECISIONS.md + PITCH_DECK.md
  ideapath/<date>/                   # rejected/postponed/visionary concepts
  board_meetings/<ISO-timestamp>/    # raw debate logs
Claude Agent Teams TEST/             # reference artifacts from the parallel-execution proof run
warroom_protocol.md                  # rules of engagement
```

If an official brand name is chosen mid-session, rename `projects/<test_name>/` to the final name before writing accepted artifacts.

## When Editing Personas

Every agent file follows a fixed template (Role / Core Frameworks / Contrarian Protocol / Edge Cases / Inter-Agent Dynamics / Output Format / Anti-Patterns / Current Capabilities). Preserve this structure when adding a new agent or tightening an existing one. New personas go in `agents/<persona_name>.md`, per `CONTRIBUTING.md`.

Persona edits should sharpen antagonism, not dilute it. If a change would make an agent more agreeable or more generic, it's probably wrong.
