# skills-safe-commit

> Pre-commit validator for secrets, AI attribution, and policy violations

A [Claude Code](https://claude.ai/code) skill that validates staged changes before committing. Blocks on secrets, AI attribution, oversized files, and policy violations.

[日本語はこちら](./README.ja.md)

## Install

```bash
git clone https://github.com/torifo/skills-safe-commit /tmp/skills-safe-commit
cp -r /tmp/skills-safe-commit/safe-commit ~/.claude/skills/
```

## Usage

Triggers before `git commit` with staged changes.

**What it checks:**
- Secrets and credentials (API keys, tokens, private keys)
- AI attribution in commit messages
- Oversized files (warn at 1MB, block at 5MB)
- Policy violations (`.env` files, design assets in wrong dirs)

**What it does:**
- Blocks the commit with clear reasons if any check fails
- Approves and shows commit preview if all checks pass

## Related Skills

- [skills-secret-scan](https://github.com/torifo/skills-secret-scan) — deeper secret scanning across files and history
- [skills-commit](https://github.com/torifo/skills-commit) — bilingual commit workflow to run after safe-commit approves
