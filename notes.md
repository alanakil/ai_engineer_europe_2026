# Notes

## Mergeable by default: Building the context engine to save time and tokens

By: Peter Werry, Unblocked.

"The gap is not intelligence. It's context.", Karpathy.

Problem: Access $\neq$ Understanding
Agents may connect to many things, but they also need to udnerstand relationships and why's.

Levels of AI maturity in engineering:
1. Tab complete
2. Agent IDE
3. Context engineering
4. Parallel agents
5. MCP + skills
6. Harness engineering
7. BAckground agents
8. Agent teams

1-2 -> you are the context
3-5 -> curated context
5-8 -> context engine

Myths:
- Naive RAG over my docs is a context engine.
- Just connecting naively to MCPs.
- A bigger context window will solve this.

Why you need a context engine: 
- Understands who you are and what info matters.
- Resolves conflicts between sources (code, Jira, slack).
- Respects permissions and governance.
- Delivers the right context to the right model at the right time.

Requirements to be a context engine:
- Unified system context (merge signals from all sources before delivering to agent).
- Targeted retrieval.
- Token optimization (ranked, compressed).
- Conflict resolution (recency + authority).
- Data governance (permissions + policies).
- Personalized relevance (scopred to repos, teammate, and work history).

Three hard lessons:
- Wiring in more tools didn't help the model understand the task (access vs understanding).
- Hid conflicts instead of surfacing them: when sources disagreed, they picked one truth.
- Cached answers instead of computing them.

Where to use a context engine: 
- Agent plans and code -> hydrate context before planning.
- Ticket enrichment.
- Triage ops -> routing issues, enriching tickets, validate bugs.
- Incident management.
- Customer success and sales.

How? Skills, workflows, and agents.

---

## AI coding for real engineers

By: Matt Pollock.

- Smart zone / Dumb zone. Some say we hit the dumb zone at around 40%, but he suggests about 100,000 tokens regardless of total size.
- "Ralph it" -> Let the agent improvise the plan and jump into an autonomous loop.
- Multi-phase plan: prd, plan, phase 1,...
- AFK multiphase plan.
- Clearing vs compacting?

Layers:
- Code is split in layers -> db, frontend, etc.
- LLMs like to code horizontally.
- We need to direct it to code vertically to be able to test and have feedback loops.

LLMs tend to hack unit tests.

---

## The new application layer

By: Malte Ubl, Vercel.

Two disruptions:
1. How we build with agents.
2. What agents we build.

"Agents are a new kind of software".
AI is allowing us to write all the software that is nice to hace, not just the economically viable.

He thinks SaaS companies will be fine. The cheaper the software, the more we will make and the more engineers will be needed.

Software will be used by agents.
- 60% of page views in Vercel are agents.
- Agents should run the infra.
- But we need agentic security infrastructure.

The new application layer should trhive independently of models. 

Two possible futures ahead:
1. Foundational labs win. Engineers lose.
2. Model commoditization. Engineers win.


---

## Frontier AI and the future of intelligence

By: Raia Hadsell, Google DeepMind.

Mission:
- Create the future of intelligence.
- Find root nodes.
- Partner with the world.
- Solve problems that are worth solving.

The Jennifer Aniston cell -> do they exist in AI models? Yes, through embedding layers.

Gemini embedding 2:
- Omni-modal, Gemini-derived.
- Matryoshka Representation Learning (MRL), dim up to 3,072.
- Text, visual, audio, layout (PDF), video.

GraphCast (2024): Solving global weather with AI
- Graphical Neural Network.
- Predicts weather up to 15 days in the future.

GenCast (2024)
- Probabilistic model. 
- Higher accuracy and efficiency. 
- Outperformed other methods on 97% of evals.

Functional Generative Network (2025): End to end trained on cyclones.

Genie 2: Large-scale foundation world model, 3D env, but very slow.

Veo family: state of the art video generation.

---

## Harness engineering: How to build software when humans steer and agents execute

By: Ryan Lopopolo, OpenAI.

The way we build software has changed. We are shifting towards systems thinking/design.

1. Models are good enough.
2. Code is free.
3. Your role is to unblock your team.

Scarce resources:
- Human time.
- Human and model attention.
- Model context window.

---

## OpenClaw update

By: Peter Steinberger, OpenAI/OpenClaw

The Maintainer Problem: How can we maintain projects at the speed of AI?

