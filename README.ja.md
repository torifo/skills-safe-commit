# skills-safe-commit

> コミット前にシークレット・AI帰属・ポリシー違反を検証してブロックする

[Claude Code](https://claude.ai/code) のスキル。コミット前にステージ済み変更を検証し、シークレット・AI帰属・大容量ファイル・ポリシー違反があればブロックします。

[English README](./README.md)

## インストール

```bash
git clone https://github.com/torifo/skills-safe-commit /tmp/skills-safe-commit
cp -r /tmp/skills-safe-commit/safe-commit ~/.claude/skills/
```

## 使い方

ステージ済み変更がある状態で `git commit` 実行前に起動します。

**検証内容:**
- シークレット・認証情報（APIキー、トークン、秘密鍵）
- コミットメッセージのAI帰属
- 大容量ファイル（1MB警告・5MBブロック）
- ポリシー違反（.envファイル、誤ったディレクトリのデザインアセット）

**動作:**
- 違反があればブロックと理由を表示
- 全チェック通過で承認とコミットプレビューを表示

## 関連スキル

- [skills-secret-scan](https://github.com/torifo/skills-secret-scan) — ファイル・履歴全体への深いシークレットスキャン
- [skills-commit](https://github.com/torifo/skills-commit) — safe-commit承認後に使う英日バイリンガルコミット
