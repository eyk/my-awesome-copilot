# VS Code Workspace Custom Agents (`.agent.md`)

## Structure

VS Code discovers workspace custom agents from `.github/agents/*.agent.md`. Each file contains YAML frontmatter (metadata) and a prompt body (behavioral instructions).

## Frontmatter Fields

### `name`

- **Type**: string
- **Purpose**: Display name in the agent picker
- **Guidance**: Short, recognizable identifier (matches file name convention)

### `description`

- **Type**: string
- **Purpose**: Agent's intent shown in UI
- **Guidance**: Explain what the agent does and when to use it

### `argument-hint`

- **Type**: string
- **Purpose**: UI hint for user input
- **Guidance**: Suggest effective trigger phrases

### `model`

- **Type**: string
- **Purpose**: Preferred model for the agent
- **Common values**: `GPT-5 mini`, `GPT-4o`, `Claude Sonnet 4.5`
- **Guidance**: Balance latency and reasoning needs (mini for speed, larger for complex tasks)

### `infer`

- **Type**: boolean
- **Purpose**: Whether the agent may delegate to subagents
- **Default**: `false`
- **Guidance**: Enable only when delegation improves workflow

### `target`

- **Type**: string
- **Purpose**: Host integration target
- **Value for workspace agents**: `vscode`

### `tools`

- **Type**: array of strings
- **Purpose**: Tools the agent can call
- **Guidance**:
  - Favor read/search tools for safety
  - Add `edit`, `execute`, `web` only when clearly needed
  - User decides final selection via Tools konfigurieren

### `handoffs`

- **Type**: array of objects (optional)
- **Fields**:
  - `label`: Button text
  - `agent`: Target agent name/ID
  - `prompt`: Prompt sent to target
  - `send`: `true` to auto-send on click
- **Guidance**: Optional; ask user before adding

## Prompt Body Patterns

The prompt body defines the agent's role, constraints, and output style.

**Effective patterns:**

- **Role statement**: "You are a [type] agent."
- **Hard guardrails**: "CRITICAL: This agent has NO rights to..." or "Never attempt to..."
- **Goals**: Bulleted objectives
- **Rules**: Bulleted behavioral constraints

**Examples:**

- Chat-only agent: Forbid edits, implementation suggestions
- Planning agent: Require structured plans, prohibit coding
- Implementation agent: Require confirmation before risky operations

## Resources

- Handoffs documentation: https://code.visualstudio.com/docs/copilot/customization/custom-agents#_handoffs
