---
name: copilot-models
description: Use when asked about GitHub Copilot LLM model availability, release status, retirement, preview/GA state, or request cost multipliers in IDEs, Copilot Chat, coding agent, or other Copilot surfaces.
---

# GitHub Copilot model availability and cost

Answer questions about which LLM models are available in GitHub Copilot and what they cost in request multipliers.

## Source of truth

Use the upstream compact JSON as the source of truth:

`https://raw.githubusercontent.com/sollie/copilot-model-availability/main/copilot_models.compact.json`

Do not answer from memory when the user asks about model availability, retirement, preview/GA status, or multipliers. Fetch the compact JSON first and base the answer on matching entries.

You may reuse a previously fetched copy of the JSON if it was fetched in the same agent session and less than one hour ago. If the cached copy is older than one hour, fetch the JSON again before answering.

If the compact JSON cannot be fetched, fall back to the GitHub Docs page:

`https://docs.github.com/en/enterprise-cloud@latest/copilot/reference/ai-models/supported-models#supported-ai-models-in-copilot`

The docs page requires more processing and may use more tokens, so only use it when the JSON is unavailable. If neither source can be fetched, say the current model data is unavailable rather than guessing.

## How to answer

- Prefer exact model-name matches from the fetched JSON. If there is no exact match, mention the closest matching model names from the JSON.
- Include the model name, provider when present, release status, paid-plan multiplier, and Copilot Free multiplier when those fields exist.
- When using the docs fallback, extract the relevant tables from the page instead of summarizing surrounding explanatory text.
- Treat `Not applicable` in `multiplier_for_copilot_free` as unavailable for Copilot Free for that multiplier field.
- If a model has `availability.release_status` set to `retired`, say it is retired and include `retirement.retirement_date` plus `retirement.suggested_alternative` when present.
- If a model is `Closing down ...`, say it is still listed but closing down on the date in that status.
- If a model lacks a `multiplier` object, say the multiplier is not listed in the data instead of guessing.
- Include the data timestamp from `generated_at` when the user asks how current the information is or when the answer depends on recent changes.
- Keep answers concise unless the user asks for a table or comparison.

## Useful JSON fields

- `generated_at`: when the data file was produced.
- `source_url`: upstream GitHub documentation used to produce the data.
- `models[].name`: model display name.
- `models[].provider`: provider, when listed.
- `models[].availability.release_status`: GA, public preview, closing down, retired, or other listed status.
- `models[].multiplier.multiplier_for_paid_plans`: paid-plan request multiplier.
- `models[].multiplier.multiplier_for_copilot_free`: Copilot Free request multiplier or `Not applicable`.
- `models[].retirement`: retirement date and suggested alternative for retired models.
