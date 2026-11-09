# Week 12: Interview readiness sprint

**Month 3: Production, deployment, and getting hired** · You are not studying anymore, you are rehearsing · 4 lessons · about 19 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 11](week-11.md) · [Week 13 →](week-13.md)

## What you will be able to do

- Two full passes through the DSA pattern list, timing yourself on mediums
- Two mock system-design interviews: one RAG design, one agent design
- Two mock behavioral interviews using the STAR stories from the Interview Playbook tab
- Rewrite your resume and LinkedIn in forward-deployed-engineer language, and reach out to ten target companies or recruiters

## You ship this week

> You book a real interview, or you apply on purpose to the ten companies you actually researched, not fifty you did not.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. Two timed passes through the DSA patterns, practised like an interview

*About 5 hours*

Almost every FDE loop still has a coding screen, and it is usually the first technical filter. The Interview tab's stage list describes it as often project-style, sometimes with an AI assistant allowed. At Palantir, the archetypal FDE employer, the tab's notes say AI tools are prohibited throughout and the screen is live coding or a HackerRank. You can have three shipped projects and still be cut at this stage, because you froze on a sliding-window question you would have solved in your sleep with a notebook and no clock. This week is not about learning new algorithms. It is about making the 54 problems in the Problems tab automatic under a timer, out loud, with someone watching. Recognising a pattern quickly and then explaining it clearly is a separate skill from knowing it, and that skill only comes from timed practice.

Covers: The mental model: recognise, template, variations; The plan: two passes that train different skills.

### 2. Two mock system-design interviews, a RAG design and an agent design

*About 5 hours*

The system-design round is where an FDE loop decides whether you can be trusted alone with a client. The Interview tab's stage list says this round is graded on guardrails, cost and observability, not on cleverness, and its question bank opens with "Design a RAG system for a customer support chatbot" and "Design an agentic system ... with explicit guardrails and cost controls." You have built small versions of both in Weeks 3 to 10. What you have not done is design one out loud in 45 minutes, for a scale you have never run, with someone interrupting. Candidates who know the parts still fail this round by drawing boxes in a random order, skipping numbers, and never saying how they would know the system works. This lesson gives you a fixed framework, two fully worked designs with their numbers computed in code, and the questions interviewers use to probe.

Covers: The mental model: a design is a chain of decisions, each justified by a number or a risk; The framework, with a 45-minute budget; Mock 1: RAG over 2 million policy documents for an Indian insurer.

### 3. Two mock behavioural interviews, with a STAR story bank built from your projects

*About 4 hours*

For a forward deployed role, the behavioural round is not a formality after the "real" interviews. An FDE spends half their time with a client who is confused, impatient or sceptical, and the behavioural round is the company's only direct evidence of how you will handle that. The Interview tab says the round is weighted toward ownership and client-facing communication, and that the interviewer is listening for "ownership past the point where it stopped being fun" and for evidence that you can translate between an executive's language and an engineer's. Graduates lose this round in a predictable way: vague stories, "we" everywhere, no numbers, no result, and nothing learned. You have twelve weeks of real projects to draw on. This lesson turns them into a story bank, shows what a strong answer sounds like next to a weak one, and gives you a way to rehearse out loud until the answers are specific and not scripted.

Covers: The mental model: a behavioural answer is evidence, not a description of yourself; STAR done well: four properties; Building the story bank from the course; The common FDE questions; Worked example 1: a technical decision that turned out wrong; Worked example 2: pushback from a stakeholder; Practising out loud; Running the two mocks.

### 4. An FDE resume, LinkedIn and ten targeted outreach messages, then the Week 12 deliverable

*About 5 hours*

You now have three projects, case studies, a live deployment and an eval suite, and none of it helps if a recruiter skims your resume for a few seconds and sees "Proficient in Python, ML, Deep Learning, NLP." Most graduate resumes in India describe courses and tools; an FDE hiring manager is looking for evidence that you ship working systems into messy environments and can prove they work. The Get Hired tab ranks what actually moves an application, and resume formatting and keywords come last: necessary so you are not disqualified, not enough to get you picked. What moves the decision is proof (a published artifact, a merged contribution) and removing objections early (location, legal route, timezone). This lesson rewrites your resume and LinkedIn so they point at that proof, makes every claim defensible, writes ten outreach messages that get read, and plans the deliverable: a real interview booked, or ten deliberate applications.

