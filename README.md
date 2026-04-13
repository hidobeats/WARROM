# WARROOM v1.0
**Advanced Agentic Brainstorming & Architecture System**

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Version](https://img.shields.io/badge/Version-1.0-green.svg)

WARROOM is an autonomous multi-agent system built to run within your IDE or terminal. It is designed for aggressive "pressure-testing," idea generation, and architectural planning for tech startups. The system emulates a closed-door Board of Directors meeting featuring 7 highly specialized AI agents, each wielding distinct personas, methodologies, and mental frameworks.

Unlike standard chatbots, WARROOM agents are explicitly instructed to be hostile to bad ideas.

---

## 🛡️ The 7 Board Members

1. **The Visionary Founder:** Pushes for 10-year paradigm shifts. Hates incremental software.
2. **The Investor Critic:** Defends the capital. Kills ideas with poor unit economics.
3. **The Analyst:** Demands supply/demand equations and competitive moats.
4. **The Tech Nerd:** Ruthlessly optimizes architecture. Adheres to KISS and hates bloat.
5. **The Creative Producer:** Defines the emotional journey, lore, and "Nintendo Polish" of UX.
6. **The Marketing Genius:** Crafts the viral mechanics, positioning, and prestige.
7. **The Legal & Finance Advisor:** Identifies regulatory loopholes and worst-case compliance scenarios.

---

## ⚙️ Installation & Setup

WARROOM v1.0 is currently a prompt-and-protocol based framework running atop your existing AI IDE or terminal agent (e.g., Cursor, Claude Code, Windsurf, or web interfaces with project context).

**1. Clone the repository:**
```bash
git clone https://github.com/your-username/WARROOM.git
cd WARROOM
```
**2. Setup your AI environment:**
- **For AI IDEs / CLI Agents:** Open the `WARROOM` folder as your root workspace. The AI will automatically read the `.md` files to understand its roles and the framework.
**3. Dependencies:** Zero dependencies out-of-the-box. It relies entirely on your LLM's workspace context.

---

## 🧠 Core Features & Rules

### 1. The Contrarian Protocol (No Yes-Men)
Agents are strictly forbidden from agreeing with the User (CEO) simply because of hierarchy. If an idea is economically unviable, technically absurd, or structurally flawed, agents are legally bound by their prompt to attack it with facts and frameworks. The system thrives on critical friction.

### 2. Blind Evaluation Phase
To prevent LLM autoregressive bias and "groupthink," each session begins with a blind evaluation. Before inter-agent debate begins, every active agent must produce an independent assessment of the CEO's pitch.

### 3. Execution Mode (Trigger Flow)
Agents don't just talk; they execute. But they are leashed. The flow works as follows:
- **Trigger:** Either the **User (CEO) explicitly requests** an artifact (e.g., "*Tech Nerd, show me the schema*"), OR an **agent proactively proposes** it to prove their point (`[ACTION REQUIRED: Let me build a financial model to prove this doesn't work...]`).
- **Approval Gate:** Agents cannot generate scripts or heavy documents autonomously without permission.
- **Execution:** The action is triggered *only* upon explicit approval from the CEO (e.g., "*Approved, do it*").

### 4. The Hive Hub (Global Memory)
- `memory/hive_mind.md` — A global registry storing distilled lessons and conclusions from all past WARROOM sessions. 
- Agents rely on this database to avoid repeating the same historical mistakes across different projects. Raw, searchable session logs are funneled into `memory/archive/`.

### 5. Consensus Gate & Artifact Generation
Once the agents and the CEO achieve alignment, the system closes the debate and generates two defining artifacts inside the project directory: 
- `KEY_DECISIONS.md` (A pure distillation of accepted architecture and business logic)
- `PITCH_DECK.md` (The final project presentation and Go-To-Market strategy)

---

## 🗂️ Directory Architecture

WARROOM enforces strict file hygiene across multiple concurrent projects.

```text
WARROOM/
├── agents/                     # The 7 agent persona .md files (System Prompts)
├── memory/
│   ├── hive_mind.md            # The Global Hive Mind (Universal lessons)
│   └── archive/                # Raw dumps of past Board sessions
├── warroom_protocol.md         # The Rules of Engagement for the Board
│
└── projects/
    └── <project_name>/         # Directory for a specific project
        ├── accepted/
        │   └── <date>/         # Finalized, approved artifacts log
        │       ├── KEY_DECISIONS.md
        │       └── PITCH_DECK.md
        │
        └── ideapath/
            └── <date>/         # Archive of rejected, postponed, or visionary concepts
                └── concept_name.md
```

---

## 🚀 Getting Started (Example Session)

1. Open your AI Assistant interface in the root directory of the `WARROOM`.
2. Issue the starting command: 
   > `"Open the Board of Directors session. Here is my pitch: A decentralized social network for indie musicians..."`
3. **The Initialization:** The system will ask for a **Test Name** and automatically generate the `projects/<test_name>` directory.
4. **Blind Eval:** The 7 agents will output their immediate, unvarnished thoughts on your pitch. (e.g., The *Analyst* points out terrible CAC; the *Visionary* loves the ethos).
5. **The Debate:** You drive them. Defend your thesis. Trigger *Execution Mode* for data. If they deadlock, use the *Tiebreaker Vote*.
6. **The Close:** Once consensus is reached, command: `"Save the session."` The system renames the folder (if a final brand name was chosen), writes the `KEY_DECISIONS.md`, and updates the `hive_mind.md`.

---

## ⚠️ Known Limitations

- **Single-LLM Orchestration:** When running WARROOM within a standard AI chat interface, the LLM roleplays all 7 agents sequentially. This introduces **autoregressive bias** — later agents are influenced by earlier ones, reducing independence. We mitigate this via the *Blind Evaluation Phase*, but true parallelism requires isolated agent contexts. See the **Agent Teams Test** below for a proven solution.
- **Context Window:** Lengthy debates across 7 agents consume tokens rapidly. Distill and save to `projects/` frequently to clear context.

---

## 🧪 Agent Teams Test: Parallel Execution with Zero Cross-Contamination

We ran a full 2-phase WARROOM session using **Claude Code Agent Teams** — where each of the 7 board members runs as an independent parallel agent with its own isolated context window. No shared state, no autoregressive bias, no sequential influence.

This test validates that the WARROOM protocol can achieve **true multi-agent independence** without a custom orchestrator or API costs — running entirely on a standard Claude Code subscription.

### Test Setup

- **Pitch evaluated:** *"An AI platform that generates a complete business plan and financial model for a startup in 5 minutes based on a single idea description. Monetization: $29/month subscription for founders."*
- **Execution environment:** Claude Code CLI with Agent Teams (Claude Opus 4.6)
- **Isolation method:** Each agent spawned as an independent subagent with its own context — physically unable to see other agents' outputs during blind evaluation

### Phase 1: Blind Evaluation (7 Parallel Agents)

All 7 agents evaluated the pitch simultaneously in complete isolation, then wrote their assessments to individual files.

![Phase 1 — Blind Evaluation: 7 agents running in parallel](Claude%20Agent%20Teams%20TEST/phase1_blind_eval_tokens.png)

| Agent | Tool Uses | Tokens | Score |
|-------|-----------|--------|-------|
| Visionary Founder | 2 | 15.5k | 2/10 |
| Investor Critic | 2 | 15.5k | 2/10 |
| Analyst | 3 | 15.6k | 2/10 |
| Tech Nerd | 3 | 15.6k | 7/10 |
| Creative Producer | 3 | 15.7k | 3/10 |
| Marketing Genius | 3 | 15.7k | 3/10 |
| Legal & Finance | 3 | 15.7k | 5/10 |
| **Total Phase 1** | **19** | **~109k** | **Avg: 3.4** |

**Key finding:** 4 out of 7 agents independently arrived at the exact same conclusion — *"this is a feature, not a company"* — through completely different analytical frameworks, with zero cross-communication. This would not happen in a sequential single-LLM run where later agents parrot the framing of earlier ones.

### Phase 2: Structured Debate (7 Parallel Agents)

Each agent received ALL 7 blind evaluations and was asked to respond to specific tensions, challenge other agents, and evaluate proposed pivots.

![Phase 2 — Structured Debate: 7 agents cross-examining each other's positions](Claude%20Agent%20Teams%20TEST/phase2_debate_tokens.png)

| Agent | Tool Uses | Tokens |
|-------|-----------|--------|
| Visionary Founder | 11 | 30.2k |
| Investor Critic | 11 | 30.0k |
| Analyst | 11 | 30.0k |
| Tech Nerd | 13 | 31.4k |
| Creative Producer | 13 | 31.3k |
| Marketing Genius | 11 | 30.0k |
| Legal & Finance | 11 | 30.0k |
| **Total Phase 2** | **81** | **~213k** |

### Results: Score Evolution Across Phases

The board evaluated three scenarios in Phase 2: the original pitch, a Marketing pivot ("AI Startup Validation"), and the Visionary's pivot ("AI Co-Founder Platform").

| Agent | Original (Ph1 → Ph2) | Marketing Pivot | Visionary Pivot |
|-------|----------------------|-----------------|-----------------|
| Visionary Founder | 2 → 3 | — | — |
| Investor Critic | 2 → 2 | 6 | 5 |
| Analyst | 2 → 2 | 5 | 4 |
| Tech Nerd | 7 → 5 | 6 | 7 |
| Creative Producer | 3 → 3 | 6 | 8 |
| Marketing Genius | 3 → 2 | 7 | 5 |
| Legal & Finance | 5 → 4 | 6 | 2 |
| **Average** | **3.4 → 3.0** | **6.0** | **5.2** |

### Total Token Cost

| Phase | Tokens | Duration |
|-------|--------|----------|
| Phase 1 (Blind Eval) | ~109k | ~65s (parallel) |
| Phase 2 (Debate) | ~213k | ~200s (parallel) |
| **Full Session** | **~322k** | **~4.5 min total** |

> [!WARNING]
> **This is expensive.** A single 2-phase session consumes **~322k tokens** — a substantial portion of most subscription quotas. Running multiple sessions per day is impractical at this cost. The results are impressive, but the token efficiency needs serious work before Agent Teams mode is viable for regular use.
>
> **We need your help.** If you have ideas on how to reduce token consumption without sacrificing evaluation quality — whether through smarter prompt compression, selective agent activation, tiered evaluation (fewer agents in Phase 1, full board only when needed), smaller model routing, or a fundamentally different architecture — **contributions are very welcome.** See [CONTRIBUTING.md](CONTRIBUTING.md) and the optimization goals in the Roadmap below.

### What This Proves

1. **Autoregressive bias is eliminated.** Agents in isolated contexts produce genuinely independent evaluations — no sequential contamination.
2. **Natural convergence validates the protocol.** Independent agents reaching the same conclusion through different frameworks is a stronger signal than sequential agreement.
3. **Natural divergence surfaces unique insights.** The Tech Nerd's 7/10 vs the business board's 2-3/10 revealed a feasibility-viability gap that sparked productive debate in Phase 2.
4. **The protocol works without a custom orchestrator.** Claude Code Agent Teams provide true parallel execution using the existing subscription — no Python/Node wrapper or API keys required.
5. **Emergent strategy is greater than any single agent.** No individual agent proposed the final board recommendation. It emerged from cross-pollination: Marketing's repositioning + Creative's brand vision + Analyst's phased economics + Tech's architecture + Legal's constraints = a strategy none could have produced alone.

> Full test artifacts (all 14 evaluation files + summary) are available in [`Claude Agent Teams TEST/`](Claude%20Agent%20Teams%20TEST/).

---

## 🛣️ Roadmap

- [x] **Parallel Agent Execution via Agent Teams:** Validated using Claude Code Agent Teams — 7 truly isolated agents running in parallel with zero cross-contamination. No custom orchestrator needed.
- [ ] **Token Optimization (Help Wanted):** The current Agent Teams approach works but burns ~322k tokens per session. We need contributors to help bring this down significantly. Potential directions:
  - Prompt compression — shorter persona prompts that preserve agent behavior
  - Selective activation — smart routing to activate only 3-4 relevant agents per pitch instead of all 7
  - Tiered evaluation — quick pre-screen with fewer agents, full board only for promising ideas
  - Smaller model routing — use cheaper/faster models for initial evaluation, premium models for debate
  - Incremental context — avoid re-sending full evaluations in Phase 2, use diffs or summaries
  - Hybrid approach — combine single-LLM sequential for low-stakes phases with parallel for blind eval only
- [ ] **Python/Node Orchestrator API:** A dedicated CLI tool for environments without Agent Teams support, spawning isolated parallel API calls for each agent.
- [ ] **Automated GitHub Integration:** Allow the *Tech Nerd* to automatically open tracking issues for MVP features decided upon in `KEY_DECISIONS.md`.
- [ ] **Custom Persona Loader:** Easy JSON/YAML support for loading custom industry-specific agents (e.g., *FDA Compliance Auditor*).

---

## ❓

**Can I fire an agent mid-session?**
Yes. You are the CEO. Command: *"Silence the Legal Advisor for the rest of this session, keep the other 6."* The system will dynamically adjust.

**Contributions:**
Please see `CONTRIBUTING.md` if you wish to add new personas or improve the framework!
