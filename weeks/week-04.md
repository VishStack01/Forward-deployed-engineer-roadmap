# Week 4: The agent loop, by hand

**Month 1: Foundations, engineer before agent** · Understand what frameworks abstract away · 4 lessons · about 13 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 3](week-03.md) · [Week 5 →](week-05.md)

## What you will be able to do

- Build the ReAct pattern yourself: a loop that calls the model, parses a tool call, executes it, feeds the result back
- Add three memory types: a simple buffer, a summarized history, and a vector-store lookup
- Add retries, timeouts, and exponential backoff for tool calls that fail
- Handle malformed model output on purpose: bad JSON, a hallucinated tool name, an infinite loop

## You ship this week

> A from-scratch agent loop, still zero frameworks, using three or more tools, that retries failed calls and stops cleanly when done or after a step limit. Keep this file. You will compare it to LangGraph next week.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. The ReAct loop by hand: call, parse, execute, feed back

*About 3 hours*

Every agent framework you will meet, LangGraph next week included, is a wrapper around one small loop: ask the model what to do, run the tool it asked for, show it the result, repeat until it says it is done. When a client's agent "hangs", "calls the same tool forever", or "gives up after one step", the bug is almost always in that loop: a missing stop condition, a tool result attached to the wrong call, a history the API rejects. If you have only ever used a framework, you cannot see the loop, so you cannot debug it. This lesson has you write it yourself, run it with no API key against a scripted fake model, and then point the same design at the real Anthropic Messages API.

Covers: The mental model: the model proposes, your code disposes; The ReAct idea; From text protocol to native tool use; The loop as a state machine; Message history: the shape the API insists on; A complete loop you can run with no API key.

### 2. Agent memory three ways: buffer, rolling summary, retrieval

*About 3 hours*

Your agent from the last lesson resends the entire conversation on every model call. That works for a five-step demo and fails in production: a support agent that has been talking to a customer for forty turns, with tool results full of order JSON, eventually sends a request the API refuses as too long, and long before that it gets slower, more expensive and less accurate. "Memory" in an agent is not a magic feature; it is your decision, made on every single call, about what goes into a context window that is finite. Clients will also ask the uncomfortable follow-ups: what exactly is the agent remembering about our customers, where is it stored, and can someone plant something in it? This lesson gives you three memory designs you can build and explain, plus the rules for what must never be stored.

Covers: The mental model: memory is what you choose to put in the next request; Buffer; Rolling summary; Retrieval; Counting tokens, approximately; Memory 1: a token-budgeted buffer; Memory 2: a rolling summary.

### 3. When tools fail: retries, timeouts, backoff and honest error reports

*About 3 hours*

In a demo every tool call succeeds. In a client's environment the shipping API returns 503 every afternoon at peak, the ERP takes 40 seconds to answer when its nightly batch is running, and the payments gateway rate-limits you at 429 when the marketing team sends a campaign. An agent loop without failure handling does one of three bad things: it crashes on the first exception, it hangs forever on a call that never returns, or, worst, it retries a non-idempotent call and issues the same refund twice. Retries, timeouts and backoff are old distributed-systems techniques, and an agent needs all of them plus one new skill: telling the model what went wrong in a way it can act on. This lesson builds each piece so you can run it and watch it work.

Covers: The mental model: decide, per failure, who should handle it; Retry in code; Report to the model; Stop and alert a human; Transient versus permanent errors; Idempotency: the question before any retry; Exponential backoff with full jitter; Timeouts without signals.

### 4. Breaking your agent on purpose: malformed output, guards, and the Week 4 build

*About 4 hours*

Models produce bad output. Not often, but at scale "not often" means every day: a tool call whose arguments are not valid JSON, a call to a tool that does not exist because the model guessed a plausible name, a number sent as a string, or the same search issued over and over while the bill climbs. A demo agent crashes or spins on these. A production agent detects each one, tells the model precisely what was wrong so it can correct itself, and stops cleanly when it cannot. The only reliable way to know your agent does this is to inject each failure deliberately and watch what happens. This lesson builds the guard layer and a test harness that drives it with a scripted fake model, then helps you plan the Week 4 deliverable.

