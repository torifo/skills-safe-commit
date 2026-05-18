[English](#english) | [日本語](#日本語)

---

## English

### skills-safe-commit

> Pre-commit validator for secrets, AI attribution, and policy violations

A [Claude Code](https://claude.ai/code) skill that validates staged changes before committing. Blocks on secrets, AI attribution, oversized files, and policy violations.

#### Install

```bash
git clone https://github.com/torifo/skills-safe-commit /tmp/skills-safe-commit
cp -r /tmp/skills-safe-commit/safe-commit ~/.claude/skills/
```

#### Usage

Triggers before `git commit` with staged changes.

**What it checks:**
- Secrets and credentials (API keys, tokens, private keys)
- AI attribution in commit messages
- Oversized files (warn at 1MB, block at 5MB)
- Policy violations (`.env` files, design assets in wrong dirs)

**What it does:**
- Blocks the commit with clear reasons if any check fails
- Approves and shows commit preview if all checks pass

#### Related Skills

- [skills-secret-scan](https://github.com/torifo/skills-secret-scan) — deeper secret scanning across files and history
- [skills-commit](https://github.com/torifo/skills-commit) — bilingual commit workflow to run after safe-commit approves

---

## 日本語

### skills-safe-commit

> コミット前にシークレット・AI帰属・ポリシー違反を検証してブロックする

[Claude Code](https://claude.ai/code) のスキル。コミット前にステージ済み変更を検証し、シークレット・AI帰属・大容量ファイル・ポリシー違反があればブロックします。

#### インストール

```bash
git clone https://github.com/torifo/skills-safe-commit /tmp/skills-safe-commit
cp -r /tmp/skills-safe-commit/safe-commit ~/.claude/skills/
```

#### 使い方

ステージ済み変更がある状態で `git commit` 実行前に起動します。

**検証内容:**
- シークレット・認証情報（APIキー、トークン、秘密鍵）
- コミットメッセージのAI帰属
- 大容量ファイル（1MB警告・5MBブロック）
- ポリシー違反（.envファイル、誤ったディレクトリのデザインアセット）

#### 関連スキル

- [skills-secret-scan](https://github.com/torifo/skills-secret-scan) — ファイル・履歴全体への深いシークレットスキャン
- [skills-commit](https://github.com/torifo/skills-commit) — safe-commit承認後に使う英日バイリンガルコミット
