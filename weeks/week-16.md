# Week 16: Case interview practice

**Month 4: The Enterprise and Consulting Track (Optional Stretch)** · Enterprise FDE interviews test judgment, not just code · 4 lessons · about 13 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 15](week-15.md)

> Weeks 13 to 16 are the optional enterprise track, for Palantir-scale FDE roles: messy client data, cloud at client scale, and the consulting side of the job.

## What you will be able to do

- Learn the C.A.S.E. framework: Clarify, Architect, Solve (the Delta), Evaluate
- Work through the Hospital Readmission case study in the Interview Playbook tab, then redo it cold without looking
- Practice the high-frequency enterprise FDE questions in the same tab out loud, timing yourself to under 3 minutes per answer
- Write your own Site Survey and Executive Status Report using the templates in the Interview Playbook, based on a real or invented client scenario

## You ship this week

> A completed Site Survey, Technical Scoping Document, and Executive Status Report for one invented client scenario, all three ready to reference in an interview.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. The C.A.S.E. framework, Clarify, Architect, Solve the Delta, Evaluate

*About 2 hours*

Enterprise FDE interviews often replace the coding puzzle with a case: a messy client situation and the question "what would you do?" There is no single right answer, so the interviewer scores how you reason: whether you find the constraints before you design, whether your design names real systems and trade-offs, whether you know where an off-the-shelf product stops and custom work begins, and whether you can prove the thing works. Candidates who free-associate ("we could use a vector database, and maybe Kafka") read as guessing. The Interview Playbook gives you a four-part structure for exactly this round, C.A.S.E., and tells you not to propose anything until you have clarified the constraints. This lesson takes each stage apart, shows how it fits with the Signature Framework you rehearsed for the Week 12 mock interviews, and runs it on a fresh case so that next lesson's hospital case has a pattern to follow.

Covers: The four stages, as the app defines them; The mental model: one arc for the whole case, one pattern for each decision; Clarify: questions that change the design; Architect: the data flow with real names; Solve the Delta: where the product ends and your glue begins; Evaluate: proof, and the alarm for silent failure; Turning Clarify answers into design decisions; A fresh case, run through C.A.S.E. in miniature.

### 2. The hospital readmission case, worked in full, then redone cold

*About 4 hours*

The hospital readmission case in the Interview Playbook is a compact version of almost every hard enterprise engagement: a legacy on-premises database, decades of messy data, strict privacy law, a nervous IT team, clinicians who will ignore a tool they do not trust, and a goal ("predict readmission") that sounds precise and is not. If you can walk through it fluently, with real decisions and honest trade-offs, you can handle most variants an interviewer will throw at you. This lesson works the case at full depth using C.A.S.E. It follows the app's four 30-day phases, adds the questions and details a strong interviewer will probe, points out two places where the app's short version needs care, and ends with a protocol for redoing the case cold until you can deliver it without notes.

Covers: The scenario; Clarify: what "readmission" means is the first design decision; Days 1 to 7: discovery and trust; Days 8 to 15: a secure landing zone; Days 16 to 25: the pipeline; Days 26 to 30: value validation.

### 3. Answering enterprise FDE questions out loud in under three minutes

*About 3 hours*

Enterprise FDE interviews are full of short scenario questions: a petabyte that must move in two days, an engineer who will not give you access, a bank that wants an LLM inside a 100-millisecond decision. Each one is a small case, and you get a few minutes, not forty-five. Candidates fail these in two opposite ways: they ramble for six minutes and never land the answer, or they give a one-line answer that shows no reasoning. Three minutes is enough time to give the answer, three reasons, the main risk and how you would check, and not enough time to wander. This lesson gives you a fixed structure for a three-minute spoken answer, works the three high-frequency questions from the Interview Playbook, adds the arithmetic and current product facts that make them convincing, and sets up timing drills so the structure becomes automatic.

Covers: The mental model: a three-minute answer is a pyramid with a clock on it; Question 1: five petabytes to the cloud in 48 hours.

### 4. Writing a Site Survey and an Executive Status Report, and the three-document deliverable

*About 4 hours*

