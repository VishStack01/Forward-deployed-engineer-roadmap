<p align="center"><img src="assets/banner.png" alt="Forward Deployed Engineer Roadmap, India 2026" width="100%"></p>

# Forward Deployed Engineer Roadmap (India, 2026)

A free, week-by-week roadmap to becoming a **Forward Deployed Engineer (FDE)**: the engineer who takes AI from a demo to a client's production systems. Written for working software engineers and AIML graduates in India.

Every week ends with one thing you ship. Follow it on your own with free resources, or use the [Zero to FDE course](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo), which teaches each week as hands-on lessons ([Week 1 is free](https://zero-to-fde-90-days.site/free-week-1?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo)).

## What is a Forward Deployed Engineer?

An FDE sits with a client, finds the real problem, connects AI to messy data and existing systems, and ships something that runs. The role combines a software engineer, an AI engineer and a solutions consultant. [Full explainer](https://zero-to-fde-90-days.site/what-is-a-forward-deployed-engineer).

## Why now

- FDE job postings in India grew about 19x between June 2025 and June 2026 (Indeed data, [reported by PTI](https://www.peoplematters.in/news/workforce-planning/demand-for-forward-deployed-engineers-jumps-19-fold-in-india-report-52770)).
- 52 organisations in India were hiring FDEs in July 2026, and an estimated ~1,200 engineers are fully ready for the role ([CIEL HR](https://www.cielhr.com/?p=357198)).
- 45% of current FDEs came from software engineering ([Bloomberry, 1,000 job posts](https://bloomberry.com/blog/i-analyzed-1000-forward-deployed-engineer-jobs-what-i-learned/)).

These are market figures, not a promise of a job or salary.

## Month 1: Foundations

### Week 1: Python and the engineering floor

*Backend basics, not notebooks.*

- Python as backend code, not notebook code
- Git and GitHub as a team sport: snapshots, branches, pull requests and merge conflicts
- The command line as a power tool: streams, pipes, curl and calm stack-trace reading
- HTTP from first principles, then a tested FastAPI CRUD service
- SQL from the relational model up: keys, joins, grouping, NULLs and indexes

**You ship:** A tested FastAPI CRUD service on a real database, pushed to GitHub.

### Week 2: How LLMs actually work

*The mechanics, not the marketing.*

- Tokens, context windows, sampling and embeddings
- Calling Claude and OpenAI directly, over raw HTTP and the SDKs
- Structured outputs and tool calling at the raw API level
- Prompts as application code: structure, examples, reasoning and tests
- Guided reading of Building Effective Agents, then planning your first agent

### Week 3: Retrieval, from first principles

*RAG before you ever say the word RAG.*

- Embeddings and chunking, the decisions that make or break retrieval
- A vector database by hand, pgvector first and Chroma second
- Hybrid search, reranking, and measuring retrieval with recall@k
- Naive RAG with no framework, then planning your document Q&A tool

**You ship:** A document Q&A tool that cites its sources.

### Week 4: The agent loop, by hand

*Understand what frameworks abstract away.*

- The ReAct loop by hand: call, parse, execute, feed back
- Agent memory three ways: buffer, rolling summary, retrieval
- When tools fail: retries, timeouts, backoff and honest error reports
- Breaking your agent on purpose: malformed output, guards, and the Week 4 build

**You ship:** An agent loop built by hand, with failure handling.

## Month 2: Agentic systems

### Week 5: LangGraph, properly

*The current production standard for stateful agents.*

- State graphs: nodes, edges, reducers and conditional routing
- Checkpoints, threads and streaming: agents that survive restarts and show their work
- Human-in-the-loop with interrupt(): pausing a graph until a person decides
- Week 4's agent, rebuilt in LangGraph: a line-by-line comparison

**You ship:** A stateful LangGraph agent with checkpoints and human-in-the-loop.

### Week 6: MCP and the tool ecosystem

*Now assumed, not optional.*

- The Model Context Protocol from the spec up, and a real MCP server
- Connecting an MCP server to real clients: Inspector, Claude, your own host, and what can go wrong
- CrewAI's crews and LangGraph's graphs: two mental models for multi-step agents
- LangGraph, CrewAI or a plain loop: choosing, writing the decision down, and planning your MCP server

**You ship:** A working MCP server connected to real clients.

### Week 7: Multi-agent systems and memory

*Know when it earns its complexity.*

- Supervisor, handoff, hierarchy: how agents actually work together
- Short-term, episodic and long-term memory, and what never to store
- When multi-agent is overkill: arguing it with a cost model
- Designing the failure path: when one agent in the chain returns garbage

### Week 8: Evaluation, the actual differentiator

*Where most candidates stop, and where you do not.*

- A golden dataset for your multi-agent system, case by case
- Graders, exact match where you can and an LLM judge where you must
- Calibrating your LLM judge against human labels
- Tracing the multi-agent system with LangSmith, then planning the Week 8 build

**You ship:** A golden dataset and an evaluation suite with a calibrated LLM judge.

## Month 3: Production and hiring

### Week 9: Observability, cost, and guardrails

*Proving to a security team the agent is safe.*

- Tracing every model and tool call, and finding the slow step
- Where the money goes, a running cost dashboard from token usage
- Guardrails at both edges, redacting Indian PII going in and checking replies going out
- Gating expensive actions, then planning the Week 9 build

**You ship:** Tracing, a cost dashboard and guardrails with PII redaction.

### Week 10: Real deployment

*Off localhost, onto the internet.*

- Containers from first principles, then a production Dockerfile for your agent service
- Off localhost - deploying the agent service to Render, with Fly.io as the alternative
- Configuration and secrets - nothing hardcoded, nothing leaked, and the first hour after a leak
- Auth for agent actions - who is asking, what they may do, and the Week 10 deliverable

**You ship:** The agent service deployed off localhost, with secrets and auth.

### Week 11: The portfolio and the niche

*Go narrow, it is where the money actually is.*

- Choosing a niche and finding a workflow worth automating
- Your third system: scope, cost and polish for one expensive workflow
- Messy data, and writing down everything that broke
- Case studies that prove it worked, and your Week 11 portfolio

### Week 12: Interview readiness sprint

*You are not studying anymore, you are rehearsing.*

- Two timed passes through the DSA patterns, practised like an interview
- Two mock system-design interviews, a RAG design and an agent design
- Two mock behavioural interviews, with a STAR story bank built from your projects
- An FDE resume, LinkedIn and ten targeted outreach messages, then the Week 12 deliverable

## Month 4: Enterprise track (optional)

### Week 13: Data engineering, the bedrock a client audit needs

*Untangle the mess before you build on it.*

- Advanced SQL for a data audit - window functions, recursive CTEs and reading EXPLAIN plans
- The Medallion architecture - Bronze, Silver and Gold, and why the layers exist
- Star schema versus One Big Table, and choosing for a real client dataset
- Distributed data basics - partitions, shuffles, skew and OOM, then the Week 13 data audit

**You ship:** A data audit of a messy real dataset.

### Week 14: Cloud architecture at client scale

*You are deploying into someone else's environment, not your own.*

- Cloud networking for client deployments - VPCs, private clusters and connecting the on-prem data centre
- Managed Kubernetes - what EKS, GKE and AKS run for you, and what you still own
- Infrastructure as code with Terraform - state, plans, and a database, network and access policy from one script
- Data exfiltration and security perimeters for regulated clients, then the Week 14 Terraform deliverable

**You ship:** Network, database and access policy from one Terraform script.

### Week 15: The consulting mindset

*Solve the people problem so the technical solution can work.*

- MECE decomposition, from "make us more efficient with AI" to tasks you can actually build
- The Pyramid Principle, answer first, so an executive can stop reading at any line
- The Three Whys, system of record, cost of doing nothing, and who owns it after you leave
- Running a discovery conversation and turning a vague ask into a one-page scope

### Week 16: Case interview practice

*Enterprise FDE interviews test judgment, not just code.*

- The C.A.S.E. framework, Clarify, Architect, Solve the Delta, Evaluate
- The hospital readmission case, worked in full, then redone cold
- Answering enterprise FDE questions out loud in under three minutes
- Writing a Site Survey and an Executive Status Report, and the three-document deliverable

## Tools you will use

| Tool | What it's for | Official docs |
| --- | --- | --- |
| Python | Backend and AI code | [docs.python.org](https://docs.python.org/3/) |
| FastAPI | APIs and agent services | [fastapi.tiangolo.com](https://fastapi.tiangolo.com/) |
| PostgreSQL | Client data, vectors via pgvector | [postgresql.org/docs](https://www.postgresql.org/docs/) |
| Git and GitHub | Version control, pull requests | [git-scm.com/book](https://git-scm.com/book/en/v2) |
| pytest | Tests | [docs.pytest.org](https://docs.pytest.org/) |
| Claude API | LLM calls, tool use | [docs.anthropic.com](https://docs.anthropic.com/) |
| OpenAI API | LLM calls, structured outputs | [platform.openai.com/docs](https://platform.openai.com/docs) |
| pgvector, Chroma | Vector search for RAG | [github.com/pgvector/pgvector](https://github.com/pgvector/pgvector), [docs.trychroma.com](https://docs.trychroma.com/) |
| LangGraph | Stateful agents | [langchain-ai.github.io/langgraph](https://langchain-ai.github.io/langgraph/) |
| CrewAI | Multi-agent crews | [docs.crewai.com](https://docs.crewai.com/) |
| Model Context Protocol | Connecting tools to models | [modelcontextprotocol.io](https://modelcontextprotocol.io/) |
| LangSmith | Tracing and evaluation | [docs.smith.langchain.com](https://docs.smith.langchain.com/) |
| Docker | Containers | [docs.docker.com](https://docs.docker.com/) |
| Terraform | Infrastructure as code | [developer.hashicorp.com/terraform](https://developer.hashicorp.com/terraform/docs) |
| Kubernetes | Running services at client scale | [kubernetes.io/docs](https://kubernetes.io/docs/home/) |
| Claude Code, Cursor, Copilot, Codex | AI-assisted coding | Each tool's own docs |

## Interview preparation

FDE interviews usually combine coding, an AI system design round (design a RAG system or an agent for a client), and a customer scenario or decomposition round where you break a vague business problem into something buildable. Weeks 12, 15 and 16 cover all three.

## FAQ

**Do I need an ML background?** No. FDE work is mostly software engineering plus the AI layer. Basic Python is enough to start.

**How long does it take?** About 10 to 15 hours a week for the 12 core weeks. Weeks 13 to 16 are an optional enterprise track.

**I'm already working. Can I follow this part-time?** Yes. It's built for working engineers: one deliverable a week, no fixed class times.

**Is this a job guarantee?** No. Nobody can promise that. What you get is a portfolio of shipped systems and practice for the interview rounds.

## Contributing

Found a broken link or a better resource? Open an issue or a pull request.

## License

CC BY 4.0. Share and adapt with attribution.

---

**Join the https://zero-to-fde-90-days.site/ program to learn all of these.**
