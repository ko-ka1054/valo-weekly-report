# Valorant情報収集エージェント

## このプロジェクトの目的

Playwright MCPを使ってブラウザを操作し、Valorantの最新情報を自動収集してMarkdownレポートを生成する。
主目的は**Playwright MCPの動作検証・活用習得**。将来的には品質推進業務の週次レポート自動化に展開予定。

## 使い方

このディレクトリをClaude Codeで開くと、`.mcp.json`の設定によりPlaywright MCPサーバが自動的に利用可能になる。
Claude Codeに以下のように依頼するだけで情報収集が始まる：

```
Valorant情報を収集してレポートを作成してください
```

## 収集タスク定義

Claudeは以下の手順で情報を収集すること。

### 1. エージェントTier情報（★★★ 最優先）

- **URL**: https://tracker.gg/valorant/articles/valorant-agent-tier-list
- **収集内容**: 現在のメタにおけるエージェントTier表（S/A/B/C/Dなど）と推奨構成
- **注意**: `/*/profile/*` と `/*/matches/*` はrobots.txtでDisallowのためアクセス禁止

### 2. Omen 立ち回りTips（★★★ 最優先）

- **URL**: https://www.proguides.com/valorant/agents/omen/
- **収集内容**: Omen（コントローラー）の立ち回り・スキルコンボ・ポジション解説
- **補足**: Feydhスタイルの攻撃的なOmen運用に関する記述を重点的に収集

### 3. マップ別定石（★★☆ 中優先）

- **ヘイブン**: スパイク設置場所・初動セットアップ・煙幕ポジション
- **アセント**: 同上
- **検索方法**: ProGuides または Liquipedia（https://liquipedia.net/valorant/）で検索

## 出力仕様

### ファイル名
`reports/valorant_report_YYYYMMDD.md`（当日の日付）

### レポート構成

```markdown
# Valorant情報レポート YYYY-MM-DD

## メタ情報 — エージェントTier

（Tier表と推奨構成）

## 立ち回りTips — Omen

（Feydhスタイル・スキルコマンド・ポジション）

## マップ別定石

### ヘイブン
（定石セットアップ）

### アセント
（定石セットアップ）

---
*参照元・取得日時*
- Tracker.gg: <URL> (取得: YYYY-MM-DD HH:MM)
- ProGuides: <URL> (取得: YYYY-MM-DD HH:MM)
```

## 制約事項

- robots.txtのDisallowパスへのアクセス禁止（`/*/profile/*`, `/*/matches/*`）
- ログイン不要な公開ページのみ対象
- 個人利用に限定
