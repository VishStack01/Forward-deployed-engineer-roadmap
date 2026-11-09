# Week 3: Retrieval, from first principles

**Month 1: Foundations, engineer before agent** · RAG before you ever say the word RAG · 4 lessons · about 14 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 2](week-02.md) · [Week 4 →](week-04.md)

## What you will be able to do

- Embeddings deep dive: cosine similarity, and three chunking strategies (fixed-size, recursive, semantic)
- Stand up one vector database by hand: pgvector or Chroma is enough, and store and query embeddings yourself
- Reranking and hybrid search (BM25 plus vectors), and how to measure retrieval quality with recall at k
- Build a naive RAG pipeline with no framework: chunk, embed, store, retrieve, stuff into the prompt

## You ship this week

> A document Q&A tool over a real PDF corpus (your own notes, or a company’s public docs) that answers questions and cites the exact source chunk it used.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. Embeddings and chunking, the decisions that make or break retrieval

*About 3 hours*

When a document Q&A system gives a wrong answer, people blame the LLM. Most of the time the model never saw the right text. The paragraph that held the answer was split in half, buried inside a 3,000-word chunk about something else, or lost when a PDF table was flattened into a stream of numbers. Those failures are decided at indexing time, long before any prompt is written, by two choices: how you cut documents into chunks and how you turn each chunk into a vector. This lesson teaches both from the ground up, so that when retrieval fails on a client's documents you can say exactly which decision caused it and what to change.

Covers: The mental model: a learned coordinate system for meaning; What an embedding model actually is; Cosine, dot product and Euclidean distance.

### 2. A vector database by hand, pgvector first and Chroma second

*About 3 hours*

Every RAG system needs somewhere to keep vectors and a fast way to find the nearest ones. Tutorials hide this behind one line of a framework, so when retrieval is slow, returns different results after an index is added, or quietly ignores a filter, nobody on the team knows why. As an FDE you will also be asked the question that decides architecture: "Do we need a new vector database, or can we use what we already run?" Often the honest answer is Postgres with pgvector, which the client's DBAs already know how to back up and secure. This lesson builds the core operation yourself in plain Python, then stands up pgvector by hand, then shows the same thing in Chroma, so the database stops being a black box.

Covers: The mental model: a table, a distance function and a shortcut; What the database does without an index.

### 3. Hybrid search, reranking, and measuring retrieval with recall@k

*About 3.5 hours*

Vector search alone fails in ways that embarrass you in front of a client. A support agent pastes error code "U16" and gets an article about a different error. A finance user searches an invoice number and gets the invoice next to it. These are not edge cases in enterprise data; IDs, codes, product names and people's names are a large share of real queries. The fix is old and reliable: combine keyword search (BM25) with vectors, then rerank the best candidates with a more careful model. But no change to retrieval is an improvement until you have measured it. This lesson builds BM25, fusion and an evaluation harness from scratch, so every retrieval decision you make for a client comes with a number attached.

Covers: The mental model: two retrievers, one fusion, one judge, one scoreboard; Why embeddings struggle with IDs, codes and names; BM25, from first principles.

### 4. Naive RAG with no framework, then planning your document Q&A tool

*About 4 hours*

Retrieval-augmented generation is the most common thing clients will ask you to build, and the most common thing you will be asked to fix. Frameworks let you assemble a pipeline in ten lines, which is exactly the problem: when the bot confidently quotes last year's policy or answers from a chunk that has nothing to do with the question, ten lines of someone else's abstractions tell you nothing about which stage broke. Building the pipeline yourself, with every stage visible and logged, gives you the one skill that matters in production RAG: looking at a wrong answer and saying, with evidence, "extraction", "chunking", "retrieval", "context assembly" or "generation". This lesson builds that pipeline end to end and then sets you up to build the Week 3 deliverable.

