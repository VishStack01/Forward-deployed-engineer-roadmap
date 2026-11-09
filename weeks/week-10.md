# Week 10: Real deployment

**Month 3: Production, deployment, and getting hired** · Off localhost, onto the internet · 4 lessons · about 12 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 9](week-09.md) · [Week 11 →](week-11.md)

## What you will be able to do

- Containerize the system with Docker
- Deploy to a real host: Render, Fly.io, or a cloud free tier, not your laptop
- Environment variables and secrets management done properly, nothing hardcoded
- A basic auth layer for any agent action that touches a real system

## You ship this week

> Your multi-agent system running live at a public URL you can hand to someone else to try, with the codebase and a short architecture write-up on GitHub.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. Containers from first principles, then a production Dockerfile for your agent service

*About 3 hours*

Until now your multi-agent system has run inside your own virtual environment, on your own Python, with your own `.env` file sitting next to the code. None of that exists on a server. A container image packages the exact Python, the exact pinned dependencies and your code into one artifact that runs the same way on your laptop, in CI, on Render, and on the client's Kubernetes cluster. It is also the first thing a client's security team will inspect: they will scan the image, ask what user it runs as, and check whether a key is hiding in one of its layers. A careless Dockerfile turns a working agent into a 1.5 GB image that runs as root with your Anthropic key readable by anyone who pulls it. This lesson teaches you to build the careful one, and to explain every line of it.

Covers: The mental model: an image is a recipe's output, a container is a running process; Image; Container; Layers and the build cache.

### 2. Off localhost - deploying the agent service to Render, with Fly.io as the alternative

*About 3.5 hours*

"It works on my laptop" is not a deliverable. A client, an interviewer or a teammate needs a URL they can open from their own network, at a time that suits them, without you sitting next to the server. Getting there means understanding what sits between their browser and your container: DNS, a load balancer that terminates TLS, a port your process must bind to, health checks that decide whether your new version gets traffic, environment variables injected at start-up, logs you can search after something breaks, and a way to undo a bad release in a minute. A platform-as-a-service handles most of that for you, which is exactly why you must know what it is doing: when the deploy hangs at "waiting for health check", or the first request after lunch takes a minute, the platform will not explain itself. This lesson takes the image from the last lesson to a public HTTPS URL.

Covers: The mental model: a PaaS runs your container and owns everything around it; What happens to one request; Health checks: liveness and readiness.

### 3. Configuration and secrets - nothing hardcoded, nothing leaked, and the first hour after a leak

*About 3 hours*

Your deployed agent holds keys that cost money and keys that open doors: the model provider key (anyone who has it can run up your bill), the database password (anyone who has it can read every customer conversation), tracing keys, and the pepper that protects your users' API keys. In a client engagement you will add their CRM token and perhaps a payments key. Every one of these will, at some point, be one careless commit, one debug log line or one Docker layer away from public. Automated scanners watch public code hosts continuously, so treat a key pushed to a public repository as compromised the moment it lands. The engineering answer has three parts: configuration that comes from the environment and is validated before the app serves a single request, secrets that live only in places built to hold them, and a rehearsed plan for the hour after something leaks anyway.

Covers: The mental model: code is the same everywhere, configuration is what differs; Code; Configuration; Secrets; Where each value comes from; Load once, validate everything, fail at startup.

### 4. Auth for agent actions - who is asking, what they may do, and the Week 10 deliverable

*About 3.5 hours*

The moment your agent is at a public URL, anyone who finds the URL can talk to it, and anything the agent can do, they can make it do. Week 9 put gates in front of risky actions; those gates are only meaningful if the system knows who is asking and what that person is allowed to do. Without authentication, "requires a support lead's approval" means "requires anyone to type support lead". Without authorization at the tool boundary, a junior user can ask the agent to issue a refund that they could never issue themselves, because the agent's own credential can. Client security teams probe exactly this: can the agent be used to do something the user cannot? This lesson builds the answer: API keys done properly, a per-action permission check enforced in code with the end user's identity, and an audit trail that can show who did what through the agent. Then it helps you plan the Week 10 deliverable.

