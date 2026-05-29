# copilot-model-skill

Claude Skill compatible guidance for answering questions about GitHub Copilot model availability and request cost multipliers.

The skill fetches its compact source of truth directly from:

`https://raw.githubusercontent.com/sollie/copilot-model-availability/main/copilot_models.json`

That upstream file is generated from GitHub's supported Copilot models documentation and checked for updates every hour.

Agents may reuse a JSON copy fetched during the same session for up to one hour, so repeated model questions do not require repeated downloads.

If the compact JSON cannot be fetched, the skill falls back to the GitHub Docs source page:

`https://docs.github.com/en/enterprise-cloud@latest/copilot/reference/ai-models/supported-models#supported-ai-models-in-copilot`

## Files

- `SKILL.md` - Claude Skill instructions and trigger description.
