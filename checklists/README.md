# Checklists FDEs actually use

## Before the engagement starts

- [ ] A named sponsor on the client side who owns the outcome
- [ ] One success metric, written down, that the sponsor agrees to (for example: 30% of tier-1 tickets resolved without a human)
- [ ] Access confirmed: data, systems, test accounts, and who approves each
- [ ] The system of record for each key fact identified
- [ ] Security and data-residency rules known (can data leave the country, the cloud account, the VPC?)
- [ ] A named project counterpart for weekly check-ins

### Warning signs in the first meeting

- "Data will be ready in two weeks." It never is; plan the timeline as if it will not be.
- "We don’t need a project manager on our side." The project will lose direction without a named counterpart.
- "Can we just run this on-prem for now?" Usually signals a deeper trust problem that will block the project later, not a small infrastructure preference.

*Several FDE terms and the warning signs in this repo are adapted from [Awesome-FDE-Roadmap](https://github.com/pierpaolo28/Awesome-FDE-Roadmap) by Pier Paolo Ippolito (MIT License, Copyright (c) 2026 Pier Paolo Ippolito).*

### A typical engagement timeline

| When | What happens |
| --- | --- |
| Week 0 | Qualification: confirming there is a real internal sponsor, real access, and a real, specific success metric before any work starts. |
| Weeks 1 to 2 | Discovery and workflow mapping: understanding how the client actually works today, not how their documentation says they work. |
| Weeks 3 to 6 | Build, integration, and proof of value: the first working version, scoped narrow enough to actually finish. |
| Weeks 7 to 12 | Production deployment, adoption, and an executive readout proving the value actually landed. |
| After | Stabilization and handoff: making sure the system survives you leaving, which is the actual definition of done for this role. |

## Production readiness for an LLM application

### Quality
- [ ] A golden dataset of real questions, with expected answers or rubrics
- [ ] Evals run on every change, in CI, with a pass threshold
- [ ] RAG answers cite their sources; the system says "I don't know" when nothing relevant is found
- [ ] Retrieval measured separately (recall@k) from answer quality

### Safety and security
- [ ] Inputs and retrieved documents treated as untrusted (prompt-injection tests included)
- [ ] Tools have the narrowest permissions possible; destructive actions need explicit confirmation
- [ ] PII redacted before logging and before third-party calls
- [ ] Users can only retrieve documents they are allowed to see

### Operations
- [ ] Every request traced: prompt, tools, outputs, latency, cost
- [ ] Cost per request known, with a budget alert
- [ ] Timeouts, retries with backoff, and a step limit on every agent loop
- [ ] A fallback when the model provider is down or slow
- [ ] Secrets in a secret manager, never in code or prompts

### Handover
- [ ] A runbook: how to deploy, roll back, rotate keys and update the eval set
- [ ] An owner on the client side who has done one deploy themselves
- [ ] An executive summary: what changed, the metric before and after, what's next

---

These checklists come from the enterprise track of [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=checklists), where you write a site survey, a scoping document and an executive report for a client scenario.
