# Contributing to WARROOM

First off, thank you for considering contributing to the WARROOM framework! The strength of this system relies on diverse mental models, aggressive "pressure testing," and structural polish.

## How to Contribute

There are several ways you can contribute to this project:

### 1. Propose a New Agent
Have an idea for an 8th or 9th persona? We welcome new agents (e.g., The Ethicist, The Hacker, The Anthropologist).
- Create a new `{persona_name}.md` in the `agents/` directory.
- Follow the standard template: Role, Core Frameworks, Contrarian Protocol, Edge Cases, Inter-Agent Dynamics, Output Format, Anti-Patterns.
- Submit a Pull Request with a brief explanation of why the Board of Directors needs this voice.

### 2. Improve Existing Personas
Feel like the Tech Nerd is too soft? Or the Visionary lacks specific mental models? 
- Submit a Pull Request updating the specific agent's `.md` file. Add new frameworks or tighten the prompt instructions to make them more rigorous.

### 3. Expand the Hive Mind
We encourage sharing anonymized, structural lessons in `memory/hive_mind.md`. 
- If you've run a WARROOM session and discovered a universal truth about SaaS pricing, architecture, or onboarding, add it to the Hive Mind so other boards don't make the same mistakes.

### 4. Build an Orchestrator
The core repository relies on manual prompt execution or IDE features. If you write a Python (`langchain`/`autogen`) or Node.js orchestrator that automatically runs the 7 agents in parallel for the **Blind Evaluation Phase**, please submit it! We will gladly include it in a `/scripts/` directory.

## Pull Request Process

1. Fork the repo and create your branch from `main`.
2. If you've updated `README` or Documentation, ensure your prose is clear, professional, and entirely in English.
3. Submit the PR! A core maintainer will review it. (Prepare for the maintainer to channel the "Investor Critic" to evaluate your PR!).

## Code of Conduct
While the AI agents are encouraged to be aggressive and contrarian, the human contributors must be respectful. No personal attacks, harassment, or toxic behavior will be tolerated in the issues or PR discussions.
