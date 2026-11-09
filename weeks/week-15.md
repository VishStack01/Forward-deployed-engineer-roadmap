# Week 15: The consulting mindset

**Month 4: The Enterprise and Consulting Track (Optional Stretch)** · Solve the people problem so the technical solution can work · 4 lessons · about 10 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 14](week-14.md) · [Week 16 →](week-16.md)

> Weeks 13 to 16 are the optional enterprise track, for Palantir-scale FDE roles: messy client data, cloud at client scale, and the consulting side of the job.

## What you will be able to do

- MECE thinking: break a vague mandate like "make us more efficient with AI" into non-overlapping, individually solvable technical tasks
- The Pyramid Principle: lead with the answer, then the supporting detail. Executives want the conclusion before the method
- The Three Whys: "What is the actual system of record?" "What is the cost of doing nothing?" "Who owns this once you leave?"
- Run a real discovery conversation with a friend or mentor roleplaying a skeptical client stakeholder, and practice translating a vague ask into a scoped technical requirement

## You ship this week

> A one-page Technical Scoping Document for a real or hypothetical client request, written so a non-technical executive would accept it on first read.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. MECE decomposition, from "make us more efficient with AI" to tasks you can actually build

*About 2.5 hours*

The first sentence a client says is almost never a requirement. "Make us more efficient with AI", "use GenAI on our documents", "fix customer support" are mandates: real worries, phrased so loosely that any project could claim to answer them, and so no project can be said to have succeeded. An FDE who starts building from a mandate ends up with a demo nobody asked for. The skill this lesson teaches is decomposition: breaking a vague mandate into pieces that do not overlap and together cover the whole problem, until each piece is small enough to have one owner, one data source and one number that tells you it worked. Consultants call this MECE. Engineers already do a version of it when they split a system into modules. Doing it on a business problem, out loud, in front of a client, is what makes the rest of Month 4 possible.

Covers: The mental model: a tree whose siblings never collide and never leave holes; Mutually exclusive; Collectively exhaustive; How to choose the cut; A worked example: a general insurer in Pune; Check MECE against real items, not against your intuition.

### 2. The Pyramid Principle, answer first, so an executive can stop reading at any line

*About 2 hours*

Engineers explain in the order they worked: we looked at the data, we found a problem, we tried three things, and here is what we recommend. Executives read in the opposite order, and most of them stop after a few lines. If your recommendation is in paragraph four, a Chief Operating Officer forwards the email with "can someone summarise this?" and the decision slips a week. On an FDE engagement your writing is how the client's leadership sees your work: the scoping document, the weekly status report, the escalation when the data is late. This lesson teaches the structure consultants use to make that writing land, the Pyramid Principle, so the reader gets the answer first and the support only as far down as they choose to go.

Covers: Where it comes from; The mental model: the reader builds a tree, so hand them the tree top-down; Vertical logic: every line raises a question the next level answers; Horizontal logic: group, do not chain; The introduction: Situation, Complication, Question; Before and after: the same email, twice; Checking a pyramid mechanically; Saying it out loud.

### 3. The Three Whys, system of record, cost of doing nothing, and who owns it after you leave

*About 2 hours*

Most failed AI projects inside companies do not fail on the model. They fail because the team built on a copy of the data instead of the real source, because nobody could say why the project was worth doing this quarter rather than next year, or because the engineer who built it left and nobody on the client side knew how to keep it alive. The course's Three Whys are three questions that expose exactly those failure points before you write any code: What is the actual system of record? What is the cost of doing nothing? Who owns this once you leave? Each one sounds simple. Each one, asked properly and followed up, usually changes the scope. This lesson teaches what each question is really testing, how to ask it without sounding like an auditor, what weak answers sound like, and what you do with the answer.

Covers: The mental model: three questions about the start, the reason and the end; Why 1: "What is the actual system of record?"; Why 2: "What is the cost of doing nothing?".

### 4. Running a discovery conversation and turning a vague ask into a one-page scope

*About 4 hours*

