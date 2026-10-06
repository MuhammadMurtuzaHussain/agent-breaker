# AgentBreaker

A red-team playbook for breaking LLM agents — tool-calling, RAG, MCP and memory-backed — in authorised security testing and prompt-injection CTFs such as Lakera's Agent Breaker.

## What it covers

- A recon-first workflow and a decision tree for reading an agent's response (blocked / ignored / leaked) and picking the next move
- Seven injection techniques: tool-description poisoning, memory poisoning, indirect document injection, planted-record framing, turning the system prompt against itself, fake tool-output identity spoofing, and system-prompt extraction
- Verbatim worked payloads from sanctioned CTF runs
- What reliably fails (obfuscation, encoding) and why

**Companion skill:** [AgentArmor](https://github.com/MuhammadMurtuzaHussain/agent-armor) — the defensive checklist for the same attack classes.

## Install

As a Claude Skill:

```bash
git clone https://github.com/MuhammadMurtuzaHussain/agent-breaker ~/.claude/skills/agent-breaker
```

## Scope

Authorised red-team engagements and sanctioned CTFs only — not for production systems or anyone's data without written authorisation. See `SKILL.md` for the full scope note.
# agent-breaker