Security DDoS: OpenClaw had 1,000+ security advisories. Mostly: remote code execution, approval bypass, etc.

Nation states target lobsters:
- GhostClaw (North Korea).
- Axios attack

How did they survive the 1,142 advisories? They got help from several companies.

"Agent of Chaos" paper is a critique to OpenClaw, however he claims that they ignored the OpenClaw security recommendations.

"Honest assessment" of OpenClaw: 
- Unsolved LLM risk (lethal trifecta).
- Real implementation bugs.

Pain of maintaining infra:
- Volunteer model is breaking.
- AI-generated reports look real.
- 12-20% of early third-party skills can be malicious.
- Open source governance.

He is now working on building "the foundation" which aimes to get tax deductions to hire full-time maintainers.

Shipping now:
- Dreaming: REM backfill + UI for agent memory.
- Local model benchmarks with Prime Intellect + Tencent.
- vLLM partnership.
- GitHub secure open source fund.

---

## One dev, two dozen agents and zero alignment: Why we need collaborative AI engineering

By: Maggie Appleton, Github Next.

Implementation is now a sovled problem. Alignment and communication are now the bottleneck. However, all fo our coordination tools are from the previous era.

Chats -> docs -> issues -> build -> PR

Build has shrunk a lot. 

Problem: This disruption leads to wasted work and coordination debt.

Solution: Bring collaboration and alignment to the flow. plan -> build -> plan -> build ->...

Human context is not in the codebase:
- Business context.
- Political dynamics. 
- Product views.

They introduced a new product called "ACE" (coming soon in a few months).
- It's like Slack, VSCode, and GitHub - all in one.
- Session: prompt agents, multiplayer, agent spins off in a microVM cloud, others can spin up the exact same environment, can see diffs, and preview UIs.

Goal: Reclaim time for better design, product thinking, and high quality engineering.

Quality will be the new differentiator.

---

## Teaching coding agents to master spreadsheets

By: Nuno Campos, Witan Labs.

Problem: The LLM sees formulas and metadata, we see the rendered data. How can we make spreadsheet handling better?

Dead ends:
- TSV views: loses formatting.
- SQL views: flat tables.
- HTML views: too verbose.
- DOT graphs: useful for analysis, not interaction.
- XML/XLST: LLM struggled with syntax.

They replaced 15 tools with a Node.js REPL and a spreadsheet API. This worked best.
They used coder mode: instead of tool calls, the model would write and execute code.

REPL => Code mode + Persistent state

Agent then writes short scripts, reasons between them, building understanding incrementally.
Agent could now course-correct mid-exploration.

Results: 74% -> 92% on an internal benchmark.

Takeaways:
1. Many sequential tool calls = bad scripting language. Use code instead.
2. Build verification engines.
3. Interfaces are ephemeral, engines are durable.
4. Structured reasoning > better tools. "Define the end state before you act."
5. Domain knowledge outlasts tools.
6. Match eval to output type.
7. When something fails, check plumbing first.

---

## Hierarchical memory: Context management in agents

By: Sally-Ann Delucia, Arize.

She shared lessons learned from building their agent Alyx, which is a harness to help build your AI apps.

Context engineering = choosing what the model sees. Not just a engineering problem, but alos a Product and UX problem.

How did they control context?
1. Naive truncation: early turns. Did not work well, as too much information was lost. 
2. LLM summarization: inconsistent, unreliable, and hard to control what was important.
3. Best one: truncation + summarization. They would keep the earliest part of the context, store and retrieve the middle, and keep the last part.

This is not perfect, it still fails for really really long sessions. 

Eval: Load N turns, test the N+1 turn.

Keep in mind that not all context belongs to the same agent. They had success offloading heavy tasks to subagents, keeping the main conversation short. 

---

## Personalization in the era of LLMs

By: Shiva Verma, Spotify. 

1. Foundational user modeling: seq -> vec
    - Represent user taste and are foundational for several features.
2. Catalog grounding: vec -> tokens
3. Steerable and personalized recommendations: tokens + vec -> recs via LLMs

User modeling:
- Previous modeling: Audio feature embed + collaborative filtering + demographics + context + new user onboarding signal -> embedding using AutoEncoder.
- Now: User activities + request context + query/prompt + item -> embedding via a transformer.

Catalog grounding:
- Content vector + user vector -> fine-tuned LLM -> sequenced recs + rec explanations

Semantic IDs: vectors -> tokens. Represent artists with 4-6 tokens.

