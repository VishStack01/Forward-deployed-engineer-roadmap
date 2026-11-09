# Week 8: Evaluation, the actual differentiator

**Month 2: Agentic systems, frameworks, tools, evaluation** · Where most candidates stop, and where you do not · 4 lessons · about 14 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 7](week-07.md) · [Week 9 →](week-09.md)

## What you will be able to do

- Write a golden dataset of 10 to 20 real test cases for your Week 7 system
- Score outputs both by exact match where possible and by LLM-as-judge where it is not
- Sanity-check your judge against your own human labels on a sample, and note where they disagree
- Instrument the system with one observability tool (LangSmith if you used LangGraph, otherwise Langfuse or Arize Phoenix)

## You ship this week

> An eval suite for your multi-agent system with a pass/fail view, plus at least one real regression you caught before it shipped.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. A golden dataset for your multi-agent system, case by case

*About 3 hours*

Last week you built a supervisor that routes work to specialist agents. Right now the only evidence that it works is that you tried a few requests and the answers looked fine. That is not evidence a client can rely on, and it will not survive the first prompt edit, model upgrade or new tool. A golden dataset is the fixed set of realistic requests, each with a written statement of what a good result looks like, that every version of your system is measured against. It turns "seems better" into "passes 14 of 16, and here are the two it fails". Everything else this week, scoring, LLM judges, observability, sits on top of it. A weak dataset makes every later number meaningless, so this is the lesson to do slowly.

Covers: The mental model: the specification, written as examples; Requirement in prose; A golden case; Where good cases come from; The schema of a case; Outcome, trajectory, or both; A dataset, a loader and a coverage report.

### 2. Graders, exact match where you can and an LLM judge where you must

*About 3.5 hours*

A golden dataset without graders is a list of questions. To turn it into a number you trust, every expectation in every case needs a grader: a piece of code, a model call or a person that looks at one trial and says pass or fail, with a reason. Pick graders badly and the eval lies in one of two directions. Strict string checks fail correct replies because they say "Rs 10000" instead of "₹10,000", and the team stops believing the eval. Loose LLM judges pass replies that sound good and are wrong, and the team believes the eval when it should not. An FDE is expected to know which grader fits each expectation, to make the cheap deterministic ones carry as much of the load as possible, and to treat an LLM judge as a measuring instrument with known biases, not an oracle.

Covers: The mental model: a ladder of graders; Deterministic metrics, done carefully.

### 3. Calibrating your LLM judge against human labels

*About 3 hours*

In the last lesson you built an LLM judge, and every judged criterion in your eval suite now rests on it. Until you have checked it against a person, you do not know whether a "pass" means the reply is good or that the judge was impressed by a long, polite paragraph. Clients and interviewers ask the same question: "How do you know your judge is right?" "It is a strong model" is not an answer. "I labelled 40 of its verdicts blind, it agreed on 32, kappa was about 0.55, it waved through five replies I failed, and here is what I changed" is an answer. This lesson teaches you to measure a judge the way you would measure any classifier, to read the disagreements instead of only counting them, and to improve the rubric without fooling yourself.

Covers: The mental model: the judge is a classifier, and you are its test set; Before the judge: can two humans agree?; Building the labelled sample; Agreement in code: accuracy, kappa, and the confusion matrix.

### 4. Tracing the multi-agent system with LangSmith, then planning the Week 8 build

*About 4 hours*

Your eval suite now tells you *that* case `wrong-route-bug` failed on v2. It does not tell you *why*. Did the supervisor choose the wrong agent, did the researcher's search return nothing, did the critic approve a bad draft? In a system with four agents and a dozen model calls per request, "why" lives in the sequence of calls, and you cannot reconstruct it from the final reply. A trace records that sequence: every agent, model call and tool call, with its inputs, outputs, timing and tokens, in one tree. Evals and traces are two halves of one loop. The eval finds the failing case; the trace explains it; the fix becomes a new eval run you can compare. This lesson sets up one tool end to end, links its traces to your eval runs, keeps personal data out of the logs, and then helps you plan this week's deliverable.

