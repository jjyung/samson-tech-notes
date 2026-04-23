---
aliases:
  - LLM Wiki
---
# LLM Wiki

## Source

- Title: `LLM Wiki`
- Author: `karpathy`
- Type: idea memo / operating pattern
- URL: [https://gist.githubusercontent.com/karpathy/442a6bf555914893e9891c11519de94f/raw/ac46de1ad27f92b28ac95459c782c07f6b8c964a/llm-wiki.md](https://gist.githubusercontent.com/karpathy/442a6bf555914893e9891c11519de94f/raw/ac46de1ad27f92b28ac95459c782c07f6b8c964a/llm-wiki.md)

## Summary

This piece argues that personal knowledge systems for LLMs should not stop at retrieval over raw files. Instead, the LLM should maintain a persistent markdown wiki that sits between the user and the source documents. New material is not merely indexed for future search; it is read, summarized, cross-linked, and merged into an evolving knowledge base.

The central shift is from "answering from scattered documents each time" to "compiling knowledge once, then continuously maintaining it." In that model, the wiki becomes the durable artifact, and the LLM acts more like a maintainer than a chatbot.

## Key Ideas

### 1. Persistent wiki beats repeated reconstruction

Standard RAG-style workflows repeatedly rediscover the same knowledge at query time. The article's alternative is a maintained wiki where synthesis, contradictions, and cross-references accumulate over time.

Why this matters:

- repeated questions get cheaper
- multi-source synthesis is preserved instead of re-derived
- knowledge quality can improve incrementally as new sources arrive

### 2. The wiki is the compounding artifact

The most important object is not the chat session or vector index, but the wiki itself. The wiki stores summaries, topic pages, entity pages, comparisons, and analyses that remain useful after the current conversation ends.

Practical implication:

- valuable answers should often be filed back into the wiki as pages

### 3. Clear separation of three layers

The article proposes a simple architecture:

- raw sources: immutable source material
- wiki: LLM-maintained markdown knowledge base
- schema: the instruction file that defines structure and workflow

This separation keeps source truth, synthesized knowledge, and operating rules from getting mixed together.

### 4. LLM as maintainer, human as curator

The human is responsible for choosing sources, directing inquiry, and judging what matters. The LLM handles bookkeeping work such as summarizing, cross-linking, updating related pages, and logging changes.

This is a workflow claim as much as a technical one: LLMs are valuable not just for answering, but for maintaining coherence across many files.

### 5. Query output should become knowledge

The article treats queries as part of knowledge production rather than disposable chat. If a question produces a useful comparison, synthesis, or memo, that output should be saved as a new page in the wiki.

This creates a feedback loop:

- ingest sources
- ask questions
- save useful answers
- strengthen the wiki

### 6. Maintenance is a first-class operation

Beyond ingest and query, the article emphasizes linting the wiki for:

- contradictions
- stale claims
- orphan pages
- missing entity or concept pages
- absent cross-references
- data gaps worth further research

This frames knowledge-base quality as an ongoing maintenance problem, not a one-time setup task.

## Memorable Framing

- Obsidian is the IDE
- the LLM is the programmer
- the wiki is the codebase

This framing is useful because it turns note-taking into an operational system with structure, tooling, and iterative improvement.

## Why It Resonates

This model works well when:

- you are accumulating knowledge over weeks or months
- the topic needs repeated synthesis across many sources
- you want durable structure instead of ephemeral chat answers
- maintaining cross-links manually would be too tedious

It is especially strong for research, technical reading, book notes, internal team knowledge, and long-running personal learning projects.

## Limits And Caveats

- The article is intentionally abstract and does not prescribe one fixed directory layout.
- It assumes you are willing to let the LLM write and reorganize many markdown files.
- The quality of the wiki depends heavily on the schema and workflow discipline.
- Small collections may not need extra search tooling beyond a strong `index.md`.

## Relevance To This Repo

This repository is already aligned with the article's model:

- [raw/](../../raw/) matches the raw source layer
- [wiki/](../../wiki/) matches the maintained knowledge layer
- [AGENTS.md](../../AGENTS.md) acts as the schema layer

The note therefore serves as both a source summary and a design rationale for the repo structure itself.

## Suggested Follow-up Pages

- [持久化 Wiki 與 RAG 的差異](../concepts/persistent-wiki-vs-rag.md)
- [Wiki 維護](../concepts/wiki-maintenance.md)
- [Ingest 工作流](../topics/ingest-workflow.md)
- [Query 即知識生產](../topics/query-as-knowledge-production.md)