Covers: The mental model: a search engine bolted to a careful reader; Indexing, offline; Query, per question; The whole pipeline, small enough to read in one sitting.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [Voyage AI docs: Text embeddings (input_type, output_dimension, limits)](https://docs.voyageai.com/docs/embeddings)
- [Claude docs: Embeddings (Anthropic's recommendation and Voyage examples)](https://platform.claude.com/docs/en/build-with-claude/embeddings)
- [Chroma research: Evaluating Chunking Strategies for Retrieval](https://www.trychroma.com/research/evaluating-chunking)
- [Anthropic: Introducing Contextual Retrieval](https://www.anthropic.com/news/contextual-retrieval)
- [pypdf docs: Extract text from a PDF](https://pypdf.readthedocs.io/en/stable/user/extract-text.html)
- [pgvector README (operators, HNSW, IVFFlat, filtering, iterative scans)](https://github.com/pgvector/pgvector)
- [pgvector-python README (Psycopg 3 usage)](https://github.com/pgvector/pgvector-python)
- [Chroma docs: Configure collections (distance space, HNSW parameters)](https://docs.trychroma.com/docs/collections/configure)
- [Chroma docs: Query and get](https://docs.trychroma.com/docs/querying-collections/query-and-get)
- [Malkov and Yashunin: Efficient and robust approximate nearest neighbor search using HNSW graphs](https://arxiv.org/abs/1603.09320)
- [Robertson and Zaragoza: The Probabilistic Relevance Framework: BM25 and Beyond](https://www.staff.city.ac.uk/~sbrp622/papers/foundations_bm25_review.pdf)
- [Cormack, Clarke and Büttcher: Reciprocal Rank Fusion outperforms Condorcet and individual Rank Learning Methods](https://cormack.uwaterloo.ca/cormacksigir09-rrf.pdf)
- [Voyage AI docs: Rerankers](https://docs.voyageai.com/docs/reranker)
- [Sentence Transformers: Cross-Encoder usage](https://sbert.net/docs/cross_encoder/usage/usage.html)
- [Claude docs: Search results (native RAG citations)](https://platform.claude.com/docs/en/build-with-claude/search-results)
- [Claude docs: Citations](https://platform.claude.com/docs/en/build-with-claude/citations)
- [Claude docs: Prompting best practices (long context: documents first, query last)](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)
- [OWASP GenAI: LLM01 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)

## Further reading

- [RAG (Retrieval-Augmented Generation)](https://aiengineeringfromscratch.com/lesson?path=phases%2F11-llm-engineering%2F06-rag)
- [Advanced RAG: Chunking, Reranking, Hybrid Search](https://aiengineeringfromscratch.com/lesson?path=phases%2F11-llm-engineering%2F07-advanced-rag)
- [Chunking Strategies for RAG](https://aiengineeringfromscratch.com/lesson?path=phases%2F05-nlp-foundations-to-advanced%2F23-chunking-strategies-rag)
- [Embedding Models: The 2026 Deep Dive](https://aiengineeringfromscratch.com/lesson?path=phases%2F05-nlp-foundations-to-advanced%2F22-embedding-models-deep-dive)

## Check yourself

Answer out loud before opening each answer.

<details><summary>Your embeddings are normalised to length 1. A teammate wants to switch the database from cosine distance to inner product. Will rankings change?</summary>

No. For unit vectors the dot product equals the cosine similarity, and Euclidean distance is a monotonic function of it (`||a-b||² = 2 - 2cos`), so all three give the same order. Inner product is often slightly faster to compute.

</details>

<details><summary>Why do bigger chunks tend to hurt retrieval for specific questions, even though they contain more information?</summary>

One vector must summarise the whole chunk, so a chunk covering several topics gets an averaged, diluted vector. A specific question matches it weakly and is beaten by a shorter chunk focused on that topic, even if the long chunk contains the answer.

</details>

<details><summary>Your RAG app returns slightly different chunks for the same question after you add an HNSW index. Is something broken?</summary>

No. HNSW is approximate: it returns probably-nearest neighbours, so some true top-k results can be missed. Measure index recall against exact search and raise `hnsw.ef_search` if it is too low.

</details>

<details><summary>Why does pgvector return the negative inner product from `&lt;#&gt;`?</summary>

Postgres index scans only run in ascending order, so the operator must make "most similar" the smallest value. Negating the inner product does that; multiply by -1 to display the real value.

</details>

<details><summary>Why does BM25 find "INV-2024-00731" when vector search returns "INV-2024-00713"?</summary>

To an embedding model both strings mean roughly "an invoice number", so their vectors are nearly identical. BM25 matches the exact token, and because that token is rare, its IDF gives it a large weight.

</details>

<details><summary>Why does RRF use ranks rather than the retrievers' scores?</summary>

Cosine similarities and BM25 scores are on different, incomparable scales, so adding them lets one retriever dominate. Ranks are on the same scale for every retriever, and `1/(k + rank)` rewards documents ranked well by several lists.

</details>

<details><summary>The right chunk is retrieved at rank 7 but you only put the top 5 in the prompt, and the bot says "I don't know". Which stage failed, and what are two fixes?</summary>

Context assembly, after a partial retrieval failure: the chunk was found but not ranked high enough to be used. Either rerank a deeper candidate list so it moves up, or pass more chunks if the token budget allows; then confirm with recall@5 on the evaluation set.

</details>

<details><summary>Why use an exact abstain sentence rather than "say if you are unsure"?</summary>

Code can detect an exact string, so you can measure abstention accuracy on unanswerable questions and handle abstentions in the interface. Free-form hedging cannot be reliably detected or tested.

</details>

---

**Learn Week 3 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week03). Week 1 is free.
