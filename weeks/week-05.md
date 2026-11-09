# Week 5: LangGraph, properly

**Month 2: Agentic systems, frameworks, tools, evaluation** · The current production standard for stateful agents · 4 lessons · about 12 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 4](week-04.md) · [Week 6 →](week-06.md)

## What you will be able to do

- Nodes, edges, and state graphs, conditional routing between nodes
- Checkpointing and persistence across sessions, streaming partial output
- Human-in-the-loop interrupts: a graph that pauses and waits for a person before continuing
- Rebuild Week 4’s hand-written agent in LangGraph and compare the two implementations line by line

## You ship this week

> A LangGraph agent with at least one conditional branch and one human-approval checkpoint gating a risky action, like sending an email or making a purchase.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. State graphs: nodes, edges, reducers and conditional routing

*About 3 hours*

Last week you wrote an agent as a `for` loop with `if` statements inside it, and you drew it as a state machine before you coded it. LangGraph asks you to hand over the drawing instead of the loop: you declare the states, the transitions and the data that flows between them, and a runtime walks the graph for you. That trade buys you things a plain loop does not have for free, such as saving progress after every step, pausing for a human, streaming each step and a diagram of the logic that a client can read. It also adds a layer that hides control flow if you do not understand it. Most LangGraph bugs that reach production are not exotic: a list that is overwritten instead of appended, a router that returns a label nobody mapped, a node that edits state in place and loses the edit. This lesson teaches the model underneath so those bugs are obvious to you.

Covers: The mental model: you declare the state machine, a runtime walks it; State: a schema with a merge rule per key; Nodes: functions that return what changed; Edges: fixed, conditional, START and END; Under the hood: super-steps; A state-graph engine in 50 lines.

### 2. Checkpoints, threads and streaming: agents that survive restarts and show their work

*About 3 hours*

Real conversations with a client's agent do not fit in one function call. A customer messages on WhatsApp at 9 p.m., replies the next morning, and expects the bot to remember the order they were talking about. Meanwhile the client deploys twice a day, and every deploy restarts the process that held the conversation in memory. Long runs fail halfway: a payment gateway times out at step 7 of 9, and you do not want steps 1 to 6, each with a paid model call, to run again. And a user who sees nothing for 20 seconds assumes the system is broken. Checkpointing solves the first three problems by saving the graph's state after every step; streaming solves the last by showing progress while the run happens. Both are the reason many teams adopt LangGraph at all, so you need to know exactly what they save, when, and where.

Covers: The mental model: a save file after every step, one slot per conversation; What a checkpoint holds; A checkpointer by hand.

### 3. Human-in-the-loop with interrupt(): pausing a graph until a person decides

*About 3 hours*

The first question a client's risk team asks about an agent is "what can it do without asking anyone?" For anything that moves money, writes to a system of record, or speaks to a customer in the company's name, the honest answer must be "nothing, until a named person approves". That approval might come in four seconds or four hours, from a different device, after your server has restarted twice. A `while` loop waiting on `input()` cannot do that. LangGraph's `interrupt()` can: it saves the run to the checkpointer, hands a question to your application, and lets any later process continue the run with the person's answer. It is also easy to get subtly wrong, because the node that paused runs again from its first line when it resumes. This lesson shows the mechanism, the patterns (approve, edit, reject) and the traps that cause double refunds.

Covers: The mental model: pause means "save and return", resume means "run the node again with the answer"; The mechanism, by hand.

### 4. Week 4's agent, rebuilt in LangGraph: a line-by-line comparison

*About 3.5 hours*

Clients will ask you, often in the first meeting, "should we use LangGraph or just write it ourselves?" An answer based on taste is useless to them. An answer based on having built the same agent both ways, and knowing exactly which line of one became which line of the other, is what makes you credible. This lesson ports the Week 4 order agent to LangGraph, proves the two behave identically on the same scripted model, and then lists precisely what the framework adds (checkpoints, streaming, interrupts, tracing), what it hides (defaults you did not choose, message translation, deep stack traces) and what it costs you over time (version churn). It ends with a plan for this week's deliverable, which is the first agent you build where the framework clearly earns its place.

