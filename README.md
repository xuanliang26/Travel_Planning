# Travel Research Copilot

A research-first travel planning skill for China domestic trips.

Instead of acting like a booking site, Travel Research Copilot turns a destination-first travel idea into a practical planning brief: how to get there, where to stay, what is worth doing, what to skip, and what still needs verification.

## What it does

- asks for the missing trip constraints before researching
- compares direct transport options with trade-offs, not just raw prices
- recommends where to stay before recommending specific hotels
- prefers chain hotel sources such as Huazhu and Atour when checking lodging options
- uses public web research plus Xiaohongshu signals to surface highlights and pitfalls
- produces a source-backed Markdown brief with recommendations, alternatives, risks, and next actions

## Product philosophy

This project is built around a simple idea: trip planning is mostly repeated decision-making.

The value is not only in collecting information, but in applying a consistent workflow:

1. lock the destination
2. decide whether to research transport or lodging first
3. compare realistic options
4. filter noise from useful signals
5. output something practical enough to act on

## Current scope

v1 is intentionally narrow so the workflow stays strong.

- China domestic leisure trips
- destination already known
- couple / solo / small-group casual travel
- direct transport comparison first
- lodging-area recommendation before property shortlist
- chain hotels first, other properties only when chain options are weak or unavailable
- public web research plus Xiaohongshu as a signal layer
- no booking, no account system, no historical project database

## How the workflow works

### 1. Intake

Collect destination, departure city, dates, budget, travel party, and preferences. If any key field is missing, ask follow-up questions instead of guessing.

### 2. Transport

Compare direct flight, high-speed rail, train, and other mainstream options. Rank them by total cost, total time, convenience, and whether the savings are worth the friction.

### 3. Lodging

Research the best area first. Then check chain hotel ecosystems such as Huazhu and Atour in that area. If chain choices are limited, overpriced, or clearly poor-fit, expand to other hotels or homestays.

### 4. Activities

Search public guides and destination keywords, then use Xiaohongshu to validate vibe, avoid obvious traps, and spot repeated complaints.

### 5. Final brief

Return one structured Markdown plan with:

- travel brief
- transport recommendation and alternatives
- lodging area recommendation and backup areas
- hotel shortlist
- recommended places and pending decisions
- pitfalls, source links, and next actions

## Repository structure

- `travel-research-copilot/SKILL.md`: skill definition and behavior rules
- `travel-research-copilot/references/workflow.md`: routing, scoring, lodging, and activity workflow
- `travel-research-copilot/references/source-rules.md`: source hierarchy, citation, and confidence policy
- `travel-research-copilot/references/output-template.md`: final Markdown output shape
- `travel-research-copilot/agents/openai.yaml`: UI-facing metadata for the skill

## Example prompts

- `我想五一去杭州，先看交通。`
- `去成都，先看住宿，预算每晚 600 左右。`
- `山西太原，从杭州出发，7 天，情侣出行，想看全部。`
- `目的地定了西安，先帮我判断住哪里，再看连锁酒店。`

## Why chain hotels first

For this workflow, chain hotels are useful because they reduce uncertainty.

Compared with random listings, chain brands usually make it easier to verify:

- location consistency
- room standards
- loyalty ecosystem and app availability
- review stability
- whether the property is a safe default for a relaxed trip

The current default is to check chain ecosystems such as Huazhu and Atour first, then widen the search only when they do not provide good enough options in the recommended area.

## Validation

If you want to validate the skill structure locally, run:

```bash
python3 /Users/wxl/.codex/skills/.system/skill-creator/scripts/quick_validate.py /Users/wxl/Desktop/travel_planner/travel-research-copilot
```

Note: on this machine, that validator currently needs `PyYAML` installed in Python.

## Roadmap

- add prompt kits for common trip types
- add a more explicit chain-hotel decision rubric
- evolve the workflow into a reusable agent
- build a lightweight web form and result page on top of the same logic