Discovery is the part of FDE work that no tutorial shows you and every engagement depends on. A client stakeholder gives you twenty minutes, a vague ask and, often, a sceptical look, because two previous vendors promised AI and delivered a slide deck. In that conversation you have to learn how the work really happens, where the data lives, what success would mean in numbers, and who will fight you, without pitching and without sounding like a questionnaire. Then you have to write it down as a scope a non-technical executive will sign on first read. This lesson gives you a structure for the conversation, a question bank, a roleplay script you can run with a friend or mentor, a method for translating the ask into a requirement, and a plan for this week's deliverable: a one-page Technical Scoping Document.

Covers: The mental model: you are there to learn how work actually happens; How people describe it; What you ask for; The shape of a 45-minute discovery meeting; A question bank; The roleplay: practising with a sceptical stakeholder; Watch for the red flags; From vague ask to scoped requirement.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [Wikipedia: MECE principle (origin and criticisms)](https://en.wikipedia.org/wiki/MECE_principle)
- [Wikipedia: Barbara Minto](https://en.wikipedia.org/wiki/Barbara_Minto)
- [McKinsey Alumni: Barbara Minto on MECE (where the idea came from, and how she pronounces it)](https://www.mckinsey.com/alumni/news-and-insights/global-news/alumni-news/barbara-minto-mece-i-invented-it-so-i-get-to-say-how-to-pronounce-it)
- [Python docs: itertools (useful for pairwise overlap checks between branches)](https://docs.python.org/3/library/itertools.html)
- [Barbara Minto: The Minto Pyramid Principle, the concept (Minto's own summary of the method)](https://barbaraminto.com/concept)
- [Wikipedia: Five whys (origin at Toyota and criticisms)](https://en.wikipedia.org/wiki/Five_whys)
- [Atlassian: RACI chart, what it is and how to use it](https://www.atlassian.com/work-management/project-management/raci-chart)
- [Google SRE Workbook: SRE engagement model (handing back operational ownership)](https://sre.google/workbook/engagement-model/)
- [Simon and Schuster: The Mom Test by Rob Fitzpatrick (how to ask questions people cannot lie about)](https://www.simonandschuster.co.uk/books/The-Mom-Test/Rob-Fitzpatrick/9798893312577)

## Check yourself

Answer out loud before opening each answer.

<details><summary>Why is "Intake, Verification, Email automation, Settlement" not a MECE set of branches?</summary>

It mixes two dimensions. Email is a channel that runs through every stage, so an email claim belongs to both "Intake" and "Email automation", and anything that is neither a named stage nor email falls through.

</details>

<details><summary>What makes a formula cut MECE by construction?</summary>

The terms of an equation partition the quantity. Every hour or rupee is counted in exactly one term, and the terms add up to the total, so there is no overlap and no gap as long as the equation is correct.

</details>

<details><summary>What question should the key points directly under a governing thought answer?</summary>

The question the governing thought raises in the reader's mind, usually "why?" or "how?". If a key point does not answer that question, it belongs somewhere else or nowhere.

</details>

<details><summary>Why prefer an inductive group of reasons over a deductive chain at the top of an executive email?</summary>

Independent reasons survive one of them being challenged; a chain collapses if any single link is rejected, and it forces the reader to hold every step in mind before reaching the point.

</details>

<details><summary>Why ask "which screen settles a dispute?" instead of "what is your system of record?"</summary>

The abstract question gets the official answer. A concrete dispute reveals which source people actually trust when sources disagree, which may be a different system or a spreadsheet.

</details>

<details><summary>A client sends you a clean Excel export to start building on. What do you do with it?</summary>

Use it for profiling and to understand fields, but record it as a copy, find out where it comes from and how stale it is, and make access to the real source (or a replica) an explicit early milestone.

</details>

<details><summary>Why ask "walk me through the last case that went badly" rather than "what are your main problems?"</summary>

A specific past case produces facts about how the work really flows, including workarounds and waits, while a general question produces the official story and opinions.

</details>

<details><summary>What three things should qualification confirm before discovery begins?</summary>

A real internal sponsor, real access to the people and data, and a real, specific success metric.

</details>

---

**Learn Week 15 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week15). Week 1 is free.
