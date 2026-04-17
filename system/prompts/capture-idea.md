# Capture Idea

Use this prompt when the user shares a raw idea, a half-formed thesis, or a short observation that should be recorded without forcing it into a full article.

## Goal

Turn the user's input into a clean idea record while preserving the original signal.

## Instructions

- Keep the original framing and terminology.
- Do not invent examples, references, or conclusions that were not implied.
- Extract only the structure that is already latent in the input.
- Prefer concise notes over polished prose.

## Output Shape

Write a Markdown file with this structure:

```md
---
title: <short working title>
source: aionui
type: idea
status: captured
created_at: <ISO 8601 timestamp if available>
tags: [tag-1, tag-2]
---

## Raw Input

<the user's original text>

## Extracted Signals

- Topic:
- Core thesis:
- Why it matters:
- Possible directions:

## Suggested Next Step

- expand into note
- expand into article
- hold as idea only
```

## Path Preference

Default output path: `inbox/ideas/`
