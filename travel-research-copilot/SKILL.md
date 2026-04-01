---
name: travel-research-copilot
description: Research-first travel planning workflow for China domestic leisure trips after the destination is known. Use when Codex needs to turn a natural-language trip request into a structured planning brief by asking for missing trip constraints, comparing direct transport options, recommending lodging areas and hotel candidates, screening activities from public web research plus optional Xiaohongshu sentiment signals, and producing a source-backed Markdown trip draft with risks and next actions.
---

# Travel Research Copilot

## Overview

Use this skill when the user already knows the destination and wants a practical trip-planning draft instead of bookings. Work in Chinese by default, ask for missing constraints first, research public sources second, and only then make recommendations.

## Quick Start

1. Confirm the destination and ask whether to start with `交通` or `住宿`.
2. Collect missing inputs before researching. Treat `出发地`, `时间`, `预算`, `同行人`, and `偏好/约束` as required.
3. Follow the routing and scoring rules in [workflow.md](references/workflow.md).
4. Apply the source and confidence rules in [source-rules.md](references/source-rules.md).
5. Return one structured Markdown draft using [output-template.md](references/output-template.md).

## Typical Requests

- `我想五一去杭州，先看交通。`
- `去成都，先看住宿，预算每晚 600 左右。`
- `目的地定了西安，帮我整理一个完整的出游研究草案。`

## Required Behavior

- Ask follow-up questions when required trip fields are missing.
- Compare direct transport first. Do not invent complex transfer routing in v1.
- Recommend lodging areas before recommending specific properties.
- Treat Xiaohongshu as auxiliary sentiment and pitfall evidence, not the sole basis for a decision.
- Attach sources for key facts such as price, schedule, rating, business hours, ticket info, location, and restrictions.
- Mark uncertain or time-sensitive facts as `待确认`.
- Give one recommended option, one to three alternatives, and short reasons for the ranking.

## Workflow

### 1. Intake

Confirm the destination. Ask whether to start with `交通` or `住宿`. If the user asks for a full plan, research both paths and merge the result into one final brief.

### 2. Transport

Use the transport rubric in [workflow.md](references/workflow.md). Compare plane, high-speed rail, train, and other common direct options. Recommend one option and explain why the others lost.

### 3. Lodging

Use the lodging rubric in [workflow.md](references/workflow.md). Research the best area first by looking at public guides, map convenience, transit access, safety, and common visitor sentiment. Only then shortlist properties inside that area.

### 4. Activity Screening

Search public web sources with destination-specific keywords. Use Xiaohongshu only if public results or user-provided links are available. Include a place only when sentiment is clearly positive and repeated severe complaints are absent.

### 5. Final Draft

Assemble one Markdown planning brief with recommendations, alternatives, pitfalls, sources, pending confirmations, and next actions.

## Research Standards

- Prefer official sites and large public travel sources for hard facts.
- Use review-heavy or creator-heavy sources for sentiment, atmosphere, and pitfalls.
- Show source conflicts instead of averaging them away.
- Never present stale prices, schedules, or business hours as guaranteed.

## Output Rules

- Produce one coherent Markdown draft, not scattered notes.
- Keep sections in the order shown in [output-template.md](references/output-template.md).
- Be explicit about why an option is recommended and why alternatives lost.
- End with a short `下一步动作` list that the user can act on immediately.

## Resources

- [workflow.md](references/workflow.md): step-by-step workflow, routing rules, scoring rubrics, and inclusion logic.
- [source-rules.md](references/source-rules.md): source hierarchy, citation policy, confidence rules, and Xiaohongshu guidance.
- [output-template.md](references/output-template.md): final Markdown structure and field expectations.