Covers: The mental model: the loop did not disappear, it moved; Week 4: your loop; LangGraph: the runtime; Step 1: rewrite the loop as a graph, without the library.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [LangGraph docs: Graph API overview (state, reducers, nodes, edges, Command)](https://docs.langchain.com/oss/python/langgraph/graph-api)
- [LangGraph docs: Use the Graph API (how-to examples)](https://docs.langchain.com/oss/python/langgraph/use-graph-api)
- [LangGraph docs: The Pregel runtime and super-steps](https://docs.langchain.com/oss/python/langgraph/pregel)
- [LangGraph docs: Quickstart](https://docs.langchain.com/oss/python/langgraph/quickstart)
- [LangGraph docs: Persistence](https://docs.langchain.com/oss/python/langgraph/persistence)
- [LangGraph docs: Checkpointers (StateSnapshot, history, serialization, encryption)](https://docs.langchain.com/oss/python/langgraph/checkpointers)
- [LangGraph docs: Time travel (replay and fork)](https://docs.langchain.com/oss/python/langgraph/use-time-travel)
- [LangGraph docs: Streaming](https://docs.langchain.com/oss/python/langgraph/streaming)
- [LangChain docs: Changelog (stream version v2 in 1.1, stream_events v3 in 1.2)](https://docs.langchain.com/oss/python/releases/changelog)
- [LangGraph docs: Interrupts (interrupt, Command(resume), rules, patterns)](https://docs.langchain.com/oss/python/langgraph/interrupts)
- [LangChain docs: Human-in-the-loop middleware (HumanInTheLoopMiddleware, interrupt_on)](https://docs.langchain.com/oss/python/langchain/human-in-the-loop)
- [LangChain reference: ToolNode (handle_tool_errors)](https://reference.langchain.com/python/langgraph.prebuilt/tool_node/ToolNode)
- [LangGraph docs: v1 migration guide (deprecations)](https://docs.langchain.com/oss/python/migrate/langgraph-v1)
- [LangSmith docs: Trace with LangGraph](https://docs.langchain.com/langsmith/trace-with-langgraph)

## Further reading

- [Agent State Machines: Graphs, Nodes, Checkpoints](https://aiengineeringfromscratch.com/lesson?path=phases%2F11-llm-engineering%2F16-langgraph-state-machines)
- [Stateful Graph Orchestration](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F13-langgraph-stateful-graphs)
- [Anthropic’s Workflow Patterns: Simple Over Complex](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F12-anthropic-workflow-patterns)

## Check yourself

Answer out loud before opening each answer.

<details><summary>A node returns `{"messages": [new_message]}`. What decides whether the history grows by one or is replaced by one message?</summary>

The reducer on the `messages` key in the state schema. With `add_messages` or `operator.add` the update is merged into the existing list; without a reducer, the default rule overwrites the key.

</details>

<details><summary>Two nodes run in the same super-step and both write to `status`, which has no reducer. What happens and why?</summary>

LangGraph raises `InvalidUpdateError`, because without a reducer it has no rule for combining two values written in the same step. Add a reducer or make only one branch own that key.

</details>

<details><summary>You compile with a checkpointer and invoke twice with the same `thread_id`. Why does the second call see the first call's messages?</summary>

Before running, LangGraph loads the latest checkpoint for that thread and merges the new input into it through the reducers, so `add_messages` appends the new message to the stored history.

</details>

<details><summary>A node fails at step 5 of a run. What does `invoke(None, config)` do, and which nodes run again?</summary>

It continues the thread from its latest checkpoint, so the failed node runs again and the run carries on from there. Nodes that completed in earlier super-steps are not re-run, and successful writes from the failed step are kept as pending writes.

</details>

<details><summary>Why does `interrupt()` need a checkpointer when the reviewer answers within a second?</summary>

The pause is implemented by saving the thread and returning; resuming loads that saved state and re-runs the node. Without a checkpointer there is nothing to load, so `Command(resume=...)` fails, regardless of how fast the person is.

</details>

<details><summary>A node sends a Slack message, then calls `interrupt()` for approval. The reviewer approves. How many Slack messages were sent, and how do you fix it?</summary>

Two, because the node re-runs from its first line on resume. Move the Slack call into a separate node before the approval node, or after the decision, and make it idempotent.

</details>

<details><summary>Your Week 4 loop had `max_steps=6`. What `recursion_limit` gives the same number of model calls in a model-plus-tools graph, and what is different when it is hit?</summary>

12, because each turn is two super-steps. When it is hit, LangGraph raises `GraphRecursionError` rather than returning a status, so the caller must catch it (or the graph must check `RemainingSteps` and stop gracefully).

</details>

<details><summary>You port an agent with `ToolNode(tools)` and the prebuilt `tools_condition`. Name two behaviours that differ from the Week 4 loop.</summary>

A tool that raises an ordinary exception crashes the run instead of being reported to the model, because the default handler only converts argument-validation errors. And a `max_tokens` truncation routes to `END` like a finished answer, because `tools_condition` only checks for tool calls.

</details>

---

**Learn Week 5 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week05). Week 1 is free.