The Interview Playbook says it plainly: in enterprise FDE work, your documentation is your contract. Three documents carry an engagement. The Site Survey, written in week one before any code, records what the client's environment actually is. The Technical Scoping Document, which you wrote last week, fences what you will build. The Executive Status Report, sent every week, shows the value landing and the risks with owners, and the app says it is the document that actually justifies contract renewal, not the code itself. Most engineering graduates have never written any of them. Interviewers for enterprise roles ask about them because being able to describe and show them signals you understand the job past the code. This lesson teaches both remaining templates, works fragments of each for an invented client, and plans this week's deliverable: all three documents for one invented scenario, ready to reference in an interview.

Covers: The mental model: three documents, three questions, three moments; The Site Survey; The Executive Status Report; Checking the mechanics before sending; Planning this week's deliverable.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [Microsoft Learn: About change data capture (SQL Server)](https://learn.microsoft.com/en-us/sql/relational-databases/track-changes/about-change-data-capture-sql-server)
- [HHS: Guidance on de-identification of protected health information (Safe Harbor and Expert Determination)](https://www.hhs.gov/hipaa/for-professionals/special-topics/de-identification)
- [CMS: Hospital Readmissions Reduction Program (30-day unplanned readmission measures and covered conditions)](https://www.cms.gov/medicare/payment/prospective-payment-systems/acute-inpatient-pps/hospital-readmissions-reduction-program-hrrp)
- [van Walraven et al., CMAJ 2010: derivation and validation of the LACE index for early death or unplanned readmission](https://cmaj.ca/content/182/6/551)
- [scikit-learn: CalibratedClassifierCV and probability calibration](https://scikit-learn.org/stable/modules/generated/sklearn.calibration.CalibratedClassifierCV.html)
- [AWS Snowball Edge Developer Guide: notice that Snowball Edge is no longer available to new customers, with alternatives](https://docs.aws.amazon.com/snowball/latest/developer-guide/s3compatible-on-snow.html)
- [Google Cloud: Transfer Appliance overview (timings for offline transfer)](https://docs.cloud.google.com/transfer-appliance/docs/4.0/overview)
- [PEP 418: monotonic time and performance counter functions in Python](https://peps.python.org/pep-0418/)
- [Atlassian: RACI chart (one accountable owner per task)](https://www.atlassian.com/work-management/project-management/raci-chart)
- [Barbara Minto: The Minto Pyramid Principle (structure the report answer-first)](https://barbaraminto.com/concept)

## Check yourself

Answer out loud before opening each answer.

<details><summary>How does C.A.S.E. relate to the Signature Framework (Constraint, Tradeoff, Failure mode, Verification)?</summary>

C.A.S.E. is the arc of the whole case; the Signature Framework is how you justify each individual design decision inside it, especially during Architect and Solve.

</details>

<details><summary>The interviewer answers your clarifying question with "you decide." What do you do?</summary>

State an explicit assumption, say which part of the design would change if it were wrong, and continue. That shows you know which assumptions matter without stalling.

</details>

<details><summary>Why does the care team's capacity matter more than a probability threshold?</summary>

The team can follow up only a fixed number of patients per day, so the useful question is how many true readmissions are in that top group. Precision at capacity measures exactly that.

</details>

<details><summary>Why can you not build the readmission label after Safe Harbor de-identification?</summary>

Safe Harbor allows only the year of dates, and a 30-day readmission label needs exact intervals between discharge and readmission. Compute those intervals inside the PHI boundary before tokenising.

</details>

<details><summary>What sustained bandwidth would moving 5 PB in 48 hours require, and what does that tell you?</summary>

About 230 Gbps, before overhead. Almost no client has that, so the plan must change: move a needed subset now and the bulk later, or bring compute to the data.

</details>

<details><summary>Why is "request a transfer appliance" alone a weak answer to the 48-hour question today?</summary>

Physical transfer typically takes weeks end to end, not two days, and specific devices have been withdrawn for new customers. The answer needs a plan for what the exercise uses within 48 hours.

</details>

<details><summary>What is the job of the "quick win for week two" in a Site Survey?</summary>

To deliver a small, visible, useful result early that also proves your access and pipeline work, buying trust and patience for the longer build.

</details>

<details><summary>What separates a value line from an activity line in a status report?</summary>

A value line reports a change in a number the client cares about, against a baseline, such as a success criterion. An activity line reports work done, which executives cannot judge.

</details>

---

**Learn Week 16 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week16). Week 1 is free.
