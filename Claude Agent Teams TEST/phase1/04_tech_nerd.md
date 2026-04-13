# Blind Evaluation: The Tech Nerd

## Verdict: FEASIBLE

## Core Assessment

Let me strip this down to what it actually is from an engineering perspective: a prompt-chaining wrapper around an LLM API that takes unstructured text input and produces structured document output (business plan + financial model). That is it. No custom model training, no novel inference pipeline, no distributed compute. You are building a sophisticated prompt template engine with a nice frontend. And honestly? That is fine. The best products are often embarrassingly simple under the hood.

The core technical challenge here is not "can we do this" -- it absolutely can be done -- but "can we do this well enough that the output is not garbage." Business plans have a known structure: executive summary, market analysis, competitive landscape, go-to-market, team, financials. Financial models require assumptions, revenue projections, cost structures, unit economics. An LLM can generate all of this given a decent prompt chain. The real question is whether the output quality at $29/month crosses the "good enough" threshold versus a founder spending two hours with a template and ChatGPT directly. That is a product question, not a technical one. Technically, you can ship an MVP of this in two weeks with one engineer.

The architecture is dead simple for MVP: a Next.js or plain React frontend, a thin backend (Node or even serverless functions), and OpenAI/Anthropic API calls with structured output parsing. You do not need a database beyond user auth and saved plans. You do not need Redis. You do not need Kubernetes. You do not need a vector database. If anyone on the team suggests RAG for the MVP, I am walking out. The "5 minutes" claim is achievable -- a series of 4-6 chained LLM calls with structured JSON output, each taking 10-30 seconds depending on model and output length, parallelized where possible. Total wall clock time: 2-3 minutes realistically, which is under the promised 5.

Where I get nervous is the financial model generation. Text output is forgiving -- a slightly wrong paragraph still reads fine. Numbers are not forgiving. If your model projects $50M ARR in year 2 for a local dog-walking app, you lose all credibility instantly. You need guardrails: industry benchmark databases (static data, not AI-generated), sanity checks on financial assumptions, and probably a structured calculation layer that takes LLM-generated assumptions and runs deterministic math on them rather than letting the LLM do arithmetic. LLMs are notoriously bad at math. Do not let them do math. Extract assumptions, run them through actual formulas.

## Technical Feasibility

**Architecture (MVP):**
- Frontend: React/Next.js. Static marketing pages + authenticated app. Nothing exotic.
- Backend: Serverless functions (Vercel/AWS Lambda) or a lightweight Node server. Stateless request handlers that orchestrate LLM calls.
- LLM Layer: OpenAI GPT-4o or Claude Sonnet as the backbone. Structured output mode (JSON) for financial assumptions. Chain 4-6 prompts: (1) idea expansion + market sizing, (2) competitive analysis, (3) business model + GTM, (4) financial assumptions extraction, (5) executive summary. Parallelize steps 1-3 where possible.
- Financial Engine: Deterministic. LLM outputs assumptions (TAM, conversion rates, pricing, growth rate, burn rate). A plain TypeScript function takes those assumptions and computes projections, unit economics, cash flow. No LLM math.
- Database: Postgres via Supabase or PlanetScale. Users, plans, subscription status. Stripe for billing. Standard boring stack.
- Export: Generate PDF via a library like Puppeteer/Playwright rendering an HTML template, or use a dedicated PDF library. Excel export for financial models via a library like ExcelJS.

**Cost Estimation (per user per generation):**
- GPT-4o at ~$2.50/1M input tokens, ~$10/1M output tokens. A full business plan generation might consume ~15K input tokens and ~8K output tokens across all chained calls. That is roughly $0.04-$0.08 per generation if using GPT-4o. With Claude Sonnet, similar ballpark.
- At $29/month, even if a user generates 20 plans per month (unlikely -- most will generate 2-5), your per-user API cost is $0.80-$1.60/month. Gross margins above 90%. The unit economics work.
- Infrastructure: Vercel Pro ($20/month) or equivalent. Supabase free tier to start. Total infra under $100/month until you hit thousands of users.

**MVP Scope:**
- Solo engineer: 2-3 weeks. One week for prompt engineering and the generation pipeline. One week for frontend + auth + Stripe integration. A few days for PDF/Excel export and polish.
- Two engineers: 10-12 days comfortably.
- This is well within the 4-week red line for 1-2 engineers.

**Scaling Concerns (post-MVP):**
- LLM API rate limits are the only real bottleneck. Solved with queuing (BullMQ or similar) if you hit concurrency limits.
- No real scaling challenge until thousands of concurrent users. Serverless handles bursty traffic natively.
- Caching: if two users input similar ideas, you could cache intermediate results, but the complexity is not worth it until you have data proving duplication.

## Key Concerns

- **Financial model accuracy is the make-or-break.** If generated numbers are nonsensical, the entire product is worthless. You MUST build a deterministic financial calculation layer. Do not let the LLM do arithmetic. Extract assumptions via structured output, compute projections with real code.
- **"5 minutes" needs to be quantified honestly.** Measure actual wall-clock time for the full chain. If it creeps to 7-8 minutes under load, your marketing claim is broken. Stream partial results to the UI so the user sees progress and does not stare at a spinner.
- **Differentiation risk is high.** This is a thin wrapper around an LLM API. The technical moat is approximately zero. Anyone can replicate this in a weekend hackathon. Your moat has to be product quality -- better prompts, better templates, better financial logic, better UX. That is not a technical concern, but it matters.
- **Prompt brittleness.** LLM providers update models regularly. A prompt chain that works perfectly on GPT-4o today might produce subtly different (worse) output after a model update. You need regression testing for output quality -- save golden examples and diff against them on each model update.
- **The $29 price point is aggressive for what might feel like "just AI output."** Technically sound from a margin perspective, but if users realize they can get 80% of this by pasting a prompt into ChatGPT Plus ($20/month), your conversion will suffer. The value-add has to be the structured output, export formats, and financial modeling rigor.
- **No mention of data retention or privacy.** Startup ideas are sensitive. Users will want to know: are you sending their ideas to OpenAI? Are they stored? What is the data processing agreement? This is not technically hard to solve, but it needs to be addressed before launch.
- **Export quality matters more than generation quality.** A founder will take this PDF to investors. If it looks like it was generated by a script, credibility is gone. Invest real time in the PDF template design and Excel formatting.

## Score: 7 / 10

Technically this is almost trivially feasible -- that is both the strength and the weakness. The engineering is straightforward, the costs are low, the MVP timeline is short. I am giving it a 7 because the technical execution risk is low but the product differentiation risk is real. The hardest engineering problem here is not building it -- it is making the financial model output trustworthy enough that founders actually use it. Solve that with deterministic math on extracted assumptions, not by praying the LLM gets the numbers right. Ship the dirty version in two weeks, validate demand, then iterate on output quality. Do not over-engineer this. Boring tech, excellent prompts, bulletproof financial formulas. That is the entire technical strategy.