Covers: The mental model: two different questions; API keys, sessions and OAuth, at a practical level; Hashing secrets you store.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [Docker docs: Building best practices](https://docs.docker.com/build/building/best-practices/)
- [Docker docs: Multi-stage builds](https://docs.docker.com/build/building/multi-stage/)
- [Docker docs: Build secrets](https://docs.docker.com/build/building/secrets/)
- [Docker docs: Control startup order in Compose](https://docs.docker.com/compose/how-tos/startup-order/)
- [FastAPI docs: FastAPI in Containers - Docker](https://fastapi.tiangolo.com/deployment/docker/)
- [Render docs: Deploy for Free](https://render.com/docs/free)
- [Render docs: Deploying on Render](https://render.com/docs/deploys)
- [Render docs: Health Checks](https://render.com/docs/health-checks)
- [Render docs: Rollbacks](https://render.com/docs/rollbacks)
- [Fly.io docs: Rollback guide](https://docs.fly.io/blueprints/rollback-guide/)
- [The Twelve-Factor App: III. Config](https://12factor.net/config)
- [Pydantic docs: Settings management (pydantic-settings)](https://pydantic.dev/docs/validation/latest/concepts/pydantic_settings/)
- [GitHub docs: About secret scanning](https://docs.github.com/en/code-security/concepts/secret-security/about-secret-scanning)
- [GitHub docs: Removing sensitive data from a repository](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)
- [OWASP Secrets Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html)
- [OWASP Top 10 for LLM Applications: LLM06 Excessive Agency](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/)
- [OWASP Authorization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html)
- [OWASP Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)
- [Python docs: hmac, keyed hashing for message authentication](https://docs.python.org/3/library/hmac.html)
- [RFC 8693: OAuth 2.0 Token Exchange](https://datatracker.ietf.org/doc/html/rfc8693)

## Further reading

- [Building a Production LLM Application](https://aiengineeringfromscratch.com/lesson?path=phases%2F11-llm-engineering%2F13-production-app)
- [Managed LLM Platforms: Bedrock, Vertex, Azure](https://aiengineeringfromscratch.com/lesson?path=phases%2F17-infrastructure-and-production%2F01-managed-llm-platforms)
- [Security: Secrets, API Key Rotation, Audit Logs](https://aiengineeringfromscratch.com/lesson?path=phases%2F17-infrastructure-and-production%2F25-security-secrets-audit)

## Check yourself

Answer out loud before opening each answer.

<details><summary>You add `RUN rm /srv/.env` right after `COPY .env /srv/.env`. Is the secret gone from the image?</summary>

No. The `COPY` created a layer containing the file, and the `rm` only adds a later layer that hides it. Anyone with the image can extract the earlier layer, so the secret must be treated as leaked and rotated.

</details>

<details><summary>Why does `depends_on: [db]` alone not stop your API crashing on startup with "connection refused"?</summary>

Without a condition, `depends_on` only controls start order; Postgres may still be initialising when the API starts. `condition: service_healthy` with a `pg_isready` healthcheck makes Compose wait until the database accepts connections.

</details>

<details><summary>Your container logs `Uvicorn running on http://127.0.0.1:8000` and the Render deploy never goes live. Why?</summary>

The process listens only on the container's loopback interface, so the platform's load balancer, which connects from outside the container, cannot reach it and the health check fails. Bind `0.0.0.0` and listen on the `PORT` the platform provides.

</details>

<details><summary>Why is pointing Render's health check at an endpoint that calls the model provider a bad idea?</summary>

The health check runs constantly and decides restarts and deploys. A slow or failing provider would mark healthy instances as unhealthy, triggering restarts and cancelled deploys, and every check would cost money.

</details>

<details><summary>Why should a secret never have a default value in your settings class?</summary>

A default lets the app start without the real secret, so a misconfigured deploy looks healthy and fails only when a user hits the code path that needs it. With no default, validation fails at startup and the platform keeps the previous version serving.

</details>

<details><summary>Environment variables are the standard way to pass secrets to containers. What are their weaknesses, and how do you limit them?</summary>

Every process in the container can read them, child processes inherit them, and they can surface in crash dumps, debug pages and error trackers. Limit the damage by never logging the environment, scrubbing error reports, not passing the environment to subprocesses or agent tools, and using a secret manager or secret files when the client requires stronger controls.

</details>

<details><summary>A request arrives with a valid API key that lacks the `refunds:issue` scope and asks to issue a refund. Which status code do you return, and why not the other one?</summary>

403 Forbidden: the caller is authenticated, but this identity is not permitted to perform the action. 401 means the server does not know who the caller is, such as a missing or invalid key.

</details>

<details><summary>Why can API keys you generate be stored with a fast HMAC, while passwords need Argon2id or scrypt?</summary>

A generated key has 256 bits of randomness, so even a fast hash cannot be brute-forced; passwords are low-entropy human choices, so the hash must be slow and memory-hard to make guessing expensive. The pepper adds protection if only the database leaks.

</details>

---

**Learn Week 10 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week10). Week 1 is free.
