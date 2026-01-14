---
name: custom-agent-builder
description: Guide the creation, review, and maintenance of VS Code Copilot Chat workspace custom agents (.agent.md) under `.github/agents/`, including intent discovery, guardrail writing, tool selection, and optional handoffs.
---

# Custom Agent Builder (VS Code workspace)

## Overview

Guide the agent through creating high-quality VS Code custom agents located in `.github/agents/`, covering intent discovery, YAML frontmatter, prompt body guardrails, tooling recommendations, and optional handoffs.

## Workflow

1. Confirm the request targets a VS Code workspace agent (`.agent.md` under `.github/agents/`).
2. Ask the user for 1–2 sentences describing the agent's intent, scope, and fatal no-nos.
3. Copy and customize the template:
	- Copy `assets/agent-template.md` to `.github/agents/{agent-name}.agent.md`.
	- Replace all placeholders with the agent-specific values:
	  - `{agent_name}`: Hyphen-case name (e.g., `code-reviewer`)
	  - `{agent_description}`: Full description of what the agent does and when to use it
	  - `{argument_hint}`: User-facing hint for what to type
	  - `{tools_list}`: Comma-separated quoted tool identifiers
	  - `{handoff_label}`, `{handoff_agent}`, `{handoff_prompt}`: Handoff configuration (or remove if not needed)
	  - `{agent_role_statement}`: Opening statement defining the agent's role
	  - `{agent_guardrails}`: Critical constraints (e.g., "CRITICAL: This agent has NO rights to...")
	  - `{agent_goals}`: Bulleted list of agent objectives
	  - `{agent_rules}`: Bulleted list of behavioral rules
4. Select `tools` as a team:
	- Offer a single best-fit tool set derived from the intent, prioritizing read/search tools and adding risky tools only when clearly needed.
	- List the proposed tools in the chat as bullets with one-line rationales.
	- Fill `{tools_list}` with the selected tools.
	- Mention that the user can click **Tools konfigurieren** to adjust the selection.
5. Handle `handoffs`:
	- Ask if the user wants handoff buttons; if no, remove the `handoffs:` section from the template.
	- If yes, fill the handoff placeholders or link to the documentation (see Resources).
6. Finalize by reminding the user they own the agent file and can request changes through chat.

## Tool Collaboration

- Always ask before writing tools. Ask: "Shall I propose and prefill the tools, or do you want to select them manually?"
- When allowed, propose one best-fit suite and explain each tool's contribution to the intent.
- Highlight especially risky categories (e.g., `edit`, `execute`, `web`) and explain why they are included.
- User finalizes tools via the Tools konfigurieren UI or by instructing the agent.

## Handoffs Guidance

- Treat `handoffs` as optional and preference-driven.
- Ask: "Do you want me to suggest handoff buttons that link to other agents?"
- If the user declines, link them to https://code.visualstudio.com/docs/copilot/customization/custom-agents#_handoffs so they can learn more.

## Resources

- Agent template: `assets/agent-template.md` (copy this to create new agents)
- Field definitions and examples: `references/agent-file-format.md`

## Guardrails

- Keep the skill concise: include only what the agent truly needs to know.
- Prefer explicit constraints in the prompt body over implicit expectations.
- Never assume the tool selection is final; always invite the user to confirm or adjust.
