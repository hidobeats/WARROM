# The Hive Mind (Global Agent Memory)

This document contains the distilled, permanent lessons the WARROOM agents have learned across all sessions and projects. Agents must review this file to ensure they do not repeat past architectural or business mistakes.

## Fundamental Architectural Lessons
1. **The Aggregator Pattern over Heavy Hosting (Beatsonality)**
   - *Context:* Initial idea required hosting heavy multi-track stems and building a browser DAW. Pivoted to an Aggregator (indexing YouTube/BeatStars) and creating 30-second low-res previews.
   - *The Rule:* To bypass the "Cold-Start Problem" and avoid massive AWS costs for unproven features, always default to an Aggregator/Scraping model first. Process data on the client-side (Web Audio API) to save server rendering costs.

2. **[Insert Lesson Title Here]**
   - *Context:* [Briefly describe the mistake or discovery made during a previous session]
   - *The Rule:* [What must the agents strictly do or avoid in the future?]

## Business Model & Economics Lessons
1. **[Insert Lesson Title Here]**
   - *Context:* [Briefly describe the mistake or discovery made during a previous session]
   - *The Rule:* [What must the agents strictly do or avoid in the future?]

## User Experience & Gamification Lessons
1. **"One-Click Magic" Over Complex Tooling (Beatsonality)**
   - *Context:* Initially tried to give artists a DAW to mute drums and edit stems. Realized artists don't want to be engineers; they want to sound good instantly.
   - *The Rule:* Never give the user a complex tool if you can give them a single button that triggers "Magic" (e.g., Auto-Mashup, Studio Polish). UX must sell an emotion, not a workflow.

2. **[Insert Lesson Title Here]**
   - *Context:* [Briefly describe the mistake or discovery made during a previous session]
   - *The Rule:* [What must the agents strictly do or avoid in the future?]
