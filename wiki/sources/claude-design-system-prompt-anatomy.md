---
aliases:
  - Claude Design 系統提示 / 解剖
  - Claude Design System Prompt Anatomy
---
# Claude Design 系統提示解剖

## Source

- Title: `Claude Design 系統提示解剖 — Prompt Anatomy`
- Site: `gigaai.studio`
- Type: article / prompt analysis
- URL: [https://gigaai.studio/learning/claude-design-system-prompt.html?fbclid=IwdGRjcARcmQxjbGNrBFyYxmV4dG4DYWVtAjExAHNydGMGYXBwX2lkDDM1MDY4NTUzMTcyOAABHqPVbD0Xl7LOx8cos1QKfWyNYIm8x7W22DS9H0zjJTlYeRsuDVYeIr2wvr-R_aem_8B0iUmhRtaetVzlJrvwcHw](https://gigaai.studio/learning/claude-design-system-prompt.html?fbclid=IwdGRjcARcmQxjbGNrBFyYxmV4dG4DYWVtAjExAHNydGMGYXBwX2lkDDM1MDY4NTUzMTcyOAABHqPVbD0Xl7LOx8cos1QKfWyNYIm8x7W22DS9H0zjJTlYeRsuDVYeIr2wvr-R_aem_8B0iUmhRtaetVzlJrvwcHw)
- Reliability note: secondary explainer and framework reading, useful for pattern extraction but not a canonical source for the underlying prompt text.

## Summary

This article breaks down a Claude Design system prompt into a layered architecture. Instead of treating the prompt as a simple instruction block, it frames it as a control surface for design taste, workflow discipline, tool usage, and verification.

The key idea is that a strong agent prompt does not just say what to do. It shapes *how* the agent thinks: who it is, what standards it should uphold, when it should ask questions, how it should plan and verify, and which output patterns to avoid.

## Key Ideas

### 1. Prompt as architecture, not a checklist

The article argues that the prompt works like an architecture diagram:

- user request enters at the top
- layered guidance shapes behavior before execution
- verification and feedback are built into the loop
- output is constrained by structure, not just by wording

This is useful because it moves prompt design away from one-off instructions and toward a durable system.

### 2. Five layers of guidance

The article describes five major layers:

1. **Identity & Guardrails**
   - who the agent is
   - who it serves
   - what it must not reveal

2. **Taste & Discipline**
   - what good design looks like
   - what slop patterns to avoid
   - when to ask before adding more

3. **Workflow & Process**
   - clarify the request
   - inspect context
   - plan tasks
   - show early
   - verify at the end

4. **Tools & Protocols**
   - how tools are used
   - how verification works
   - what can be shown mid-task vs at completion

5. **Technical Specs**
   - concrete rules for layout, scale, and implementation details

The layering matters because higher levels set intent and lower levels set execution constraints.

### 3. Strong taste is encoded as constraints

A large part of the article is not about tooling but about aesthetics and discipline:

- establish a design system before producing content
- do not fill space with filler content
- avoid common AI slop patterns
- prefer placeholders over bad attempts
- do not invent colors when brand colors exist
- produce multiple variations instead of guessing one perfect answer

This turns subjective design judgment into repeatable operating rules.

### 4. Ask-first and context-first behavior

The prompt encourages the agent to ask before adding more and to avoid starting from zero when it can reuse existing context.

That means:

- ambiguous requests should be clarified
- the agent should look for UI kits, codebase context, or screenshots
- extra content should be confirmed before being added
- missing materials should be requested instead of improvised

This is a good reminder that better outputs often come from better framing, not from more generation.

### 5. Verification is part of the system

The article treats verification as a built-in sensor rather than an afterthought.

The loop is roughly:

- build
- show
- check errors or feedback
- iterate if needed
- verify silently when things are fine

That pattern is especially relevant for agent workflows because it prevents weak outputs from being treated as finished work.

## Relevance To This Repo

This piece connects directly to several existing notes:

- [AI Coding Agent 設計維度](../topics/agent-coding-agent-design-dimensions.md)
- [AI 輔助開發工作流](../topics/ai-assisted-development-workflow.md)
- [工程化讓 AI 輸出更穩定](../concepts/engineering-stabilizes-ai-output.md)
- [Plan-Gate-Execute](../../raw/articles/plan-gate-execute.md)

It is especially useful as a design reference for writing stronger system prompts and workflow prompts.

## Suggested Follow-up Pages

- [系統提示即架構](../topics/system-prompt-as-architecture.md)
- [AI Coding Agent 設計維度](../topics/agent-coding-agent-design-dimensions.md)
- [工程化讓 AI 輸出更穩定](../concepts/engineering-stabilizes-ai-output.md)
