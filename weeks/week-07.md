# Week 7: Multi-agent systems and memory

**Month 2: Agentic systems, frameworks, tools, evaluation** · Know when it earns its complexity · 4 lessons · about 12 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 6](week-06.md) · [Week 8 →](week-08.md)

## What you will be able to do

- Supervisor pattern, peer-to-peer handoff, and hierarchical delegation between agents
- Short-term versus episodic versus long-term memory, and what should never be stored at all
- Write down three real cases where multi-agent is overkill for what a single agent could do
- Design the failure path: what happens when one agent in the chain returns garbage

## You ship this week

> A two-to-three-agent system with a supervisor routing to specialists. For example a researcher, a writer, and a critic that reviews the writer’s output before it ships.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. Supervisor, handoff, hierarchy: how agents actually work together

*About 3 hours*

By now you can build one agent loop by hand (Week 4) and as a graph (Week 5). Sooner or later a client asks for "a team of agents": a researcher, a writer, a reviewer, a manager agent on top. Some of those systems are the right design and many are not. You cannot tell which until you can see what a multi-agent system really is underneath: several ordinary agent loops, a rule for who acts next, and messages passed between them. This lesson takes the three patterns you will meet everywhere (supervisor, peer-to-peer handoff, hierarchical delegation) down to that level: who holds control, what each agent can see, what a handoff costs in tokens and latency, and how errors compound along the chain. You will build a working supervisor with two workers on a fake model, so every claim is something you can print and check.

Covers: The mental model: an agent is a context window with a job; Pattern 1: the supervisor; A supervisor and two workers, running on a fake model.

### 2. Short-term, episodic and long-term memory, and what never to store

*About 3 hours*

In Week 4 you built three mechanisms: a buffer, a rolling summary and a retrieval lookup. Mechanisms are not a memory design. A client asking for "an assistant that remembers our customers" is really asking four questions: what is remembered, for how long, who can see and change it, and what happens when a customer asks you to forget. Multi-agent systems sharpen every one of them, because several agents now read and write the same store. Get the categories wrong and you get an agent that recalls last year's complaint in every reply, or forgets a refund promised yesterday. Get the privacy wrong and you have built a long-lived copy of OTPs, health details and bank numbers that sits outside every control the client's compliance team thought they had. This lesson gives you precise definitions, storage and retrieval choices for each kind, and the rules for what never gets stored.

Covers: The mental model: classify memory by lifetime and by shape; Short-term; Episodic; Semantic; Storage choices for each kind; Retrieval: relevance, recency and importance.

### 3. When multi-agent is overkill: arguing it with a cost model

*About 2.5 hours*

Clients arrive with architecture already decided: "we want a team of agents", drawn as five boxes with job titles. Sometimes that is right. More often one well-built agent, or a plain workflow with a single model call, would be cheaper, faster, more reliable and far easier to debug. Saying so is part of the job, but "I think it's overkill" loses to a confident slide. What wins is an argument with numbers: how many model calls, how many tokens, how long the user waits, how likely the whole chain is to succeed, and which specific benefit the split would buy. This lesson gives you a small cost model you can run and adapt, three worked cases where multi-agent is overkill, and the few signals that genuinely justify the extra agents. The task is to write down three such cases of your own; by the end you will know how to write each one so a sceptical architect accepts it.

Covers: The mental model: the burden of proof is on the split; What each agent costs; What can justify it; Where the costs come from, precisely; A cost model you can run.

### 4. Designing the failure path: when one agent in the chain returns garbage

*About 3 hours*

In a single agent, a bad model output usually shows up as a bad answer you can see. In a multi-agent chain it shows up three steps later, polished by a writer agent, approved by a critic agent that checked the prose rather than the facts, and delivered to the client with a confident tone and a citation to a source that does not exist. Every agent in the chain makes garbage look more legitimate. The researchers behind the MAST taxonomy (Cemri and others, 2025), who annotated failures in seven popular multi-agent frameworks, grouped them into system design issues, inter-agent misalignment and task verification. The last two are exactly what this lesson is about: what one agent hands another, and who checks it. You will design the failure path before the happy path: contracts at each handoff, layered validation, a policy for retrying versus escalating, honest partial results, and the traces that let you say which agent was wrong.