Covers: The mental model: model output is untrusted input; Where malformed output comes from; Parsing defensively; Validating names and arguments, and feeding errors back; Detecting loops; A guarded loop and a failure-injection harness.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [Yao et al., ReAct: Synergizing Reasoning and Acting in Language Models (arXiv 2210.03629)](https://arxiv.org/abs/2210.03629)
- [Claude docs: Handle tool calls (tool_use and tool_result format)](https://platform.claude.com/docs/en/agents-and-tools/tool-use/handle-tool-calls)
- [Claude docs: Stop reasons and fallback](https://platform.claude.com/docs/en/build-with-claude/handling-stop-reasons)
- [Claude docs: Define tools](https://platform.claude.com/docs/en/agents-and-tools/tool-use/define-tools)
- [Anthropic Engineering: Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)
- [Claude docs: Context windows (context rot, compaction, context editing)](https://platform.claude.com/docs/en/build-with-claude/context-windows)
- [Claude docs: Token counting](https://platform.claude.com/docs/en/build-with-claude/token-counting)
- [Anthropic Engineering: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [Park et al., Generative Agents: Interactive Simulacra of Human Behavior (arXiv 2304.03442)](https://arxiv.org/abs/2304.03442)
- [OWASP GenAI Security Project: Top 10 for Agentic Applications for 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)
- [Marc Brooker, AWS Architecture Blog: Exponential Backoff And Jitter](https://aws.amazon.com/blogs/architecture/exponential-backoff-and-jitter/)
- [Claude docs: API errors (status codes, retry advice)](https://platform.claude.com/docs/en/api/errors)
- [Claude docs: Python SDK (retries, timeouts, error classes)](https://platform.claude.com/docs/en/cli-sdks-libraries/sdks/python)
- [Python docs: concurrent.futures](https://docs.python.org/3/library/concurrent.futures.html)
- [Stripe API: Idempotent requests](https://docs.stripe.com/api/idempotent_requests)
- [Claude docs: Strict tool use](https://platform.claude.com/docs/en/agents-and-tools/tool-use/strict-tool-use)
- [Python docs: json, including parse_constant and object_pairs_hook](https://docs.python.org/3/library/json.html)

## Further reading

- [The Agent Loop: Observe, Think, Act](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F01-the-agent-loop)
- [Tool Use and Function Calling](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F06-tool-use-and-function-calling)
- [Function Calling & Tool Use](https://aiengineeringfromscratch.com/lesson?path=phases%2F11-llm-engineering%2F09-function-calling)
- [Reflexion: Verbal Reinforcement Learning](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F03-reflexion-verbal-rl)

## Check yourself

Answer out loud before opening each answer.

<details><summary>Who executes a tool in an agent: the model or your program? Why does the answer matter for safety?</summary>

Your program. The model only emits a request; your loop decides whether and how to run it, so permission checks, validation and limits belong in your code, where they cannot be talked around by a prompt.

</details>

<details><summary>The model made two tool calls in one turn and the second tool raised an exception. What do you send back?</summary>

One user message containing two `tool_result` blocks, first in the content, each with its own `tool_use_id`; the failed one carries the error message and `"is_error": true`.

</details>

<details><summary>Why can you not cut a conversation history at any message boundary to fit a token budget?</summary>

The API requires the history to start with a user message and every `tool_use` to be answered by a `tool_result` in the next message. Cutting inside a tool exchange, or starting at a tool-result message, makes the request invalid, so you cut only at user turns that carry real text.

</details>

<details><summary>An agent loop adds about 1,000 tokens per step. Why is a 40-step run far more expensive than 40,000 input tokens?</summary>

Each step resends the whole history, so step n sends about n thousand tokens. Summed over 40 steps that is roughly 820,000 input tokens, which is why trimming and summarising pay off quickly.

</details>

<details><summary>A refund tool call times out. Why is a blind retry dangerous, and what makes a retry safe?</summary>

The server may have completed the refund and only the response was lost, so a retry can refund twice. It is safe when the write carries an idempotency key the server deduplicates on (the `tool_use` id works well), or when you first check whether the refund already exists.

</details>

<details><summary>Why add jitter to exponential backoff when the waits already grow?</summary>

Growth spaces out one client's retries but not many clients' retries: clients that failed together retry together and overload the service again. Full jitter spreads them randomly across the whole interval.

</details>

<details><summary>Your provider supports strict tool use, which guarantees schema-valid inputs and valid tool names. Why keep a guard layer?</summary>

Not every model or provider offers it, it supports only a subset of JSON Schema, and it cannot check meaning (a refund larger than the order, an id that does not exist). Validation in your code is also what lets you write precise error messages for self-correction.

</details>

<details><summary>Why should the parser not fix trailing commas or single quotes automatically?</summary>

A guessed repair can change what the call means, especially for truncated output, and hides the problem from your logs. Only repairs that cannot change content, like stripping a markdown fence, are safe; everything else goes back to the model as an error.

</details>

---

**Learn Week 4 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week04). Week 1 is free.