Covers: The mental model: a resume is a list of claims, each with a pointer to proof; FDE language: say what you shipped, for whom, and how you know it works; Resume structure for FDE roles; The bullet formula, with numbers that come from your files; Being careful with claims; ATS reality, without the myths; LinkedIn: headline, About, Featured; Choosing ten targets on purpose.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [LeetCode 3: Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [LeetCode 973: K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)
- [LeetCode 200: Number of Islands](https://leetcode.com/problems/number-of-islands/)
- [Python docs: heapq, heap queue algorithm](https://docs.python.org/3/library/heapq.html)
- [Python wiki: TimeComplexity of list, deque, set and dict operations](https://wiki.python.org/moin/TimeComplexity)
- [Anthropic: Building effective agents](https://www.anthropic.com/research/building-effective-agents)
- [Anthropic: Introducing Contextual Retrieval](https://anthropic.com/news/contextual-retrieval)
- [pgvector README: indexing, filtering and iterative index scans](https://github.com/pgvector/pgvector)
- [Claude docs: Batch processing with the Message Batches API](https://platform.claude.com/docs/en/build-with-claude/batch-processing)
- [Google SRE book: Monitoring distributed systems (the four golden signals)](https://sre.google/sre-book/monitoring-distributed-systems/)
- [MIT CAPD: Using the STAR method for your next behavioral interview](https://capd.mit.edu/resources/the-star-method-for-behavioral-interviews/)
- [Amazon: Leadership Principles (a well-known example of the behaviours interviewers probe)](https://www.amazon.jobs/content/en/our-workplace/leadership-principles)
- [Palantir blog: A day in the life of a Forward Deployed Software Engineer](https://blog.palantir.com/a-day-in-the-life-of-a-palantir-forward-deployed-software-engineer-45ef2de257b1)
- [Harvard Mignone Center for Career Success: Harvard College Resumes and Cover Letter Guide](https://careerservices.fas.harvard.edu/resources/create-a-strong-resume/)
- [GitHub Docs: Managing your profile README](https://docs.github.com/en/account-and-profile/how-tos/profile-customization/managing-your-profile-readme)

## Further reading

- [Benchmarks: SWE-bench, GAIA, AgentBench](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F19-benchmarks-swebench-gaia)
- [Benchmarks: WebArena and OSWorld](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F20-benchmarks-webarena-osworld)
- [Failure Modes: Why Agents Break](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F26-failure-modes-agentic)

## Check yourself

Answer out loud before opening each answer.

<details><summary>Why is pass 2 interleaved rather than group by group?</summary>

In an interview nobody tells you the pattern. Interleaving makes every problem start with recognising which pattern applies, which is the skill blocked practice never trains.

</details>

<details><summary>The sliding-window solution has a `while` or a jump inside a `for` loop. Why is it still O(n)?</summary>

Each index enters the window once when `right` reaches it and leaves at most once when `left` passes it, so the total pointer movement across the whole run is at most 2n. The cost is counted per element, not per loop.

</details>

<details><summary>Why read the customer's sum insured from the system of record instead of retrieving it?</summary>

It is a structured fact with one correct value, and the policy administration system holds it. Similarity search can return a different customer's schedule or a stale copy; a keyed lookup cannot, and it is cheaper.

</details>

<details><summary>In the insurer estimate, which term dominates the LLM bill, and what are two levers to cut it?</summary>

Input tokens, mostly the retrieved chunks. Rerank and send fewer chunks, and route simple questions to a cheaper model; caching answers to identical general questions per wording version also helps.

</details>

<details><summary>Why does the interviewer ask "what exactly was your part?" so often?</summary>

Because "we" hides who did the work, and they are hiring you. The answer should separate your actions from others' precisely.

</details>

<details><summary>In a STAR answer, which part should take the most time, and why?</summary>

The Action, roughly 60% by the MIT guide's split, because what you did and why is the evidence being scored. Situation and Task only set it up.

</details>

<details><summary>The Get Hired tab ranks resume formatting and keywords as a small lever. Why bother rewriting the resume at all?</summary>

Because it is necessary to avoid disqualification: a garbled parse, a missing term or a vague line can get you skipped. It will not get you selected by itself, so its real job is to send the reader to your proof.

</details>

<details><summary>What is the bullet formula, and why does each part matter?</summary>

Verb, what you built and for whom, the key technical decision, the measured result. Each part answers an interviewer question in advance (what, for whom, how, how do you know), and the result makes it checkable.

</details>

---

**Learn Week 12 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week12). Week 1 is free.
