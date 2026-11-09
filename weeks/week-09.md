# Week 9: Observability, cost, and guardrails

**Month 3: Production, deployment, and getting hired** · Proving to a security team the agent is safe · 4 lessons · about 14 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 8](week-08.md) · [Week 10 →](week-10.md)

## What you will be able to do

- Full tracing on every LLM and tool call: inputs, outputs, latency, token counts
- A running cost dashboard: token spend by session, and where the money is actually going
- One input guardrail (PII redaction or a basic prompt-injection check) and one output guardrail
- Sandbox or gate any action your agent takes that would be expensive to get wrong

## You ship this week

> Your Week 7 system with full tracing, a live cost view, and at least one guardrail that blocks a destructive action without explicit confirmation.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. Tracing every model and tool call, and finding the slow step

*About 3.5 hours*

Week 8 gave you tracing for evaluation: one tool, wired so every eval trial is a tree you can open. Production asks harder questions. A security reviewer wants to know what the agent sent to the model and what it is allowed to keep. An operations lead asks why replies take nine seconds on Monday mornings. Finance asks which feature burns the tokens. All three are answered from the same data, but only if *every* model call and *every* tool call is a span with the same shape: inputs (or a safe summary), outputs, latency, token counts, errors, and ids that join to the request the customer actually made. Partial tracing is worse than it looks, because the slow or expensive step is usually the one nobody instrumented. This lesson makes coverage complete, uses the vendor-neutral vocabulary so your traces survive a change of tool, and turns a pile of spans into percentiles that point at the real bottleneck.

Covers: The mental model: one schema, three questions; Span anatomy, the OpenTelemetry way; The GenAI semantic conventions, and their real status; Instrument every call through one wrapper.

### 2. Where the money goes, a running cost dashboard from token usage

*About 3 hours*

The first invoice is when a client's finance team meets your agent. If you cannot say which feature, which customer conversations and which step produced it, the conversation becomes "turn it off until we understand it". Agents make this harder than ordinary API spend: one customer email can trigger a dozen model calls, a critic loop can multiply the cost of one conversation by ten, and cached tokens, cache writes and batch discounts mean that token counts alone do not give you the bill. An FDE who can show, on day one, the cost per resolved email, the five most expensive sessions and the step that dominates spend, earns the trust to keep the system running and the room to make it cheaper. This lesson builds that view from the usage fields every API response already returns, with prices kept in configuration where they belong.

Covers: The mental model: a ledger, not a guess; Reading the usage fields correctly; Prices belong in config, dated and sourced; A day of spend, aggregated.

### 3. Guardrails at both edges, redacting Indian PII going in and checking replies going out

*About 3.5 hours*

A bank's security reviewer will ask two questions about your agent before it touches a real customer. What personal data reaches the model provider and your logs? And what stops the agent from saying or doing something the bank never authorised, because a customer, or a document the agent read, told it to? Prompts are not an answer to either, because a model can be talked out of its instructions. Guardrails are: deterministic checks in code at the boundaries, with a defined action when they fire. This lesson builds one input guardrail properly (a PII redactor for Indian identifiers, with a real checksum and tests), shows what a prompt-injection screen can and cannot do, builds output checks that block ungrounded or unauthorised replies, and, most importantly, measures how often each one is wrong, because a guardrail that blocks one honest customer in five will be switched off within a week.

Covers: The mental model: a check, a boundary, an action, a measured error rate; Input guardrail: a PII redactor for Indian identifiers.

### 4. Gating expensive actions, then planning the Week 9 build

*About 4 hours*

Everything so far this week reduces the chance that the agent does something wrong. This lesson limits what happens when it does anyway. Sooner or later a model will misread a message, a document will carry an injection your screen misses, or a bug will call the right tool with the wrong amount. Whether that becomes a non-event or an incident depends on one thing: whether the action had to pass through code that the model cannot talk its way past. Waiving a fee, changing a repayment date, emailing a customer or deleting a record are the moments when an agent's mistake costs real money or real trust. A security team signs off on an agent when you can show them, for every such action, what limits it, who approves it, what happens on a retry, and where the record of it lives. This lesson builds that gate and then helps you plan the week's deliverable.