Steerable and personalized recommendations:
- Prompt + user vector (projected) -> LLM -> recs.

---

## AI harnesses

By: Tejas Kumar, IBM.

Why harnesses? They give reliability irrespective of the model.

What harness? Eval (ML) or agent (AI).

Focus now is on agent harnesses -> everything around the model to make it reliable.

It has:
- Tool registry.
- Model.
- Context management.
- Guardrails (e.g., max_stops).
- Agent loop.
- Verify.

NOTE: Changing the prompt is not harnessing!

IBM open source project: OpenRAG

"2026 is the year of harnesses".

What if agents create their own dynamic on-the-fly harness?

---

## What we learned from writing the supabase skill

By: Pedro Rodrigues, Supabase.

Agents are now smart enough, but they need the right guidance.
- Security pitfalls
- Stale data
- Missing workflows

Skills: Folder containing instructions, scripts, and resources that agents discover and load dynamically.

Principles:
1. Describe intent, not means.
2. If it can be skipped, it will be. Optional files are rarely loaded.
3. Be opinionated, state workflows that you know work best.
4. Use your docs.
5. Start minimal, iterate with evals.

---

## From writing code to designing systems: How the developer role has changed

By: Chris Noring, GitHub.

Old world: 100% hands on keyboard.

What happened? The center of gravity moved. We are stuck with an AI tool that we try to make the most of.

Problem: When to use what?

Solution: 
1. Start -> CLI. Create a first draft, set up guardrails. Manage repo tasks including issues, PR, status checks. Prompts are inputs.
2. Continue -> Editor. Set up guardrails (agents.md; skills; custom agent). Fine grained interaction. Use when you want more control.
3. Scale/delegate -> CLI / GitHub UI. 

The speaker argued that we will move further away from the editor as time goes by.

---

## Kitze keynote

By: Kitze, Sizzy.co

Code mode > tool calling.

Code is the only composable tool.

They went from 2,594 endpoints to two tools: search and execute. Let the code do the talking. Building an MCP is not feasible when you have so many tools.


---

## Gemma 4

By: Omar Sanseviero, Google DeepMind.

They released: 
E2B -> 4.6 GB
E4B -> 7.5 GB
26A4B -> 26 GB
31B -> 31 GB

- Suitable for phones and consumer computers.
- Switched to Apache 2.0 licence.
- New component: per-layer embedding. E2B is actually 4B params, but this makes it effectviely 2B.
- They implemented a new multilingual-friendly tokenizer which allows for training on new languages without affecting current capabilities.

---

## The future of MCP

By: David Soria-Parra (creator of MCP), Anthropic. 

MCP apps: it allows rendering stuff in chat.

Skills over MCP coming soon. 

"2026 is the year of taking agents to production."

Coding agents have been very successful, but no other types of agents will emerge.

2026 agents use all of these:
- Skills
- MCP
- CLI / Computer use

We need a few things though, harness work: 
- Progressive discovery pattern: tool search. Load tools when needed.
- Programmatic tool calling: do not call one tool at a time, write code instead and execute via REPL.

Build for agents:
1. Design for the agent (or for a human)
2. Reach for code mode
3. Ship an MCP app

MCP on 2026:
- Improve the core: improved tasks, stateless transport.
- Integrate everywhere. Cross-app access, server discovery via server-cards.
- Pushing the boundary: skills over MCP

"2026 is all about connectivity".

---

## Agent orchestration

By: Ido Solomon, AgentCraft / MCP UI.

Why can't we scale up agents? B/c we are the bottleneck. We need human skills to tackle this.

AgentCraft: It's like a game but characters are agents like Copilot/ClaudeCode/etc. and you can talk to them and send them to work.

---

## Building pi in a world of slop

By: Mario Zechner, pi.

"We are in a fuck around and find out era of coding agents."

He built pi which adapts to workflows. Tools: read, write, edit, bash.

10x token reduction compared to Claude Code. 

Pi extensions like /btw. It can write them for you.

Most of the code in the internet is garbage and that's what the LLM has learned.

Large context windows are a hack.

Properties of good agent tasks:
- Scoped so the agent does not need a lot of context. 
- Closed slop: agent can evaluate its own work.
- Not mission critical.
- Boring stuff we don't have time for.
- Reproduction cases from user issues.

---

## Replacing 12K LoC with a 200 LoC skill

By: David Gomes, Cursor.