Covers: The mental model: a trace is a call tree with receipts; A tracer by hand, so the tool holds no mystery.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [Anthropic Engineering: Demystifying evals for AI agents](https://anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [Anthropic docs: Define success criteria and build evaluations](https://platform.claude.com/docs/en/test-and-evaluate/develop-tests)
- [LangSmith docs: Evaluation concepts (datasets, examples, versions, splits)](https://docs.langchain.com/langsmith/evaluation-concepts)
- [JSON Lines format](https://jsonlines.org/)
- [Zheng et al., Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena (arXiv:2306.05685)](https://arxiv.org/abs/2306.05685)
- [Liu et al., G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment (arXiv:2303.16634)](https://arxiv.org/abs/2303.16634)
- [Anthropic docs: Structured outputs](https://platform.claude.com/docs/en/build-with-claude/structured-outputs)
- [Shankar et al., Who Validates the Validators? Aligning LLM-Assisted Evaluation of LLM Outputs with Human Preferences (arXiv:2404.12272)](https://arxiv.org/abs/2404.12272)
- [scikit-learn: cohen_kappa_score](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.cohen_kappa_score.html)
- [LangSmith docs: Trace with LangGraph](https://docs.langchain.com/langsmith/trace-with-langgraph)
- [LangSmith docs: Observability concepts (runs, traces, threads, retention)](https://docs.langchain.com/langsmith/observability-concepts)
- [LangSmith docs: Prevent logging of sensitive data in traces](https://docs.langchain.com/langsmith/mask-inputs-outputs)
- [LangSmith docs: Evaluate an LLM application](https://docs.langchain.com/langsmith/evaluate-llm-application)
- [OpenTelemetry: Traces](https://opentelemetry.io/docs/concepts/signals/traces/)

## Further reading

- [Evaluation & Testing LLM Applications](https://aiengineeringfromscratch.com/lesson?path=phases%2F11-llm-engineering%2F10-evaluation)
- [LLM Evaluation: RAGAS, DeepEval, G-Eval](https://aiengineeringfromscratch.com/lesson?path=phases%2F05-nlp-foundations-to-advanced%2F27-llm-evaluation-frameworks)
- [Eval-Driven Agent Development](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F30-eval-driven-agent-development)

## Check yourself

Answer out loud before opening each answer.

<details><summary>Why is "the reply must cite POL-PREPAY-02 and mention ₹10,000" usually a better expectation than a full reference reply?</summary>

Many different replies are correct. Assertions check the properties every correct reply must have, so valid wording variations pass, while a full reference fails good answers for irrelevant differences.

</details>

<details><summary>Your eval set has 15 cases and the new version scores one case higher than the old one. What can you conclude?</summary>

Very little on its own: one case is about 7 points and runs vary. Look at which case changed, read both transcripts, and run several trials before calling it an improvement. Per-tag results and the specific case matter more than the total.

</details>

<details><summary>Why does the eval runner check citations with code even though the judge could check them too?</summary>

Code is free, instant and reproducible, and a citation is a closed value that code checks perfectly. Spending a judge call on it adds cost and non-determinism without adding accuracy.

</details>

<details><summary>Token F1 between "₹10,000" and "₹1,000" is 0.5 after normalisation. What does that tell you about F1?</summary>

It measures word overlap, not correctness, so a wrong number gets partial credit. It suits short extractive answers where overlap means partial correctness, never as the only check on a fact.

</details>

<details><summary>Your judge agrees with you on 90% of items. Why might that still be a bad judge?</summary>

If about 90% of items truly pass, a judge that always says pass also scores 90%. Check kappa, which corrects for chance agreement, and the confusion matrix, especially false passes.

</details>

<details><summary>Why label blind, without seeing the judge's verdict?</summary>

Seeing the verdict anchors you towards it, so agreement goes up for reasons that have nothing to do with the judge's quality.

</details>

<details><summary>What is the difference between a trace and a span?</summary>

A trace is the whole record of one request; a span (a run in LangSmith) is one unit of work inside it, such as an agent step, a model call or a tool call. Spans share the trace id and point to their parent, which gives the trace its tree shape.

</details>

<details><summary>Why should a trajectory check read the route from the trace rather than from the system's output?</summary>

The output is the system's own account, and a bug can make it report the route it intended rather than the one it took. The spans record what actually ran.

</details>

---

**Learn Week 8 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week08). Week 1 is free.
