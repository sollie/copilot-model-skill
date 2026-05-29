# copilot-model-skill

Claude Skill compatible guidance for answering questions about GitHub Copilot model availability and request cost multipliers.

The skill fetches its compact source of truth directly from:

`https://raw.githubusercontent.com/sollie/copilot-model-availability/main/copilot_models.compact.json`

That upstream file is generated from GitHub's supported Copilot models documentation and checked for updates every hour.

Agents may reuse a JSON copy fetched during the same session for up to one hour, so repeated model questions do not require repeated downloads.

If the compact JSON cannot be fetched, the skill falls back to the GitHub Docs source page:

`https://docs.github.com/en/enterprise-cloud@latest/copilot/reference/ai-models/supported-models#supported-ai-models-in-copilot`

## Installation

Install the skill with the `skills` CLI:

```bash
npx skills add sollie/copilot-model-skill --global --agent claude-code
```

Restart your agent session after installation so the new skill is loaded.

To choose the install scope or agent interactively, omit the flags:

```bash
npx skills add sollie/copilot-model-skill
```

## Files

- `SKILL.md` - Claude Skill instructions and trigger description.