Cursor worktrees: Agents can work in parallel in different branches.

They removed 15K LoC and replaced with 2K in the worktree feature.

They realized they could leverage skills for the feature itself to explain to the model how to create worktrees.
Same for the "best-of-n" feature: allows for different models to work on the same thing in different worktrees.

Pros of refactor:
- Less code
- Can switch into a worktree halfway through
- Work with multiple repos OOB
- Judging experience for best-of-n is far superior
- User can ask the agent to stitch together pieces from different worktrees.

Cons of refactor:
- Hard for the agent to stay in the right worktree for a long time. This used to be hard coded, now they just tell the LLM
- Slower b/c agent creates each worktree
- Harder to find and navigate around

How could this skill be improved? Evals and RL training.

How do they eval? They start a new agent in a worktree. Two scorers: check if files were modified in this branch & check if files were modified in primary checkout.

Next:
- Native worktrees implemnetation in new Agent
- Improve skills
- Other parallelization not using git


---

## Task fidelity scaling laws

By: Kobie Crawford, Snorkel.

Snorkel is an AI data company that sells data to train LLMs.

They wanted to measure the impact of task quality on performance.

For agents: task quality = data quality!

Task quality (all must be true for a task to be accepted): 
- Achievable
- Non-trivial
- Functionally correct
- Reliable (env)

Accepted tasks are harder and more complex:
- Require 2x tool calls
- More output tokens
- Pass rate decreases
- Produce cleaner, harder failures

Accepted tasks = high quality tasks

From failures, they derived failure modes.

Rejected tasks produce noisy, unlearnable failures.

They ran RL on Qwen3-8B on accepted and rejected tasks.
- Base: 15.8%
- Low quality: 16.9%
- High quality: 22%

---

## Your coding agent should do AI systems engineering

By: Ben Burtenshaw, Hugging Face.

Reviewed:
- Write custom kernels using an agent
- Yolo an agent to finetune an LLM
- Autolab multi agent research

Kernels: Functions compiled to run on a GPU typicall executed in Python. They are specific to hardware.

Efficiency: Compute (flops) | Memory (time spent on comm; bottleneck) | Overhead

Multiagent approach (like Karpathy's auto lab):
- Researcher: literature scout
- Planner: Owns experimental queue
- Worker: Does work in one worktree
- Reporter: Monitors

Takeaways:
1. Agents work best with primitives. Do not abstract. Expose, well.
2. HF hub is ready for these kind of experiments.


---

## Gateways are all you need

By: Karan Sampath, Anthropic.

Enterprise state of play:
- Observability
- Access control
- Security

The official MCP registry is useful, but not enough for enterprises.

Bottleneck is security review.

Fix: Don't hand roll MCPs. Establish a root of trust.

Security blesses one platform -> teams ship MCPs that focus on business logic

We need a gateway:

MCP clients <-> [Gateway <-> MCP servers] (your network)

Gateway is composed of:
- Auth handler
- RBAC
- Proxy router
- Tunnel handler
- ...
- ...

It enables:
- Any surface
- Secured connections
- Faster iteration
- Standard primitives
- Pluggable connections
- Scoped and scalable

Big picture: Separate agent harness from your data.

---

## Agents need more than chat

By: Jacob Lauritzen, Legora

Goal of vertical AI: Have the AI complete end to end work.

Solvable tasks will be solved by AI because of RL.
- Easily verifiable: math, code.
- Hard to verify: legal.

Verticals have tasks across the spectrum. E.g., checking definitions vs. litigation strategies.

We have two zones:
- Trust (the AI can do very well)
- Control (we need to control it more to ensure good results)

We need to increase the zone of trust.

How do we increase control?
- Planning to steer in the right direction.
- Skills: encode humna judgement.
- Elicitation / decision log: ask the user.

Chat is 1-dimensional, low bandwidth.

Human and agents need to collaborate on high-bandwidth environments, which should depend on the specific vertical.

---

## What do models still suck at?

By: Peter Gostev, Arena

He created the bullshit benchmark: how do models respond to nonsensical questions? 

Some results:
- Thinking does not help; sometimes no reasoning performs better.
- Size is independent of performance in this benchmark.

Arena has model A, model B, or "both bad".

"both bad" rate has steadily decreased from 25% to 9% over 3 years. Also consider that prompting has changed a lot too.

He broke down results by discipline and domain. E.g., software: gaming, model serving, gpu compute, systems, etc.

---

