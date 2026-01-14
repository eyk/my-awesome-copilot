---
name: {agent_name}
description: {agent_description}
argument-hint: {argument_hint}
model: GPT-5 mini
infer: false
target: vscode
tools: [{tools_list}]
handoffs:
  - label: {handoff_label}
    agent: {handoff_agent}
    prompt: {handoff_prompt}
    send: true
---

{agent_role_statement}

{agent_guardrails}

Goals:
{agent_goals}

Rules:
{agent_rules}
