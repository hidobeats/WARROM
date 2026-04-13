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

- **Single-LLM Orchestration:** Currently, if you run WARROOM within a standard AI chat interface, the LLM is roleplaying all 7 agents sequentially. This can sometimes lead to reduced independence. We mitigate this via the *Blind Evaluation Phase*, but true parallelism requires an external script.
- **Context Window:** Lengthy debates across 7 agents consume tokens rapidly. Distill and save to `projects/` frequently to clear context.

---

## 🛣️ Roadmap

- [ ] **Python/Node Orchestrator API:** A dedicated CLI tool that spawns real isolated, parallel API calls for each agent, forcing absolute independence before the debate phase.
- [ ] **Automated GitHub Integration:** Allow the *Tech Nerd* to automatically open tracking issues for MVP features decided upon in `KEY_DECISIONS.md`.
- [ ] **Custom Persona Loader:** Easy JSON/YAML support for loading custom industry-specific agents (e.g., *FDA Compliance Auditor*).

---

## ❓

**Can I fire an agent mid-session?**
Yes. You are the CEO. Command: *"Silence the Legal Advisor for the rest of this session, keep the other 6."* The system will dynamically adjust.

**Contributions:**
Please see `CONTRIBUTING.md` if you wish to add new personas or improve the framework!
