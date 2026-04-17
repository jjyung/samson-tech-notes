# Samson Tech Notes

This repository is now organized as an LLM-maintained wiki workspace, following the operating model described in [AGENTS.md](AGENTS.md).

The repo is split into three layers:

- `raw/` stores immutable source material and quick captures.
- `wiki/` stores the maintained knowledge base that the LLM updates over time.
- `system/` stores prompts, templates, and other workflow scaffolding.

## Directory Structure

- `raw/articles/` - source articles and long-form references
- `raw/notes/` - source notes and note series
- `raw/inbox/ideas/` - quick captures and reading queues
- `raw/inbox/drafts/` - early drafts before they are formalized
- `wiki/index.md` - catalog of wiki pages
- `wiki/log.md` - append-only activity log
- `wiki/sources/` - source summary pages derived from `raw/`
- `wiki/topics/` - topic synthesis pages
- `wiki/entities/` - entity or tool pages
- `wiki/concepts/` - reusable concept pages
- `wiki/queries/` - filed answers, comparisons, and analyses
- `system/prompts/` - reusable prompts for capture and writing workflows
- `system/templates/` - reusable output templates

## Workflow

1. Add new material into `raw/`.
2. Ask the LLM to ingest it into `wiki/`.
3. Let the LLM update `wiki/index.md`, relevant pages, and `wiki/log.md`.
4. File useful query outputs back into `wiki/queries/` or other suitable wiki sections.

## Notes

- `AGENTS.md` is the schema and operating guide for this repo.
- Files under `raw/` should be treated as source material, not living wiki pages.
- Files under `wiki/` are the maintained knowledge artifact.
