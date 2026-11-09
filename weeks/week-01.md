# Week 1: Python and the engineering floor

**Month 1: Foundations, engineer before agent** · Backend basics, not notebooks · 5 lessons · about 14 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 2 →](week-02.md)

## What you will be able to do

- Functions, classes, type hints, exceptions, virtual environments, and basic packaging
- Git and GitHub properly: branches, pull requests, resolving a real merge conflict
- Command line fluency: bash, piping, grep, curl, reading a stack trace without panicking
- Build a small REST API (FastAPI or Flask) with at least three endpoints
- SQL basics: SELECT, JOIN, GROUP BY, against a real Postgres or SQLite database

## You ship this week

> A small FastAPI CRUD service (a notes or task API works fine) backed by a real database, tested, pushed to GitHub with a README that explains how to run it.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. [Python as backend code, not notebook code](https://zero-to-fde-90-days.site/free-week-1/python-engineering-floor?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=w01-l1) (free to read)

*About 2.5 hours*

Every agent you will build in this course is, underneath, an ordinary Python program: it reads input, calls functions, talks to a database and an API, and has to fail in a controlled way when something goes wrong. A notebook teaches you to run cells top to bottom and eyeball the output. A client's production system needs code that someone else can import, test, and trust at 3 a.m. This lesson moves you from the first habit to the second. Most "agent bugs" you will meet in real deployments are plain Python bugs: an exception swallowed silently, a function that returns `None` on one path, a dependency version that differs between your laptop and the server.

Covers: The mental model: code is read far more than it is run; Notebook habit; Backend habit; Functions: one job, explicit inputs, explicit outputs.

### 2. [Git and GitHub as a team sport: snapshots, branches, pull requests and merge conflicts](https://zero-to-fde-90-days.site/free-week-1/git-github-workflow?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=w01-l2) (free to read)

*About 2.5 hours*

On a client engagement nobody emails code around. Every change you make goes through Git, lands on a branch, and reaches the shared codebase through a pull request that a client engineer reviews. If you cannot branch cleanly, write a commit message that explains itself, resolve a conflict without losing a teammate's work, or undo a mistake calmly, you slow down the whole team and lose their trust in your first week. Worse, one careless `git add .` can push an API key to a repository the whole company can read. Git feels like a list of magic commands until you learn the model underneath: snapshots and pointers. Once you see that model, every command in this lesson becomes predictable, including the scary ones.

Covers: The mental model: commits are snapshots, branches are pointers.

### 3. [The command line as a power tool: streams, pipes, curl and calm stack-trace reading](https://zero-to-fde-90-days.site/free-week-1/command-line-fluency?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=w01-l3) (free to read)

*About 2.5 hours*

The servers your agents will run on have no desktop, no IDE and no mouse. When a client says "the bot stopped answering at 2 p.m.", you will be in an SSH session on their machine with a 400 MB log file, a service that will not start and a traceback scrolling past. The engineers who fix that in ten minutes are not smarter; they can search a log with `grep`, count failures with a pipe, hit the API directly with `curl` to see the real status code, check which environment variables the process actually has, and read a stack trace from the bottom up instead of panicking at its length. This lesson gives you those moves, and the model behind them, so you can debug systems you did not write.

Covers: The mental model: small programs, text streams, exit codes.

### 4. [HTTP from first principles, then a tested FastAPI CRUD service](https://zero-to-fde-90-days.site/free-week-1/rest-api-fastapi?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=w01-l4) (free to read)

*About 3 hours*

Almost everything an FDE builds is reached over HTTP. The agent you deploy is called by the client's web app through an API; the agent itself calls a model provider's API, the client's CRM API and a payments API. When those calls fail, the status code, the headers and the exact JSON body are the evidence. If you cannot design a clean endpoint, choose the right status code, validate input before it touches the database, and prove it all works with tests, your integration becomes the thing everyone else has to work around. This lesson teaches HTTP properly first, then builds a small but production-shaped FastAPI service that you will reuse as the skeleton for your Week 1 deliverable and for every agent API later in the course.

Covers: The mental model: an API is a contract written in HTTP; Methods, safety and idempotency; Status codes that matter; Designing resources; FastAPI, Pydantic, uvicorn and ASGI; The complete service.

### 5. [SQL from the relational model up: keys, joins, grouping, NULLs and indexes](https://zero-to-fde-90-days.site/free-week-1/sql-basics?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=w01-l5) (free to read)

*About 3.5 hours*

Nearly every client system you will touch keeps its truth in a relational database: orders, customers, tickets, invoices, permissions. When an agent answers "which customers in Pune have unpaid orders?", some SQL ran somewhere, written by you, by an ORM, or by a model. If you cannot read that SQL and say whether it is right, you cannot vouch for the answer. The failures are quiet: a LEFT JOIN that silently became an INNER JOIN, a `NOT IN` that returns nothing because of one NULL, a revenue total doubled by a join, a query that takes nine seconds because nobody added an index, and one string-formatted query that leaks every customer's data. This lesson teaches SQL properly, against a real SQLite database you can run from Python, and finishes by planning your Week 1 deliverable.

Covers: The mental model: tables are sets of facts, SQL describes the answer; Keys: how rows find each other.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [Python tutorial: Errors and Exceptions](https://docs.python.org/3/tutorial/errors.html)
- [Python docs: dataclasses](https://docs.python.org/3/library/dataclasses.html)
- [Python docs: venv, creating virtual environments](https://docs.python.org/3/library/venv.html)
- [Python Packaging User Guide: Writing your pyproject.toml](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/)
- [mypy: Type hints cheat sheet](https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html)
- [Pro Git: Branches in a Nutshell](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
- [Pro Git: Rebasing (including "The Perils of Rebasing")](https://git-scm.com/book/en/v2/Git-Branching-Rebasing)
- [GitHub Docs: Resolving a merge conflict using the command line](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line)
- [Chris Beams: How to Write a Git Commit Message](https://cbea.ms/git-commit/)
- [GitHub Docs: Removing sensitive data from a repository](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)
- [GNU Bash manual: Redirections](https://www.gnu.org/software/bash/manual/html_node/Redirections.html)
- [jq manual](https://jqlang.org/manual/)
- [curl man page](https://curl.se/docs/manpage.html)
- [Python docs: traceback module](https://docs.python.org/3/library/traceback.html)
- [Microsoft Learn: Install WSL](https://learn.microsoft.com/en-us/windows/wsl/install)
- [FastAPI tutorial: SQL (relational) databases](https://fastapi.tiangolo.com/tutorial/sql-databases/)
- [FastAPI tutorial: Testing](https://fastapi.tiangolo.com/tutorial/testing/)
- [MDN: HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status)
- [MDN: Idempotent (glossary)](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent)
- [ASGI documentation: Introduction](https://asgi.readthedocs.io/en/latest/introduction.html)
- [Python docs: sqlite3, DB-API 2.0 interface for SQLite databases](https://docs.python.org/3/library/sqlite3.html)
- [SQLite: Quirks, Caveats, and Gotchas in SQLite](https://www.sqlite.org/quirks.html)
- [SQLite: EXPLAIN QUERY PLAN](https://www.sqlite.org/eqp.html)
- [PostgreSQL documentation: SELECT](https://www.postgresql.org/docs/current/sql-select.html)
- [OWASP: SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)

## Further reading

- [Dev Environment](https://aiengineeringfromscratch.com/lesson?path=phases%2F00-setup-and-tooling%2F01-dev-environment)
- [Git & Collaboration](https://aiengineeringfromscratch.com/lesson?path=phases%2F00-setup-and-tooling%2F02-git-and-collaboration)
- [APIs & Keys](https://aiengineeringfromscratch.com/lesson?path=phases%2F00-setup-and-tooling%2F04-apis-and-keys)
- [Debugging and Profiling](https://aiengineeringfromscratch.com/lesson?path=phases%2F00-setup-and-tooling%2F12-debugging-and-profiling)

## Check yourself

Answer out loud before opening each answer.

<details><summary>Why is `def f(items=[])` a bug, and what is the fix?</summary>

The default list is created once when the function is defined and shared by every call that does not pass `items`, so state leaks between calls. Default to `None` and create a new list inside the function.

</details>

<details><summary>Does Python stop you from passing a `str` to a parameter hinted as `int`?</summary>

No. Type hints are not enforced at runtime. A static checker such as mypy or pyright reports the mismatch before the code runs, and external input still needs explicit validation.

</details>

<details><summary>What actually happens on disk when you create a new branch, and why is it so cheap?</summary>

Git writes a small file containing the hash of the commit the branch points to. No files are copied; branches are pointers into the existing commit graph.

</details>

<details><summary>In a conflict, Git has already merged some of the lines of the file. How did it decide those were safe?</summary>

It compared each side with the merge base. Where only one side changed a region, it took that change; it only stops where both sides changed the same region differently.

</details>

<details><summary>Why do programs write errors to stderr instead of stdout?</summary>

So diagnostics do not mix into the data. A pipeline or a `> file` redirect only carries stdout, so the output stays clean while errors still reach the person at the terminal.

</details>

<details><summary>`curl https://api.example.com/orders/9` prints an error page, yet `echo $?` shows 0. Why, and how do you make a script notice?</summary>

curl's exit code reflects whether the HTTP exchange happened, not the status code. Use `--fail` (exit code 22 on 4xx/5xx) or check `-w "%{http_code}"`.

</details>

<details><summary>Why is it safe for a client to retry a timed-out DELETE but risky to retry a timed-out POST?</summary>

DELETE is idempotent: repeating it leaves the server in the same state as doing it once. POST is not, so a retry after a lost response can create a second resource; idempotency keys solve that.

</details>

<details><summary>What is the difference between 401, 403 and 422?</summary>

401 means the request is not authenticated (we do not know who you are). 403 means we know who you are and you are not allowed. 422 means the request was well-formed but its content failed validation.

</details>

---

**Learn Week 1 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week01). Week 1 is free.
