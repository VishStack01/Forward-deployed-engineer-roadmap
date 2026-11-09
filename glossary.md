# FDE and AI engineering glossary

Plain-English definitions of the words you will hear in your first client meeting.

## The FDE job

**The Delta.** The gap between what a product does out of the box and what a specific client needs it to do. An FDE’s job is closing this gap with real code.

**System of Record (SoR).** The one authoritative data source for a given fact, for example SAP for finance or Salesforce for CRM. Find this before you build on anything, or you are building on a stale copy.

**Air-Gap / Tactical Edge.** An environment with zero or intermittent internet connectivity, common in defense, energy, and some healthcare settings. Requires offline model weights and local infrastructure.

**VPC Service Controls (VPC SC).** A cloud security perimeter that blocks data from being moved to unauthorized projects or services. Common requirement in finance and government engagements.

**Shadow IT.** Unauthorized tools or databases used by client employees outside official channels. Often where the cleanest, most current data actually lives.

**A2A Protocol (Agent2Agent).** An open standard letting autonomous agents discover and hand off tasks to each other across systems, independent of which framework built them.

**Groundedness.** Whether a model’s response is actually derived from the retrieved context it was given, rather than invented. The core metric for catching hallucination in a RAG system.

**SOW (Statement of Work).** The document that legally fences your project scope. If it is not in the SOW, asking for it is scope creep, not a small favor.

**MSA (Master Services Agreement).** The umbrella legal contract between your company and the client, signed before any specific project SOW.

**UAT (User Acceptance Testing).** The moment real client employees actually use what you built. If they do not accept it, the project is not done, regardless of code quality.

**Day 2 Operations.** Everything that happens after the FDE leaves: monitoring, retraining, and who on the client side owns it. A project with no answer to this question is not finished, it is abandoned.

**Cost of Inaction (CoI).** The argument for urgency: quantifying what the client loses every day they do not ship the solution. Often more persuasive to executives than a feature list.

*Several FDE terms and the warning signs in this repo are adapted from [Awesome-FDE-Roadmap](https://github.com/pierpaolo28/Awesome-FDE-Roadmap) by Pier Paolo Ippolito (MIT License, Copyright (c) 2026 Pier Paolo Ippolito).*

## AI engineering

**Token.** The unit a model reads and writes; roughly three-quarters of an English word. Pricing, limits and speed are all counted in tokens.

**Context window.** The maximum number of tokens a model can consider at once: your instructions, the conversation, retrieved documents and its own answer.

**Embedding.** A list of numbers representing the meaning of a piece of text, so that similar meanings sit close together. The basis of semantic search.

**Vector database.** A database that stores embeddings and finds the nearest ones to a query quickly. pgvector, Chroma, Qdrant and Pinecone are common choices.

**Chunking.** Splitting documents into passages before embedding them. Chunk size and boundaries decide whether retrieval can find the answer at all.

**RAG (retrieval-augmented generation).** Finding relevant passages from your own data first, then giving them to the model with the question so it answers from them and can cite them.

**Hybrid search.** Combining keyword search (good for exact names and IDs) with vector search (good for meaning), usually merged with reciprocal rank fusion.

**Reranking.** A second, more accurate model that reorders the top retrieved passages before they go to the LLM.

**recall@k.** The share of questions where the right passage appears in the top k results. The first number to check when a RAG system answers wrongly.

**Tool calling (function calling).** The model asks your code to run a named function with structured arguments; your code runs it and returns the result.

**Structured output.** Forcing the model to reply in a fixed JSON schema so your code can parse it reliably.

**Agent.** A loop where the model chooses a tool, your code runs it, and the model decides the next step until the task is done or a step limit is hit.

**ReAct.** A prompting pattern where the model alternates reasoning and actions (tool calls), using each observation to decide the next step.

**LangGraph.** A framework for building agents as graphs of steps with saved state, branches, retries and human approval points.

**MCP (Model Context Protocol).** An open protocol for exposing tools, data and prompts to any compatible AI client through a standard server.

**Multi-agent system.** Several specialised agents, often coordinated by a supervisor that routes work between them. Useful less often than people think.

**Human-in-the-loop.** A checkpoint where the system pauses for a person to approve, edit or reject an action before it happens.

**Evaluation (evals).** A fixed set of test inputs with expected behaviour, scored automatically, so you can prove a change made things better and not worse.

**Golden dataset.** The curated set of questions and expected answers your evals run against. Usually built from real user questions.

**LLM-as-a-judge.** Using a model to grade outputs against a rubric. Useful at scale, but it must be checked against human labels first.

**Hallucination.** A confident answer that is not supported by the sources or the facts.

**Guardrails.** Checks around the model: input filtering, output validation, PII redaction, and blocking risky actions without confirmation.

**Prompt injection.** Text in user input or retrieved documents that tries to override your instructions, for example a web page telling the agent to email out data.

**PII.** Personally identifiable information: names, phone numbers, emails, ID numbers. Usually must be redacted before logging or sending to a third party.

**Tracing / observability.** Recording every model call, tool call, input, output, latency and cost so you can debug a bad answer after the fact.

**Latency: TTFT.** Time to first token: how long before the answer starts appearing. Users feel this more than total time.

**KV cache.** Stored attention keys and values from earlier tokens so the model does not recompute them for every new token. Why long prompts use so much GPU memory.

**Prompt caching.** Reusing the processed form of a repeated prompt prefix across requests to cut cost and latency.

**Quantization.** Storing model weights in fewer bits (for example 4-bit) to fit bigger models on smaller hardware, at a small quality cost.

**Fine-tuning.** Further training a model on your examples to change its behaviour or style. Rarely the first fix; try prompting and RAG first.

**LoRA / QLoRA.** Fine-tuning a small set of added weights instead of the whole model; QLoRA does it on a quantized model to save memory.

**Distillation.** Training a small model to imitate a larger one on a specific task, for lower cost and latency.

**Temperature.** A setting that controls randomness in the model's choice of next token. Lower is more predictable.

**Medallion architecture.** Organising data in Bronze (raw), Silver (cleaned) and Gold (business-ready) layers. Common in client data platforms.

**Infrastructure as code.** Defining cloud resources (databases, networks, permissions) in files such as Terraform so environments can be rebuilt exactly.
