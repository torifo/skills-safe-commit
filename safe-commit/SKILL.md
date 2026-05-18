---
name: safe-commit
description: Use before running git commit - validates staged changes for secrets, AI attribution, large files, and policy violations, blocks unsafe commits with reasons
---

# Safe Commit

## Overview

Validate staged changes before commit. Block on secrets, AI attribution,
oversized files, or policy violations. Approve with rewritten message
if needed.

## When to Use

- About to run `git commit` with staged changes
- After commit skill proposes a message but before execution
- As a hook before any commit operation

## Validation Checks

### 1. Secret Scan

Run `git diff --staged` and search for:
- API keys: `[A-Za-z0-9]{32,}`, `sk-`, `ghp_`, `xox[baprs]-`
- AWS: `AKIA[0-9A-Z]{16}`, `aws_secret_access_key`
- Generic: `password\s*=\s*["'][^"']+`, `token\s*=\s*["'][^"']+`
- Private keys: `-----BEGIN .* PRIVATE KEY-----`

### 2. AI Attribution

Search staged content AND commit message for:
- `Co-Authored-By: Claude`
- `Generated with Claude Code`
- `🤖 Generated`
- Any `Anthropic` attribution

### 3. File Policy

Block if staged includes:
- Files matching `.gitignore-private` patterns
- Design assets in non-design dirs (`.psd`, `.ai`, `.sketch`, `.fig`)
- Files larger than 5MB (warn at 1MB)
- `.env`, `.env.local`, `credentials.json`

### 4. Commit Message Format

Verify message has:
- English subject line
- `---` separator
- Japanese subject/body
- NO `Co-Authored-By: Claude...` lines

## Output Format

**On BLOCK:**
```
🚫 BLOCKED — cannot commit

Reasons:
  1. Secret detected in src/config.ts:42 (API key pattern)
  2. AI attribution in commit message (Co-Authored-By: Claude)
  3. Large file: assets/video.mp4 (12MB)

Fix these issues and try again.
```

**On APPROVE:**
```
✅ APPROVED

Files (3): auth.ts, auth.test.ts, README.md
Message preview:
  Add user authentication
  ---
  ユーザー認証を追加

Run: git commit
```

## Rules

1. NEVER let commits with secrets through
2. NEVER allow AI attribution in messages or code
3. ALWAYS show reasons when blocking
4. ALWAYS verify bilingual message format
5. Combine with `commit` skill for message creation

## Red Flags — STOP

- "Just this once for an emergency commit" → secrets are forever
- "It's not really a secret, just an example" → block anyway
- "AI attribution is fine for this team" → user convention is no attribution
- "The file is just slightly over 5MB" → block, ask user explicitly
