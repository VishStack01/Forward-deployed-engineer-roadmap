# Week 6: MCP and the tool ecosystem

**Month 2: Agentic systems, frameworks, tools, evaluation** · Now assumed, not optional · 4 lessons · about 14 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 5](week-05.md) · [Week 7 →](week-07.md)

## What you will be able to do

- Read the Model Context Protocol spec and build one MCP server exposing two or three real tools
- Connect your MCP server to an actual MCP client and confirm it works end to end
- Skim CrewAI’s role-based multi-agent pattern and compare its mental model to LangGraph’s graph model
- Write down, in your own words, when you would reach for LangGraph versus CrewAI versus a plain loop

## You ship this week

> Your own MCP server, wrapping a public API you actually like (GitHub issues or a CSV file works fine), that any MCP-compatible client can plug into.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. The Model Context Protocol from the spec up, and a real MCP server

*About 4 hours*

In Week 2 you described tools to a model as JSON Schema inside your own program, and in Weeks 4 and 5 you wired those tools into loops and graphs. Every one of those tools was trapped in the codebase that defined it. The Model Context Protocol (MCP) takes the same idea, a named function with a schema that a model can ask to call, and moves it into a separate program that any compatible application can launch or connect to: Claude Desktop, Claude Code, an IDE, a LangGraph agent, a CrewAI crew. Clients now ask for "an MCP server for our ERP" the way they once asked for a REST API. To answer well you need to know what the protocol actually guarantees, which version you are speaking (the spec changed shape in July 2026), and how to build a server whose tools a model can use safely.

Covers: The mental model: tool calling, moved across a process boundary; Reading the spec without drowning; JSON-RPC 2.0, the envelope; Two eras: the handshake, and the stateless protocol; The three server primitives; Tools in detail; Transports; The wire format, by hand.

### 2. Connecting an MCP server to real clients: Inspector, Claude, your own host, and what can go wrong

*About 3.5 hours*

A server that only works in your own test script is not a deliverable. The client's team will plug it into Claude Desktop, Claude Code, an IDE, or the agent service you built for them, and each of those launches it differently, with a different working directory, a near-empty environment and its own logs. Most "the MCP server doesn't work" reports are not protocol bugs: they are a relative path, a missing environment variable, a stray `print()` on stdout, or a host still running last week's config. And once it does connect, you have given a model the ability to act on a real system, so the security questions (who approves a write, what happens when a tool result contains instructions) stop being theoretical. This lesson takes last lesson's `inventory_server.py` through four real clients and through the failures you will actually meet.

Covers: The mental model: connecting means handing over a launch command.

### 3. CrewAI's crews and LangGraph's graphs: two mental models for multi-step agents

*About 2.5 hours*

Sooner or later a client's team will say "we prototyped this in CrewAI" or "our platform team standardised on LangGraph", and you will need to read their code, extend it, or argue for changing it. The two frameworks describe the same underlying thing, a series of model calls with tools and shared data, in very different words. CrewAI asks you to describe a team: who is on it, what each person is responsible for, and how work is handed out. LangGraph, which you used all of Week 5, asks you to describe a state machine: what data exists, which step runs next, and why. Each makes some things easy to say and others hard to see. If you understand both, down to the prompts and model calls they produce, you can judge a design on its merits rather than on habit.

Covers: The mental model: an org chart versus a flowchart; CrewAI; LangGraph; CrewAI's building blocks, per the current docs; A small crew, run for real.

### 4. LangGraph, CrewAI or a plain loop: choosing, writing the decision down, and planning your MCP server

*About 4 hours*

On a client engagement, the framework question arrives in the first week, often as a statement rather than a question: "we'll use CrewAI, our intern liked it" or "the architecture board mandates LangGraph". The choice decides how much of the system you control, how you debug it at 2 a.m., what the client's own engineers can maintain after you leave, and how hard it is to change course. A wrong choice is rarely fatal, but it is expensive: weeks spent fighting a framework's defaults, or rebuilding half a framework by hand inside a "simple" loop. An FDE is expected to make this call with reasons, write it down so the client can challenge it, and revisit it when facts change. This lesson gives you a framework for the decision, three worked client scenarios, the format for recording it, and then helps you plan this week's deliverable.

