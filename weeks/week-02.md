# Week 2: How LLMs actually work

**Month 1: Foundations, engineer before agent** · The mechanics, not the marketing · 5 lessons · about 13 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 1](week-01.md) · [Week 3 →](week-03.md)

## What you will be able to do

- Tokenization, context windows, temperature and top-p sampling, embeddings, conceptually and hands on
- Call the Claude API and one other model API directly, with raw HTTP or the SDK, no framework
- Structured outputs and function-calling schemas at the raw API level. This is the single most important mechanical skill for everything that follows
- Prompt fundamentals: few-shot examples, chain-of-thought, system-prompt design
- Read Anthropic’s "Building Effective Agents" post start to finish before writing another line of code

## You ship this week

> A command-line tool, no framework, that takes a plain-English instruction and calls the correct one of three Python functions you wrote via tool calling. This is agent-from-scratch number one.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. Tokens, context windows, sampling and embeddings

*About 2.5 hours*

Every bill, every latency spike and every "the model forgot what I told it" bug you will meet as an FDE traces back to four mechanics: how text becomes tokens, how much of it fits in the context window, how the next token is chosen, and how text becomes a vector you can compare. A client asks why their Hindi support bot costs more per conversation than the English one. Another asks why the assistant ignores the instructions at the top of a long chat. A third wants to know whether "temperature 0" makes answers repeatable. You cannot answer any of these from marketing pages. You answer them from the mechanics in this lesson, which you will also build on directly in Week 3 when embeddings become a retrieval system.

Covers: The mental model: a function from tokens to a probability distribution; Tokens and byte-pair encoding.

### 2. Calling Claude and OpenAI directly, over raw HTTP and the SDKs

*About 2.5 hours*

Every agent framework, every "AI platform" a client has bought, and every integration you will debug is, at the bottom, an HTTPS POST with a JSON body and a JSON response. When something breaks at a client site (a 429 storm at month-end, a 401 after a key rotation, a bill three times the estimate), the framework's error message is usually useless and the raw request is the only thing that tells the truth. If you have written that request by hand, you can read logs, reproduce failures with one `curl`, and explain to a client's security team exactly what leaves their network. This lesson makes the raw call familiar so that nothing above it is magic.

Covers: The mental model: one stateless HTTPS request per turn; Keys, environment variables and model names.

### 3. Structured outputs and tool calling at the raw API level

*About 3 hours*

An LLM that returns prose is a demo. An LLM that returns a validated object your code can act on is a system. Every agent you build from here on, including this week's deliverable, works the same way underneath: you describe functions with JSON Schema, the model replies with a structured request to call one, your code checks that request and runs it, and you send the result back. Extraction pipelines, routers, form fillers and multi-step agents are all variations of that cycle. If you understand it at the level of raw JSON, frameworks become optional conveniences. If you do not, every framework bug becomes a mystery, and every malformed response becomes a production incident.

Covers: The mental model: the model writes a request, your code decides whether to run it; JSON Schema in ten minutes; How tool definitions are sent; The request and response cycle; A dispatcher you can run offline.

### 4. Prompts as application code: structure, examples, reasoning and tests

*About 2.5 hours*

When you chat with a model, a bad prompt costs you one retry. When a prompt lives inside an application, it runs thousands of times a day on inputs you never saw, written by customers who may be confused, angry, multilingual or actively trying to break it. A vague instruction becomes a stream of misrouted tickets; a missing delimiter becomes a prompt-injection hole; an "improvement" made without tests quietly breaks the cases that used to work. Clients judge an AI system by its worst outputs, and most of those trace back to the prompt. This lesson treats prompts the way you treated functions in Week 1: as code with a clear contract, structured inputs, and tests. (The AI Skills module covers the different job of prompting a coding assistant while you work.)

Covers: The mental model: a prompt is a function template that runs on untrusted input; Fixed part; Variable part; Output; Anatomy of a good application prompt; System, developer and user messages; Structure with XML tags.

### 5. Guided reading of Building Effective Agents, then planning your first agent

*About 2.5 hours*

Clients will ask you for "an agent" when what they need is a single well-prompted call, and they will ask for "a simple chatbot" when the problem actually needs a loop with tools and a human checkpoint. Choosing the right amount of autonomy is the most consequential design decision in an FDE engagement: too little and the system cannot do the job, too much and it becomes slow, expensive, and hard to debug or trust. Anthropic's "Building Effective Agents" is the clearest short statement of how to make that choice, and much of the industry now uses its vocabulary. Read it before you write the Week 2 deliverable, because the deliverable is a deliberate first step on the ladder it describes.