Covers: The mental model: every handoff is an untrusted API boundary; Four kinds of garbage; Contracts: what a worker promises; Validation in layers, cheapest first; Retry, escalate or fall back; Partial results, said out loud; Observability for blame; A supervisor that catches a bad worker.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [Anthropic Engineering: How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system)
- [LangChain docs: Multi-agent (subagents, handoffs, skills, router, custom workflow)](https://docs.langchain.com/oss/python/langchain/multi-agent)
- [LangChain docs: Subagents (wrapping an agent as a tool, context isolation)](https://docs.langchain.com/oss/python/langchain/multi-agent/subagents)
- [LangGraph docs: Multi-agent systems (network, supervisor, hierarchical, Command handoffs)](https://docs.langchain.com/oss/python/multi-agent)
- [Anthropic Engineering: Effective context engineering for AI agents (sub-agent architectures)](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [LangChain docs: Memory overview (short-term, long-term, semantic, episodic, procedural)](https://docs.langchain.com/oss/python/concepts/memory)
- [Sumers et al., Cognitive Architectures for Language Agents (CoALA), arXiv 2309.02427](https://arxiv.org/abs/2309.02427)
- [Park et al., Generative Agents: Interactive Simulacra of Human Behavior, arXiv 2304.03442](https://arxiv.org/abs/2304.03442)
- [Claude docs: Memory tool (client-side memory, security considerations)](https://platform.claude.com/en/docs/agents-and-tools/tool-use/memory-tool)
- [PIB explainer: DPDP Rules, 2025 notified (November 2025)](https://static.pib.gov.in/WriteReadData/specificdocs/documents/2025/nov/doc20251117695301.pdf)
- [Claude blog: Building multi-agent systems, when and how to use them (January 2026)](https://www.claude.com/blog/building-multi-agent-systems-when-and-how-to-use-them)
- [Anthropic Engineering: Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)
- [LangChain blog: How and when to build multi-agent systems (Harrison Chase)](https://www.langchain.com/blog/how-and-when-to-build-multi-agent-systems)
- [Cemri et al., Why Do Multi-Agent LLM Systems Fail? (MAST taxonomy), arXiv 2503.13657](https://arxiv.org/abs/2503.13657)
- [Claude docs: Structured outputs (guarantees and their exceptions)](https://platform.claude.com/docs/en/build-with-claude/structured-outputs)
- [Pydantic docs: Validators (field validators, ValidationInfo, validation context)](https://pydantic.dev/docs/validation/latest/concepts/validators/)

## Further reading

- [Why Multi-Agent?](https://aiengineeringfromscratch.com/lesson?path=phases%2F16-multi-agent-and-swarms%2F01-why-multi-agent)
- [Supervisor / Orchestrator-Worker Pattern](https://aiengineeringfromscratch.com/lesson?path=phases%2F16-multi-agent-and-swarms%2F05-supervisor-orchestrator-pattern)
- [Role Specialization: Planner, Critic, Executor, Verifier](https://aiengineeringfromscratch.com/lesson?path=phases%2F16-multi-agent-and-swarms%2F08-role-specialization)
- [Agent Framework Tradeoffs](https://aiengineeringfromscratch.com/lesson?path=phases%2F11-llm-engineering%2F17-agent-framework-tradeoffs)

## Check yourself

Answer out loud before opening each answer.

<details><summary>In a tool-calling supervisor, what does a worker agent see, and what does the supervisor see of the worker's work?</summary>

The worker sees its own system prompt, its tools and the brief passed as its first user message. The supervisor sees only what the wrapper returns, typically the worker's final message, not its tool calls or intermediate results.

</details>

<details><summary>Why are handoffs cheaper than a supervisor for follow-up questions, and what do you lose?</summary>

The active agent stays active, so a follow-up goes straight to it with no routing or delegation call. You lose a central place that sees the whole task, so loops, budgets and quality checks must be enforced in code outside the agents.

</details>

<details><summary>What distinguishes an episodic memory from a semantic one, in one test?</summary>

Remove the date and outcome. If it stops making sense, it is an episode of something that happened; if it is still true and useful, it is a semantic fact, often derived from several episodes.

</details>

<details><summary>Why does the episodic store measure recency from `last_used` rather than from when the episode happened?</summary>

So that memories that keep proving relevant decay more slowly, which is the reinforcement idea in the Generative Agents design. Recency from creation alone would bury a useful old memory regardless of how often it helps.

</details>

<details><summary>Name the benefits that can justify splitting one agent into several, and the test for each.</summary>

Parallel breadth (subtasks independent of each other), context isolation (a subtask generating lots of material the main task does not need), a permission or trust boundary (untrusted input or secrets that must be confined), and conflicting specialisation (one agent degrading as tools or instructions are added).

</details>

<details><summary>Why can a supervisor design use fewer tokens than a single agent and still be the wrong choice?</summary>

Workers start with fresh contexts, so a naive single agent that keeps every tool result can cost more tokens. But the supervisor adds calls, latency for writing briefs and handoffs that lose information, and a single agent with context clearing usually removes the token advantage anyway.

</details>

<details><summary>Why is a schema-valid worker output still untrusted?</summary>

A schema guarantees shape (valid JSON, required fields, types), not meaning. The content can still cite sources the worker never saw, misquote them or answer a different question, so you need checks against the worker's inputs.

</details>

<details><summary>When should the supervisor not retry a failing worker?</summary>

When the output contains instruction-like or hostile content (retrying re-exposes the worker), and when the failure is deterministic given the input, such as a fact that is not in the sources. Then salvage, fall back or escalate.

</details>

---

**Learn Week 7 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week07). Week 1 is free.