Covers: The mental model: a framework is a bundle of defaults you are buying; Plain loop; LangGraph; CrewAI; The five questions; A decision you can show your working for.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [Model Context Protocol specification (latest revision)](https://modelcontextprotocol.io/specification/latest)
- [MCP spec 2026-07-28: Key changes since 2025-11-25](https://modelcontextprotocol.io/specification/2026-07-28/changelog)
- [MCP spec 2026-07-28: Versioning and compatibility](https://modelcontextprotocol.io/specification/2026-07-28/basic/versioning)
- [MCP spec 2026-07-28: Tools](https://modelcontextprotocol.io/specification/2026-07-28/server/tools)
- [MCP Python SDK repository (README links the v2 docs and migration guide)](https://github.com/modelcontextprotocol/python-sdk)
- [MCP docs: Connect to local MCP servers (Claude Desktop config and logs)](https://modelcontextprotocol.io/docs/2026-07-28/develop/connect-local-servers.md)
- [MCP docs: MCP Inspector](https://modelcontextprotocol.io/docs/2026-07-28/tools/inspector.md)
- [Claude Code docs: Connect Claude Code to tools via MCP](https://code.claude.com/docs/en/mcp)
- [MCP spec 2026-07-28: stdio transport](https://modelcontextprotocol.io/specification/2026-07-28/basic/transports/stdio)
- [MCP docs: Security best practices](https://modelcontextprotocol.io/docs/2026-07-28/tutorials/security/security_best_practices.md)
- [CrewAI docs: Crews (attributes, kickoff, CrewOutput)](https://docs.crewai.com/en/concepts/crews)
- [CrewAI docs: Processes (sequential and hierarchical)](https://docs.crewai.com/en/concepts/processes)
- [CrewAI docs: Flows (start, listen, router, state, persist)](https://docs.crewai.com/en/concepts/flows)
- [CrewAI docs: MCP servers as tools](https://docs.crewai.com/en/mcp/overview)
- [LangGraph docs: Overview](https://docs.langchain.com/oss/python/langgraph/overview)
- [Anthropic: Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)
- [GitHub REST API: Issues](https://docs.github.com/en/rest/issues/issues)
- [GitHub REST API: Rate limits](https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api)

## Further reading

- [MCP Fundamentals: Stateless Requests and JSON-RPC](https://aiengineeringfromscratch.com/lesson?path=phases%2F13-tools-and-protocols%2F06-mcp-fundamentals)
- [Building an MCP Server](https://aiengineeringfromscratch.com/lesson?path=phases%2F13-tools-and-protocols%2F07-building-an-mcp-server)
- [Building an MCP Client](https://aiengineeringfromscratch.com/lesson?path=phases%2F13-tools-and-protocols%2F08-building-an-mcp-client)
- [MCP Security: Poisoned Metadata, Routing](https://aiengineeringfromscratch.com/lesson?path=phases%2F13-tools-and-protocols%2F15-mcp-security-tool-poisoning)

## Check yourself

Answer out loud before opening each answer.

<details><summary>What are the host, the client and the server, and which of them talks to the model?</summary>

The host is the user-facing application and owns the model and permissions; it runs one client per server connection; the server exposes tools, resources and prompts. Only the host talks to the model; servers only receive the requests the host chooses to send.

</details>

<details><summary>How does a 2026-07-28 client tell a server its protocol version and capabilities, and what happens on a mismatch?</summary>

Every request carries them in `params._meta` (`io.modelcontextprotocol/protocolVersion` and `io.modelcontextprotocol/clientCapabilities`). An unsupported version gets error `-32022` with a `supported` list, and the client retries with one of those versions.

</details>

<details><summary>What is the one thing every local MCP host needs from you, and why do absolute paths matter so much?</summary>

The command that starts your server. Hosts launch it from their own working directory with a minimal environment, so relative paths and shell-only environment variables do not resolve.

</details>

<details><summary>Your stdio server works when you run your test client but Claude Desktop shows it as failed. Where do you look first?</summary>

Run the exact launch command from the config yourself, then read `mcp-server-<name>.log` (the server's stderr) and `mcp.log` in Claude Desktop's log folder.

</details>

<details><summary>In one sentence each, what do CrewAI and LangGraph ask you to describe?</summary>

CrewAI asks you to describe a team: agents with roles, the tasks assigned to them and a process for handing out work. LangGraph asks you to describe a state machine: the shared state, the steps that update it and the edges that choose the next step.

</details>

<details><summary>What does `context=[find]` on a CrewAI task actually do to the next model call?</summary>

It inserts the earlier task's output text into the next task's prompt under a "context you're working with" heading. There is no other channel; the next agent sees it as prose.

</details>

<details><summary>Which two questions most often settle the choice between a plain loop, LangGraph and CrewAI, and why?</summary>

Control (must the next step be decided by code you can audit, or by model judgement) and durability (must a run pause and resume across restarts). They determine whether you need explicit routing and persistent checkpoints, which are the expensive things to build by hand.

</details>

<details><summary>How does putting your tools behind an MCP server change the lock-in question?</summary>

The client-specific, expensive part (data access, validation, permissions) becomes portable across any MCP client, so only the thin orchestration layer depends on the framework, and switching frameworks later costs much less.

</details>

---

**Learn Week 6 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week06). Week 1 is free.
