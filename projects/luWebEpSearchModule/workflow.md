# Knowledge Base workflow

## Purpose

This Knowledge Base stores durable project knowledge, investigation results, architecture notes, deployment specifics, validation behavior, and AI-agent guidance. Its purpose is to avoid repeating investigations and to give future agents consistent context.

## Updating knowledge

After completing an investigation:

1. Create or update a focused file under `investigations/`.
2. Record the problem, reproduction, diagnostics, evidence, conclusion, and follow-up actions.
3. Update `AGENTS.md` with only the final durable lessons and invariants.
4. Keep detailed logs, hypotheses, and long transcripts in the investigation file or daily notes.
5. Do not promote an unverified hypothesis to a project fact.

Before any new task, read `KnowledgeBase/projects/luWebEpSearchModule/AGENTS.md` and check the relevant topic document and existing investigations.

## Document Update Rule

When completing an investigation:

1. Save detailed findings into a focused document under `investigations/`.
2. Add only final conclusions, reusable invariants, and lessons learned to `AGENTS.md`.
3. Keep `AGENTS.md` concise and focused on project knowledge that applies to future tasks.
4. Do not store large logs, stacktraces, experiment history, or unverified hypotheses in `AGENTS.md`; keep them in the investigation document or daily notes.

Before starting a new investigation, read the existing investigation files and update the relevant one instead of creating duplicate notes.

## Prompt templates

### New Feature Development

```text
Read KnowledgeBase/projects/luWebEpSearchModule/AGENTS.md
and use it as project context.

Task:
<describe feature>
```

### Investigation

```text
Read KnowledgeBase/projects/luWebEpSearchModule/AGENTS.md.

Continue investigation:

<describe issue>
```

### Code Generation

```text
Read KnowledgeBase/projects/luWebEpSearchModule/AGENTS.md.

Generate code according to existing architecture and conventions.

Task:
<describe change>
```

### Bug Analysis

```text
Read KnowledgeBase/projects/luWebEpSearchModule/AGENTS.md.

Analyze the issue using existing investigation notes,
known limitations and project-specific implementation details.

Problem:
<error/log/stacktrace>
```

### Refactoring

```text
Read KnowledgeBase/projects/luWebEpSearchModule/AGENTS.md.

Refactor the implementation while preserving existing
architecture, validation flow, deployment assumptions
and integration contracts.

Task:
<describe refactoring>
```

### Default Prompt

```text
Read KnowledgeBase/projects/luWebEpSearchModule/AGENTS.md.

Use it as the source of truth for:
- architecture;
- validation flow;
- deployment specifics;
- debugging notes;
- investigation history;
- development conventions.

Task:
...
```
