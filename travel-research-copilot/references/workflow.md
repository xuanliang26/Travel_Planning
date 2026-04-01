# Workflow Reference

## Contents

1. Intake and routing
2. Required input fields
3. Transport research
4. Lodging area research
5. Lodging candidate selection
6. Activity screening
7. Final brief assembly
8. Failure handling

## 1. Intake and Routing

Start every run by confirming the destination. If the destination is still unknown, stop the workflow and help the user narrow destinations first.

After destination confirmation:

1. Ask whether to start with `交通` or `住宿`.
2. If the user asks for a full planning brief, research both and merge.
3. If the user only wants one module, finish that module cleanly and offer to continue with the other one.

## 2. Required Input Fields

Treat the following fields as required before making concrete recommendations:

- `目的地`
- `出发地`
- `时间` or date range
- `预算`
- `同行人`
- `偏好/约束`

Use follow-up questions when any field is missing. If the user still cannot answer, continue only with clearly labeled assumptions.

Safe assumption examples:

- `预算未定，先按中档预算做初筛`
- `同行人未说明，先按 2 人自由行理解`

Unsafe assumptions:

- inventing exact transport prices
- assuming hotel quality without current ratings
- assuming attraction opening hours without a source

## 3. Transport Research

Research direct or most common mainstream options first. v1 does not attempt complex transfer optimization.

### Modes to Check

- flight
- high-speed rail
- standard train
- other common direct option when locally relevant

### Compare on These Dimensions

- `总成本`: fare plus obvious local transfer cost when it materially affects the recommendation
- `总耗时`: use door-to-door thinking when the difference is meaningful
- `出发/到达时段`: early departures, late arrivals, overnight burden
- `便利性`: baggage burden, station/airport distance, transfer friction
- `值不值得`: whether lower cost is worth extra travel time

### Recommendation Rule

Return:

- 1 recommended option
- 1 to 3 alternatives
- a short reason each alternative did not rank first

Useful heuristic:

- prefer rail when total time is close enough and cost is better or similar
- prefer flight when rail is materially slower or availability is poor
- use overnight train mainly as a budget fallback or when schedule fit is unusually strong

Do not present an obviously inconvenient route as the top choice unless the time or cost advantage is clearly worth it.

## 4. Lodging Area Research

Decide `住哪里` before listing specific properties.

### Signals to Review

- public destination guides
- map distance to core attractions or stations
- metro or public transport convenience
- food and convenience-store density
- evening safety and noise level
- tourist versus local atmosphere
- recurring visitor praise or complaints

### Output Shape

Return:

- 1 recommended area
- 1 or 2 backup areas
- a short explanation of who each area fits

Do not skip directly to hotel names.

## 5. Lodging Candidate Selection

After the area is chosen, shortlist hotel or homestay options that fit the budget and trip style.

### Filters

- budget range
- visible rating and review volume
- distance to metro, station, or core area
- property stability: not obviously noisy, far, or complaint-heavy

### Ranking Rule

Use this weighting logic:

- `位置便利度` around 40%
- `评分与评价量` around 30%
- `预算匹配度` around 20%
- `稳定性/明显风险` around 10%

### Output Shape

Return 3 to 5 candidates with:

- name
- area
- expected price band
- rating and review context if available
- why it is on the list
- main risk or trade-off
- source links

## 6. Activity Screening

Use public web search first. Xiaohongshu is a supporting signal, not the only gate.

### Suggested Search Directions

- `{destination} 景点 推荐`
- `{destination} citywalk`
- `{destination} 住哪里`
- `{destination} 避坑`
- `{destination} 雨天 去哪`
- `{destination} 小红书`

### Inclusion Rule

Add a place or activity into the main plan only when both are true:

1. Positive public signals are clearly stronger than negative ones.
2. No high-frequency severe complaint keeps repeating.

Typical severe complaint patterns:

- pure photo spot with weak actual experience
- long queues that ruin value
- overpriced and low substance
- inconvenient access
- poor maintenance or poor service

### Xiaohongshu Handling

Use Xiaohongshu only when public search snippets or user-provided links are accessible. When using it:

- sample multiple creators instead of one viral note
- ignore obvious ad tone or repeated templated copy
- treat it as sentiment and pitfall evidence, not factual authority

If evidence is mixed or sparse, place the spot into `待判断` instead of forcing it into the main plan.

## 7. Final Brief Assembly

Always return one Markdown brief. Use [output-template.md](output-template.md) as the structure.

The final brief must include:

- travel brief
- transport recommendation and alternatives
- lodging area recommendation and alternatives
- lodging candidates
- recommended places or activities
- pitfall summary
- pending confirmations
- next actions

## 8. Failure Handling

If a required fact cannot be confirmed:

- do not invent it
- mark it as `待确认`
- state what the user should verify next

If the user gives too little detail:

- ask targeted follow-up questions
- do not jump straight to a full draft

If sources conflict:

- show the conflict
- prefer the more authoritative source for factual claims
- keep the recommendation conservative
