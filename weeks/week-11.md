# Week 11: The portfolio and the niche

**Month 3: Production, deployment, and getting hired** · Go narrow, it is where the money actually is · 4 lessons · about 16 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 10](week-10.md) · [Week 12 →](week-12.md)

## What you will be able to do

- Pick one industry you have some real access to. Dense options nearby include pharma, healthcare, and logistics back-office work
- Build your third and most polished system solving one specific, named, expensive workflow in that industry
- Run it against messy, realistic data, not a clean sample, and write down everything that broke
- Write up all three projects as short case studies: the problem, the approach, what broke, and the one number that proves it worked

## You ship this week

> A three-project portfolio, each with a case-study write-up, live on GitHub or this same site. This is what you send instead of a generic resume.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. Choosing a niche and finding a workflow worth automating

*About 3.5 hours*

By now you can build a RAG tool, an agent loop, a multi-agent system with evals, tracing and a public URL. So can thousands of other graduates, and their portfolios look like yours: "chat with your PDFs", "a research agent", "a customer support bot". A hiring manager at an FDE team, or a client's operations head, cannot tell them apart. What they can tell apart is a person who says "hospital insurance desks in Hyderabad lose most of their time to TPA query loops, here is why, and here is a system that cuts that loop". Going narrow is not a marketing trick. It is how you learn the vocabulary, the data and the failure modes that make a system actually useful, and it is the only way your third project can solve a problem someone would pay to have solved.

Covers: The mental model: a niche is an industry, a role and a workflow; Four filters for choosing; Finding the workflow through conversations; The workflow card.

### 2. Your third system: scope, cost and polish for one expensive workflow

*About 5 hours*

Your first two projects proved you can build: a document Q&A tool, and a multi-agent system with evals, tracing, guardrails and a public URL. The third has a different job. It must show that you can take one named, expensive workflow in one industry and ship something a practitioner there would recognise as useful, at a cost that makes sense, in a form a stranger can run and trust. That is the FDE job in miniature, and it is the project interviewers will spend the most time on. Projects at this stage usually fail in one of two ways: the scope is a theme ("AI for logistics") rather than a workflow, so nothing can be measured, or the system works in a demo but has no README, no tests, no evals and no answer to "what does it cost and what does it save?"

Covers: The mental model: polished means a stranger can trust it in ten minutes; Scope it on one page; Estimating what the workflow costs today.

### 3. Messy data, and writing down everything that broke

*About 4 hours*

Every system you have built so far has mostly been run on data you chose: a clean PDF, a tidy sample, test cases you wrote while you knew how the code worked. Client data is not like that. Indian business documents arrive as phone photos with stamps over the text, dates in three conventions, amounts written as "Rs. 1,25,000/-" or "1.25 lakh", remarks in Hindi, Hinglish and English, and the same document sent twice. A system that has never met that mess will fail on the first day of a pilot, in front of the client, often silently. This lesson makes the failures happen on your laptop instead: you generate realistic mess on purpose, run your system against it, write down everything that broke, and turn each failure into a test it must pass forever. The failure log you produce is also the most convincing evidence in your portfolio.

Covers: The mental model: clean data tests your code, messy data tests your system; Clean sample; Messy data; Where realistic messy data comes from; A taxonomy of Indian document mess; A messy-data generator that keeps the truth.

### 4. Case studies that prove it worked, and your Week 11 portfolio

*About 4 hours*

A repository proves you wrote code. A case study proves you solved a problem, and it is what you will send instead of a generic resume. The people who read it, an FDE hiring manager, a founder, a client's operations head, have about ninety seconds before deciding whether to read on, and they are looking for four things: did you understand a real problem, did you make sensible engineering choices, are you honest about what went wrong, and is there evidence it worked. Most portfolio write-ups fail on the last two: they list features, hide failures, and quote numbers like "98% accuracy" with no denominator, baseline or test set. An honest case study with a modest, well-measured number beats an impressive one that collapses at the first interview question. In a role where clients rely on what you tell them, the honesty is itself the qualification.

