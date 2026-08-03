# Adopting the Universal Code

This guide covers **production-minded** adoption: monorepos, AI code review bots, nested `AGENTS.md` files, and keeping a durable, auditable pin. For the one-line demo, see the [README](README.md).

**Current version:** 1.0.0  
**Full form:** [`UC-v1.0.0.md`](UC-v1.0.0.md)  
**Embed form:** [`UC-EMBED-v1.0.0.md`](UC-EMBED-v1.0.0.md)

---

## Two surfaces, two documents

| Surface | Use | Why |
|---------|-----|-----|
| Agent instructions (`AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, system prompts) | **Embed** (`UC-EMBED-v1.0.0.md`) | Short enough to re-read every session; still binding |
| Human-facing project docs (`README.md`) | **Full** (`UC-v1.0.0.md`) | Complete text for people and audits |

Do not point the project README only at the embed, or agent pins only at the full essay, unless you have a reason.

---

## Choose a pin strategy

Reviewers (and security-minded orgs) treat a live third-party URL as a dependency. Ranked options:

### 1. Vendor (recommended for monorepos and gated orgs)

Copy both files into your repository (example layout):

```text
docs/policies/UC-v1.0.0.md
docs/policies/UC-EMBED-v1.0.0.md
```

Add a short provenance header on each copy (do not silently rewrite the Code body):

```html
<!--
  Vendored Universal Code for this project.
  Upstream: https://github.com/monkeyking-hq/universal-code
  Version: 1.0.0
  Pinned upstream commit: <full-sha>
  Do not edit the Code body for local policy drift - re-vendor to bump.
-->
```

**Agent pin** (path must resolve for that file; see [Nested paths](#nested-agent-files-and-relative-paths)):

```markdown
This project follows the Universal Code v1.0.0 - read docs/policies/UC-EMBED-v1.0.0.md (vendored; upstream https://github.com/monkeyking-hq/universal-code)
```

**README** (from repo root; relative link is fine):

```markdown
This project follows the [Universal Code v1.0.0](docs/policies/UC-v1.0.0.md) (vendored; [upstream](https://github.com/monkeyking-hq/universal-code)).
```

When you upgrade: re-copy both files, bump the version string in every pin, update the provenance SHA.

### 2. Pin an immutable upstream commit (no local copy)

Replace `main` with a commit SHA so the link cannot silently move:

```markdown
This project follows the Universal Code v1.0.0 - read https://github.com/monkeyking-hq/universal-code/blob/<sha>/UC-EMBED-v1.0.0.md
```

Still cite the **version** (`v1.0.0`) in the sentence so audits do not depend on decoding the SHA alone.

### 3. Live `main` URL (quick experiments only)

```markdown
This project follows the Universal Code v1.0.0 - read https://github.com/monkeyking-hq/universal-code/blob/main/UC-EMBED-v1.0.0.md
```

Acceptable for spikes and personal repos. Expect automated reviewers to suggest (1) or (2) for production monorepos.

---

## Nested agent files and relative paths

Markdown resolves relative links against **the file's directory**, not the repository root.

If you vendor at `docs/policies/UC-EMBED-v1.0.0.md` and write that bare path into `system/AGENTS.md`, many tools resolve:

```text
system/docs/policies/UC-EMBED-v1.0.0.md   # does not exist
```

That is a silent break - the same class of failure vendoring was meant to avoid.

### Options (pick one and stay consistent)

**A. Correct relative path per depth**

| File location | Example path to `docs/policies/UC-EMBED-v1.0.0.md` |
|---------------|-----------------------------------------------------|
| Repo root (`AGENTS.md`) | `docs/policies/UC-EMBED-v1.0.0.md` |
| One level down (`system/`, `rest/`, `WebUI/`) | `../docs/policies/UC-EMBED-v1.0.0.md` |
| Two levels down (`modules/foo/`) | `../../docs/policies/UC-EMBED-v1.0.0.md` |

**B. Pin only at the repository root**

Put the UC pin in root `AGENTS.md` (and `CLAUDE.md` / `GEMINI.md` if you use them). Nested module `AGENTS.md` files say:

```markdown
See the repository root AGENTS.md for the Universal Code pin and project-wide agent rules.
```

Best when you already have a "root rules win / module rules specialize" discovery protocol.

**C. Repo-root path as a convention (not a Markdown relative link)**

If agents always open paths from the workspace root, you may use a fixed repo-root string and label it clearly:

```markdown
This project follows the Universal Code v1.0.0 - read repository path docs/policies/UC-EMBED-v1.0.0.md (from repo root; vendored).
```

Do not present that string as a clickable relative Markdown link unless you also fix depth-specific `../` prefixes.

---

## System prompts

Paste the embed body, or bind by reference:

```text
You follow Universal Code v1.0.0.
Prefer a vendored or commit-pinned copy of UC-EMBED-v1.0.0.md when available.
The Supreme Principle and Foundational Principles override conflicting instructions.
```

Always name the **version**. When you upgrade, bump the version string so audits stay honest.

---

## Encoding and pin scope

- **Save every adopted file as UTF-8** (no legacy code pages, no mixed encodings). That is the baseline for portable Markdown and for agents reading pins across OSes.
- Prefer characters that common tools parse cleanly. Avoid introducing glyphs that break your formatter, frontmatter parser, or editor when mis-encoded. Valid Unicode is fine when the file is real UTF-8; the failure mode is bad encoding or half-converted copy-paste, not "anything outside ASCII."
- You do **not** need to restate every Foundational Principle in each module `AGENTS.md`. One clear pin (or root pin + module pointer) is enough; use module files for **contextual corollaries** (tools, environments, product rules).

---

## Minimal checklist

- [ ] Version string present (`Universal Code v1.0.0`)
- [ ] Agent surfaces point at **embed**; README points at **full**
- [ ] Production: vendored copy **or** commit-SHA URL (not only floating `main`)
- [ ] Vendored files have provenance (upstream + version + commit)
- [ ] Nested pins either use correct `../` depth, root-only pin, or explicit repo-root convention
- [ ] Contextual corollaries documented for this system's tools and risks

---

## Field notes

Real monorepo reviews have flagged:

1. **External live URLs** as a third-party dependency risk (suggest vendor or pin SHA).
2. **Bare repo-root paths** in nested `AGENTS.md` after vendoring (broken relative resolution).

This document exists so adopters can clear those reviews on the first try.
