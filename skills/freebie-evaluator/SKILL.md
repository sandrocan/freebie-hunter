---
name: freebie-evaluator
description: Conservative scorecard for free classified listings with a focus on resale potential.
---

# Freebie Evaluator

Use this skill when scoring free classified listings for possible resale value.

## Goal

Score only what is evidenced. The user wants to know whether a free item is
likely to be resellable or at least worth manual review.

## Anti-Hallucination Rules

- Never invent brand, model, material, condition, or image details.
- If details are missing, lower `confidence` and `resaleScore`.
- If an image is unclear or unavailable, say so explicitly.
- If an item looks bulky, old, generic, or hard to transport, score
  conservatively.

## Positive Signals

- recognizable branded goods
- categories with likely demand: tools, solid wood furniture, good small
  furniture, lamps, design objects, children's vehicles, usable electronics
- clean or well-maintained appearance
- specific product details

## Negative Signals

- looks like disposal waste
- heavy wear
- unclear defects
- generic title with little detail
- hygiene risks or visible damage
- large transport burden without brand or quality signal

## Required Output

Always return this JSON shape:

```json
{
  "resaleScore": 0,
  "confidence": "low",
  "reasons": [],
  "riskFlags": [],
  "estimatedFlipPotential": "",
  "recommendedAction": "review",
  "stage": "list"
}
```

## Field Rules

- `resaleScore`: integer from 0 to 100
- `confidence`: `low`, `medium`, or `high`
- `reasons`: 2 to 5 short evidence-based reasons
- `riskFlags`: short warnings such as `unknown-brand`, `condition-unclear`,
  `bulky-item`, or `missing-detail-page`
- `estimatedFlipPotential`: conservative verbal estimate: `low`, `medium`, or
  `high`
- `recommendedAction`: `ignore`, `review`, `shortlist`, or `contact`
- `stage`: `list` or `detail`

## Scoring Heuristic

- `0-20`: little or no plausible value
- `21-39`: weak, many risks
- `40-69`: interesting but uncertain
- `70-84`: clearly shortlist-worthy
- `85-100`: unusually interesting; review quickly
