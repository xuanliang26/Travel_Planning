# Travel Planner

This repository contains the `travel-research-copilot` skill prototype for turning a destination-first trip request into a structured China travel research brief.

## What is included

- `travel-research-copilot/SKILL.md`: trigger description and operating rules
- `travel-research-copilot/references/workflow.md`: routing, transport, lodging, and activity decision rules
- `travel-research-copilot/references/source-rules.md`: citation and confidence policy
- `travel-research-copilot/references/output-template.md`: final Markdown structure
- `travel-research-copilot/agents/openai.yaml`: UI metadata for the skill

## Product shape

- Skill-first v1
- China domestic leisure travel
- Destination already known
- Public web research plus optional Xiaohongshu sentiment support
- Markdown output with recommendations, alternatives, risks, sources, and next actions

## Validation

Run:

```bash
python3 /Users/wxl/.codex/skills/.system/skill-creator/scripts/quick_validate.py /Users/wxl/Desktop/travel_planner/travel-research-copilot
```

## Next logical upgrades

- add a dedicated prompt kit for common trip types
- turn the workflow into a reusable agent
- build a lightweight web form and result page on top of the same decision rules
