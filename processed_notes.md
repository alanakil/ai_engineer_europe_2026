# AI Engineer Europe 2026 — Key Takeaways

## Meta-themes

Three ideas cut across nearly every talk:

1. **Code mode beats tool calling.** Multiple speakers (Kitze, Nuno Campos, David Soria-Parra) independently arrived at the same conclusion: replace many sequential tool calls with a code-executing REPL. Code is the only truly composable tool, and it collapses the overhead of bespoke tool APIs.

2. **Context engineering, not just context access.** Connecting an agent to many sources ≠ understanding. The real challenge is merging signals, resolving conflicts, respecting permissions, and delivering the *right* context at the *right* time. Bigger context windows are a hack, not a solution.

3. **The developer role is shifting from writing code to designing systems.** Implementation is increasingly solved. The bottleneck has moved to alignment, communication, task design, and harness engineering.

---

## The Agent Stack (what to build in 2026)

### Context Engines (Peter Werry, Unblocked)
A context engine is not naive RAG. It must:
- Merge signals from all sources (code, Jira, Slack) before the agent sees them
- Resolve conflicts via recency + authority
- Do targeted, token-optimized retrieval
- Respect data governance and permissions
- Be personalized to the user's repos, teammates, and work history

**Maturity ladder:** tab complete → agent IDE → context engineering → parallel agents → MCP + skills → harness engineering → background agents → agent teams.

### Harness Engineering (Ryan Lopopolo, OpenAI; Tejas Kumar, IBM)
A harness is everything around the model that makes it reliable: tool registry, context management, guardrails, agent loop, and verification. Changing the prompt is *not* harnessing. 2026 is the year of harnesses. The next frontier: agents that create their own dynamic harnesses on the fly.

Scarce resources to engineer around: human time, human and model attention, context window.

### Skills (Pedro Rodrigues, Supabase; David Gomes, Cursor; David Soria-Parra, Anthropic)
Skills are folders of instructions, scripts, and resources that agents discover and load dynamically.

Principles for writing good skills:
1. Describe intent, not means.
2. If it can be skipped, it will be — don't make things optional.
3. Be opinionated; encode the workflows you know work.
4. Use your existing docs.
5. Start minimal, iterate with evals.

Cursor replaced 12K LoC with a 200 LoC worktree skill. The tradeoff: less code and more flexibility, but slower and harder to navigate.

### MCP in 2026 (David Soria-Parra, Anthropic)
Two patterns to adopt now:
- **Progressive discovery:** tool search — load tools only when needed.
- **Programmatic tool calling:** write code and execute via REPL instead of one-at-a-time tool calls.

Roadmap: improved tasks and stateless transport, cross-app access, server discovery via server cards, and skills delivered over MCP.

### Enterprise Security & Gateways (Karan Sampath, Anthropic)
Don't hand-roll MCPs for every team. Establish a root of trust: security blesses one gateway platform, teams ship MCPs that focus only on business logic.

Gateway architecture: `MCP clients ↔ [Gateway ↔ MCP servers]` — handles auth, RBAC, routing, and tunneling. Key principle: **separate your agent harness from your data**.

---

## Practical Lessons

### Spreadsheet agents (Nuno Campos, Witan Labs)
Replaced 15 tools with a Node.js REPL + spreadsheet API. Benchmark went from 74% → 92%.

Takeaways that generalize:
- Many sequential tool calls = bad scripting language. Use code.
- Build verification engines, not just tools.
- Interfaces are ephemeral, engines are durable.
- Define the end state before you act.
- When something fails, check the plumbing first.

### Coding agents in practice (Matt Pollock)
- Context degrades around 100K tokens regardless of window size ("dumb zone").
- Direct agents to code *vertically* (one feature end-to-end) rather than horizontally (all layers at once) to enable feedback loops.
- LLMs will hack unit tests if given the chance — design evals accordingly.

### Properties of good agent tasks (Mario Zechner, pi)
- Scoped — the agent doesn't need a lot of context.
- Closed-loop — the agent can evaluate its own output.
- Not mission critical.
- Boring but necessary work.

### Task quality = data quality for RL (Kobie Crawford, Snorkel)
Task quality criteria: achievable, non-trivial, functionally correct, reliable environment. High-quality tasks produce cleaner failures and are learnable. Running RL on Qwen3-8B: base 15.8%, low-quality data 16.9%, high-quality data **22%**.

### Context management in long sessions (Sally-Ann Delucia, Arize)
Best approach: keep the earliest context, summarize and retrieve the middle, keep the last N turns. Offload heavy subtasks to subagents to keep the main conversation short. Eval method: load N turns, test the N+1 turn.

---

## The Bigger Picture

### The new application layer (Malte Ubl, Vercel)
- 60% of Vercel's page views are now agents. Agents are becoming the primary consumers of software.
- AI enables building all the software that was previously *nice to have but not economically viable*.
- Two futures: foundational labs win (engineers lose) vs. model commoditization (engineers win).

### Collaborative AI engineering (Maggie Appleton, GitHub Next)
Implementation is no longer the bottleneck — alignment and communication are. Coordination tooling hasn't kept up. GitHub Next is building **ACE**: a unified environment (like Slack + VSCode + GitHub) where humans and agents plan and build together in a continuous loop. Quality will be the new differentiator.

### Open source sustainability (Peter Steinberger, OpenClaw)
The volunteer model for open source maintenance is breaking under AI-accelerated contribution velocity. Problems: AI-generated security reports that look real, 12–20% of early third-party skills may be malicious, and nation-state attacks on MCP infrastructure. Working on a foundation to fund full-time maintainers.

### Personalization at scale (Shiva Verma, Spotify)
Pipeline: user activity sequences → user embeddings (transformer-based) → semantic IDs (4–6 tokens per artist) → LLM-steered recommendations. The shift from collaborative filtering to transformer-based user modeling enables LLM integration.

### What models still get wrong (Peter Gostev, Arena)
"Both bad" ratings have dropped from 25% → 9% over 3 years. Thinking/reasoning modes don't always help — sometimes no reasoning outperforms them. Model size is independent of performance on nonsensical-question benchmarks.

---

## One-liners Worth Keeping

- *"The gap is not intelligence. It's context."* — Karpathy (quoted by Peter Werry)
- *"Agents are a new kind of software."* — Malte Ubl
- *"2026 is the year of harnesses."* — Tejas Kumar
- *"2026 is all about connectivity."* — David Soria-Parra
- *"Implementation is now a solved problem. Alignment and communication are the bottleneck."* — Maggie Appleton
- *"Code is the only composable tool."* — Kitze