Covers: The mental model: the model proposes, code disposes; Classify every action before you build anything; The controls, and what each one stops; An action gate, end to end.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [OpenTelemetry: Traces (spans, span kinds, context propagation)](https://opentelemetry.io/docs/concepts/signals/traces/)
- [OpenTelemetry: Sampling (head and tail sampling)](https://opentelemetry.io/docs/concepts/sampling/)
- [OpenTelemetry GenAI semantic conventions repository (status: Development)](https://github.com/open-telemetry/semantic-conventions-genai)
- [W3C Trace Context recommendation (the traceparent header)](https://www.w3.org/TR/trace-context/)
- [OpenTelemetry Python: Instrumentation](https://opentelemetry.io/docs/languages/python/instrumentation/)
- [Anthropic docs: Pricing (models, caching multipliers, batch, data residency)](https://platform.claude.com/docs/en/about-claude/pricing)
- [Anthropic docs: Prompt caching (usage fields and total input formula)](https://platform.claude.com/docs/en/build-with-claude/prompt-caching)
- [OpenAI API docs: Prompt caching (cached_tokens and cache_write_tokens)](https://developers.openai.com/api/docs/guides/prompt-caching)
- [Anthropic docs: Usage and Cost API (reconciliation)](https://platform.claude.com/docs/en/manage-claude/usage-cost-api)
- [OWASP GenAI: LLM10:2025 Unbounded Consumption](https://genai.owasp.org/llmrisk/llm102025-unbounded-consumption/)
- [OWASP GenAI: LLM01:2025 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- [OWASP GenAI: LLM05:2025 Improper Output Handling](https://genai.owasp.org/llmrisk/llm052025-improper-output-handling/)
- [Anthropic docs: Mitigate jailbreaks and prompt injections](https://platform.claude.com/docs/en/test-and-evaluate/strengthen-guardrails/mitigate-jailbreaks)
- [Income Tax Department: How PAN is formed](https://www.incometaxindia.gov.in/w/how-pan-is-formed-and-how-it-gets-its-unique-identity-)
- [python-stdnum: Aadhaar format and Verhoeff check digit](https://arthurdejong.org/python-stdnum/doc/stdnum.in_.aadhaar)
- [OWASP GenAI: LLM06:2025 Excessive Agency](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/)
- [LangGraph docs: Interrupts](https://docs.langchain.com/oss/python/langgraph/interrupts)
- [Stripe API: Idempotent requests](https://docs.stripe.com/api/idempotent_requests)
- [OWASP Top 10 for LLM Applications 2025](https://genai.owasp.org/llm-top-10/)

## Further reading

- [Caching, Rate Limiting & Cost Optimization](https://aiengineeringfromscratch.com/lesson?path=phases%2F11-llm-engineering%2F11-caching-cost)
- [Guardrails, Safety & Content Filtering](https://aiengineeringfromscratch.com/lesson?path=phases%2F11-llm-engineering%2F12-guardrails)
- [Agent Observability: Langfuse, Phoenix, Opik](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F24-agent-observability-platforms)
- [OpenTelemetry GenAI Semantic Conventions](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F23-otel-genai-conventions)

## Check yourself

Answer out loud before opening each answer.

<details><summary>Why can head sampling not guarantee that every failing request is kept?</summary>

It decides when the trace starts, before any error has happened. Keeping all errors needs tail sampling, which decides after the trace completes.

</details>

<details><summary>Your dashboard shows cached prompts made input tokens fall by 90% overnight, but the invoice barely changed. What is the likely bug?</summary>

You recorded Anthropic's `input_tokens`, which excludes cache reads and writes, as the total. Cache reads are cheap but not free, and writes cost more than base input, so total input should include them.

</details>

<details><summary>An Anthropic response reports `input_tokens: 300`, `cache_read_input_tokens: 3000`, `output_tokens: 200`. How many input tokens did the model process, and what do you bill at the full input rate?</summary>

3,300 input tokens in total. Only the 300 uncached tokens are billed at the full input rate; the 3,000 cache reads are billed at the cache-read multiplier.

</details>

<details><summary>Why must a dashboard not compute spend from sampled traces?</summary>

Sampling deliberately drops traces, so totals undercount by the sampling rate and are biased toward whichever traces the rules keep. Spend needs every call, so it comes from an unsampled ledger or metrics.

</details>

<details><summary>Why does validating Aadhaar with Verhoeff reduce false positives so much?</summary>

Only about one random twelve-digit number in ten has a valid Verhoeff check digit, so most account and reference numbers that merely look like Aadhaar fail the check and are left alone. A regex alone matches all of them.

</details>

<details><summary>Your injection screen has 100% precision at threshold two. Why might you still ship threshold one?</summary>

At threshold two recall was 25%, so most attacks pass unflagged. If the action on a flag is cheap (route to a human or a no-tools mode), catching more attacks is worth some false alarms; the right threshold depends on the cost of each error, not on precision alone.

</details>

<details><summary>Why is "the agent has no tool for it" the strongest gate for a large-blast-radius action?</summary>

Every other control can be misconfigured, bypassed or approved by mistake. An action that does not exist cannot be triggered by any prompt, injection or bug.

</details>

<details><summary>An approver clicks "approve" on a ₹500 waiver, and the executed waiver is ₹5,000. Which control was missing?</summary>

Binding the approval to the exact payload: the gate should store a hash of the action and arguments shown to the approver and refuse to execute anything that does not match it.

</details>

---

**Learn Week 9 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week09). Week 1 is free.
