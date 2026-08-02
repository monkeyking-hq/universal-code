# Universal Code

**Version**: 1.0.0  
**Canonical source**: https://github.com/monkeyking-hq/universal-code/blob/main/UC-v1.0.0.md

## Overview

The Universal Code is a simple, semantically versioned ethical foundation designed for AI agents, models, and systems. It places an absolute priority on preventing physical harm to humans (including self-harm) through action or inaction, then provides an open list of foundational principles drawn from the overlapping moral core of the world’s major ethical and religious traditions.

It is intended to be referenced by version in system prompts and kept as a living, auditable standard.

## Why It’s Needed

AI agents increasingly take real-world actions that can affect human safety, trust, and systems. Without a shared, referenceable, and versioned ethical baseline, behavior drifts, cultural assumptions go unexamined, and the risk of preventable harm rises.

Existing frameworks are often too narrow, too culturally specific, too vague, or too rigid for reliable use in system prompts. The Universal Code supplies a clear, citable standard that agents can reason about and humans can audit.

## How to Use It

- Embed the **compact form** directly in system prompts and always reference it by version (`Universal Code v0.1.0`).
- Treat the **full canonical form** in this repository as the authoritative source.
- Define **contextual corollaries** for each agent or system that map the principles onto concrete tools, environments, and responsibilities.
- High-impact scripts or actions that affect production, staging, or shared environments require dual human approval (DevOps + Security) before execution (except for explicitly sandboxed local development).

## How We Made It

We distilled the principles from the common moral denominators across major traditions, including Judaism, Christianity, Islam, Buddhism, Hinduism, Confucianism, Taoism, Stoicism, and secular humanist ethics.

Strong universals include:
- Non-harm / sanctity of life
- Truthfulness
- Non-stealing
- The Golden Rule
- Justice and fairness
- Restraint and humility in the use of power

The principle of living in harmony with the natural world carries a deliberate Eastern emphasis (Taoist harmony with the Dao, Buddhist interdependence / dependent origination, and related ecological strands). This tilt was an explicit design choice while remaining compatible with stewardship concepts found in other traditions.

The list is intentionally open-ended. Semantic versioning was adopted from the start so the Code can evolve without breaking existing references.

## How to Contribute

Proposals, critiques, expansions, and discussion belong in [GitHub Discussions](https://github.com/monkeyking-hq/universal-code/discussions).

When contributing, please:
- Reference the specific principle or section you are addressing
- Explain the rationale and any supporting tradition, practical need, or edge case
- Follow semantic versioning expectations:
  - **MAJOR** — Breaking changes to the Supreme Principle or core structure
  - **MINOR** — New principles or significant clarifications
  - **PATCH** — Wording improvements and non-breaking refinements

All constructive contributions are welcome.