Covers: How to read this post; The central distinction: workflows versus agents.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [Sennrich et al., Neural Machine Translation of Rare Words with Subword Units (BPE)](https://arxiv.org/abs/1508.07909)
- [Holtzman et al., The Curious Case of Neural Text Degeneration (nucleus / top-p sampling)](https://arxiv.org/abs/1904.09751)
- [Claude docs: Context windows](https://platform.claude.com/docs/en/build-with-claude/context-windows)
- [Claude docs: Token counting](https://platform.claude.com/docs/en/build-with-claude/token-counting)
- [openai/tiktoken: the open-source BPE tokenizer used by OpenAI models](https://github.com/openai/tiktoken)
- [Claude API reference: Messages](https://platform.claude.com/docs/en/api/messages)
- [Claude API: Errors](https://platform.claude.com/docs/en/api/errors)
- [Claude API: Rate limits](https://platform.claude.com/docs/en/api/rate-limits)
- [OpenAI API: Text generation with the Responses API](https://developers.openai.com/api/docs/guides/text)
- [OpenAI API: Error codes](https://developers.openai.com/api/docs/guides/error-codes)
- [Claude docs: Tool use overview](https://platform.claude.com/docs/en/agents-and-tools/tool-use/overview)
- [Claude docs: Handle tool calls (tool_result, is_error, ordering)](https://platform.claude.com/docs/en/agents-and-tools/tool-use/handle-tool-calls)
- [Claude docs: Structured outputs](https://platform.claude.com/docs/en/build-with-claude/structured-outputs)
- [OpenAI API: Function calling](https://developers.openai.com/api/docs/guides/function-calling)
- [JSON Schema reference: object (properties, required, additionalProperties)](https://json-schema.org/understanding-json-schema/reference/object)
- [Claude docs: Prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)
- [Claude docs: Prompt engineering overview](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview)
- [Claude docs: Define success criteria and build evaluations](https://platform.claude.com/docs/en/test-and-evaluate/develop-tests)
- [OpenAI API: Prompt engineering guide](https://developers.openai.com/api/docs/guides/prompt-engineering)
- [OWASP GenAI: LLM01:2025 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- [Anthropic Engineering: Building Effective Agents (December 2024)](https://www.anthropic.com/engineering/building-effective-agents)
- [Claude docs: Define tools (descriptions, tool_choice, input examples)](https://platform.claude.com/docs/en/agents-and-tools/tool-use/define-tools)

## Further reading

- [Prompt Engineering: Techniques & Patterns](https://aiengineeringfromscratch.com/lesson?path=phases%2F11-llm-engineering%2F01-prompt-engineering)
- [Structured Outputs: JSON, Schema Validation](https://aiengineeringfromscratch.com/lesson?path=phases%2F11-llm-engineering%2F03-structured-outputs)
- [Embeddings & Vector Representations](https://aiengineeringfromscratch.com/lesson?path=phases%2F11-llm-engineering%2F04-embeddings)
- [Subword Tokenization: BPE, WordPiece, SentencePiece](https://aiengineeringfromscratch.com/lesson?path=phases%2F05-nlp-foundations-to-advanced%2F19-subword-tokenization)

## Check yourself

Answer out loud before opening each answer.

<details><summary>Why are output tokens slower and usually more expensive than input tokens?</summary>

Input tokens can be processed in parallel in one pass, but output is generated one token at a time, each needing a full forward pass that depends on the previous token. More compute and time per token means a higher price.

</details>

<details><summary>A Telugu sentence and its English translation have the same number of words. Why might the Telugu one use several times more tokens?</summary>

Telugu script takes 3 bytes per code point in UTF-8, written syllables are often several code points, and if the tokenizer saw less Telugu during training it learned fewer merges for it, so words split into many small pieces.

</details>

<details><summary>Why must your code send the earlier conversation turns on every request?</summary>

The Messages API (and Responses used without server-side state) is stateless. The model only sees what is in the current request, so the application owns the history.

</details>

<details><summary>You get HTTP 529 from Anthropic. Is it your fault, and what should the code do?</summary>

No, it means the API is temporarily overloaded across users. Retry with exponential backoff and jitter, cap the attempts, and queue the work if it keeps failing.

</details>

<details><summary>What is the difference between JSON mode and schema-constrained structured outputs?</summary>

JSON mode guarantees the output is syntactically valid JSON. Structured outputs (or strict tools) constrain generation to your schema, so required fields, types and enums match. Only the second ensures schema adherence.

</details>

<details><summary>With strict mode on, why do you still validate the model's output in code?</summary>

The output can be truncated by `max_tokens`, the model can refuse, some schema constraints (numeric ranges, string lengths) are not enforced by the provider, and valid-looking values can still be wrong for the business. Validation catches all of these.

</details>

<details><summary>What belongs in the system prompt and what belongs in the user turn?</summary>

Stable role, rules, definitions and output format go in the system (or developer) prompt; fixed few-shot examples can go there or in a fixed prefix of the user turn, as in the builder above. Per-request data, such as the customer's message or retrieved documents, goes in the user turn.

</details>

<details><summary>Why escape user text before inserting it inside XML tags?</summary>

So the text cannot contain a closing tag that ends your delimiter early and makes the rest look like instructions. It keeps the structure intact but does not stop the model reading any instructions in the text.

</details>

---

**Learn Week 2 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week02). Week 1 is free.