Covers: The mental model: a case study is an engineering argument; The structure; A full worked example.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [The Digital Personal Data Protection Act, 2023 (India Code)](https://www.indiacode.nic.in/bitstream/123456789/22037/2/a2023-22.pdf)
- [PIB: Digital Personal Data Protection Rules, 2025 explained (November 2025)](https://static.pib.gov.in/WriteReadData/specificdocs/documents/2025/nov/doc20251117695301.pdf)
- [NRCES: NHCX profiles in the FHIR Implementation Guide for ABDM](https://nrces.in/ndhm/fhir/r4/hcx-profile.html)
- [CDSCO: Central Drugs Standard Control Organisation, About us](https://cdsco.gov.in/opencms/opencms/en/About-us)
- [Anthropic: Building effective agents (workflows versus agents)](https://www.anthropic.com/research/building-effective-agents)
- [Python docs: decimal, decimal fixed point and floating point arithmetic](https://docs.python.org/3/library/decimal.html)
- [GitHub Docs: About the repository README file](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes)
- [Synthea: synthetic patient population simulator (GitHub, Apache 2.0)](https://github.com/synthetichealth/synthea)
- [openFDA: data licensing (CC0 dedication and exceptions)](https://open.fda.gov/license/)
- [Faker on PyPI (third-party; locales include en_IN and hi_IN)](https://pypi.org/project/Faker/)
- [Python docs: unicodedata, the Unicode database](https://docs.python.org/3/library/unicodedata.html)
- [Python docs: re, regular expression operations (what \d matches)](https://docs.python.org/3/library/re.html)
- [GitHub Docs: Managing your profile README](https://docs.github.com/en/account-and-profile/how-tos/profile-customization/managing-your-profile-readme)
- [GitHub Docs: What is GitHub Pages?](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages)
- [NIST/SEMATECH e-Handbook: Confidence limits for a proportion (Wilson method)](https://www.itl.nist.gov/div898/handbook/prc/section2/prc241.htm)

## Further reading

- [Define the Outcome Before You Choose the Output](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F47-outcomes-before-output)
- [Discover the Workflow People Actually Perform](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F48-discover-the-real-workflow)
- [Choose the Smallest Slice That Can Change the Decision](https://aiengineeringfromscratch.com/lesson?path=phases%2F14-agent-engineering%2F50-choose-the-smallest-testable-slice)

## Check yourself

Answer out loud before opening each answer.

<details><summary>Why are access and cost treated as gates rather than weighted scores?</summary>

Because a high score elsewhere cannot compensate for them. Without access you cannot learn the workflow or validate the system, and without a real cost nobody will pay for or adopt the solution.

</details>

<details><summary>A practitioner says your idea "sounds very useful". What should you do with that?</summary>

Treat it as politeness, not evidence. Ask instead about the last time the problem occurred, how long it took, what went wrong and what it cost.

</details>

<details><summary>Why does the scope need guardrail metrics as well as a primary metric?</summary>

A primary metric on its own can be improved by breaking something else, such as auto-clearing more documents by not checking shortages. Guardrails, like zero silent money errors, make that trade visible and unacceptable.

</details>

<details><summary>In the example ROI model, why did the sensitivity analysis matter more than the base-case saving?</summary>

It showed that error rates and error cost dominate the value, so the system must be designed and measured around catching errors, and that the all-pessimistic case loses money, which must be disclosed.

</details>

<details><summary>Why must the ground truth travel with each generated messy document?</summary>

Because it lets you detect every failure automatically, including silent wrong values that look plausible. Without it you can only find crashes, or eyeball outputs.

</details>

<details><summary>A transporter's system exports 12 August as 08/12/2026, and your DMY parser accepts it without error. Why is this worse than a crash?</summary>

It produces a valid but wrong date, 8 December instead of 12 August, which flows downstream into late-delivery penalties without any signal. A crash would have ended in a known failed state.

</details>

<details><summary>Why does the "what broke" section make the result more credible rather than less?</summary>

It shows the system was tested against realistic data and that you know its limits, and failures turned into eval cases show the number was measured after they were fixed. A case study with no failures reads as untested.

</details>

<details><summary>Your system had 0 silent errors on 40 real documents. What may you claim?</summary>

That none occurred on those 40, which only bounds the true rate below roughly 9% at 95% confidence. You may not claim it never makes silent errors.

</details>

---

**Learn Week 11 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week11). Week 1 is free.
